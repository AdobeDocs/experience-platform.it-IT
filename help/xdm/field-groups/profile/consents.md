---
solution: Experience Platform
title: Gruppo di campi schema Consensi e Preferenze
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Consensi e Preferenze .
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# [!UICONTROL Consensi e preferenze] gruppo di campi

[!UICONTROL Consensi e preferenze] è un gruppo di campi standard per [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md) che acquisisce le informazioni sul consenso e sulle preferenze di un singolo cliente.

>[!NOTE]
>
>Poiché questo gruppo di campi è compatibile solo con [!DNL XDM Individual Profile], non può essere utilizzato per [!DNL XDM ExperienceEvent] schemi. Se desideri includere i dati di consenso e preferenza nello schema Evento esperienza, aggiungi la [[!UICONTROL Consenso per privacy, personalizzazione e preferenze di marketing] tipo di dati](../../data-types/consents.md) allo schema tramite l&#39;utilizzo di un [gruppo di campi personalizzato](../../ui/resources/field-groups.md#create) invece.

## Struttura del gruppo di campi {#structure}

La [!UICONTROL Consensi e preferenze] un gruppo di campi fornisce un singolo campo di tipo oggetto, `consents`, per acquisire informazioni sul consenso e sulle preferenze. Questo campo estende [[!UICONTROL Consenso per privacy, personalizzazione e preferenze di marketing] tipo di dati](../../data-types/consents.md), rimuovendo `adID` campo e aggiunta di un `idSpecific` campo mappa.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consulta la guida su [esplorazione delle risorse XDM](../../ui/explore.md) per informazioni su come cercare una risorsa XDM ed esaminarne la struttura nell’interfaccia utente di Platform.

Il seguente JSON mostra un esempio del tipo di dati che [!UICONTROL Consensi e preferenze] gruppo di campi può elaborare. Per informazioni su come utilizzare la maggior parte dei campi forniti dal gruppo di campi, consulta la guida nella sezione [Tipo di dati Consensi e Preferenze](../../data-types/consents.md). Le sottosezioni qui sotto si concentrano sugli attributi univoci che il gruppo di campi aggiunge al tipo di dati.

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>Puoi generare dati JSON di esempio per qualsiasi schema XDM definito in Experience Platform, in modo da visualizzare in che modo i dati di consenso e preferenza dei clienti devono essere mappati. Per ulteriori informazioni, consulta la seguente documentazione:
>
>* [Generare dati di esempio nell’interfaccia utente](../../ui/sample.md)
>* [Generare dati di esempio nell’API](../../api/sample-data.md)


### `idSpecific`

`idSpecific` può essere utilizzato quando un determinato consenso o preferenza non si applica universalmente a un cliente, ma è limitato a un singolo dispositivo o ID. Ad esempio, un cliente può negare la ricezione di e-mail a un indirizzo, consentendo al contempo potenzialmente l’invio di e-mail a un altro.

>[!IMPORTANT]
>
>Consensi e preferenze a livello di canale (ossia quelli forniti in `consents` fuori `idSpecific`) si applica a tutti gli ID all&#39;interno di quel canale. Pertanto, tutti i consensi e le preferenze a livello di canale influiscono direttamente sul rispetto delle impostazioni equivalenti per ID o dispositivi:
>
>* Se il cliente ha rinunciato a livello di canale, allora tutti i consensi o preferenze equivalenti in `idSpecific` vengono ignorati.
>* Se il consenso o la preferenza a livello di canale non è impostato o il cliente ha acconsentito, il consenso o le preferenze equivalenti in `idSpecific` sono onorati.


Ogni chiave nel `idSpecific` l’oggetto rappresenta uno spazio dei nomi di identità specifico riconosciuto dal servizio Adobe Experience Platform Identity. Sebbene sia possibile definire namespace personalizzati per classificare identificatori diversi, si consiglia di utilizzare uno dei namespace standard forniti dal servizio Identity per ridurre le dimensioni di archiviazione per il profilo cliente in tempo reale. Per ulteriori informazioni sugli spazi dei nomi delle identità, consulta la sezione [panoramica dello spazio dei nomi identità](../../../identity-service/namespaces.md) nella documentazione del servizio Identity.

Le chiavi di ciascun oggetto namespace rappresentano i valori di identità univoci per i quali il cliente ha impostato le preferenze. Ogni valore di identità può contenere un insieme completo di consensi e preferenze, formattati nello stesso modo `consents`.

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID": {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

Within `marketing` gli oggetti forniti nel `idSpecific` la sezione `any` e `preferred` campi non supportati. Questi campi possono essere configurati solo a livello utente. Inoltre, il `idSpecific` preferenze di marketing per `email`, `sms`e `push` non supporta `subscriptions` campi.

Esiste anche un consenso che può essere fornito solo nel `idSpecific` sezione: `adID`. Questo campo è trattato nella sottosezione seguente.

#### `adID`

La `adID` il consenso rappresenta il consenso del cliente per sapere se un ID inserzionista (IDFA o GAID) può essere utilizzato per collegare il cliente tra le app su questo dispositivo. Questo valore può essere configurato solo in `ECID` spazio dei nomi identità nel `idSpecific` e non può essere impostato per altri namespace o a livello di utente per questo gruppo di campi.

```json
"idSpecific": {
  "ECID": {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
>
>Non devi impostare questo valore direttamente, poiché l’SDK di Adobe Experience Platform Mobile lo imposta automaticamente quando appropriato.

## Acquisizione di dati tramite il gruppo di campi {#ingest}

Per utilizzare il [!UICONTROL Consensi e preferenze] gruppo di campi per acquisire i dati di consenso dai clienti, devi creare un set di dati basato su uno schema che contiene tale gruppo di campi.

Guarda l’esercitazione su [creazione di uno schema nell’interfaccia utente](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) per i passaggi su come assegnare gruppi di campi ai campi. Una volta creato uno schema contenente un campo con [!UICONTROL Consensi e preferenze] gruppo di campi, consulta la sezione [creazione di un set di dati](../../../catalog/datasets/user-guide.md#create) nella guida utente del set di dati, segui i passaggi necessari per creare un set di dati con uno schema esistente.

>[!IMPORTANT]
>
>Se desideri inviare i dati di consenso a [!DNL Real-Time Customer Profile], è necessario creare un [!DNL Profile]schema abilitato basato su [!DNL XDM Individual Profile] la classe che contiene [!UICONTROL Consensi e preferenze] gruppo di campi. Anche il set di dati creato in base a tale schema deve essere abilitato per [!DNL Profile]. Per i passaggi specifici relativi a [!DNL Real-Time Customer Profile] requisiti per schemi e set di dati.
>
>Inoltre, è necessario assicurarsi che i criteri di unione siano configurati per assegnare priorità ai set di dati contenenti i dati di consenso e preferenza più recenti, in modo che i profili cliente vengano aggiornati correttamente. Vedi la panoramica su [criteri di unione](../../../rtcdp/profile/merge-policies.md) per ulteriori informazioni.

## Gestione delle modifiche di consenso e preferenza

Quando un cliente modifica il proprio consenso o le proprie preferenze sul sito web, queste modifiche devono essere raccolte e applicate immediatamente utilizzando il [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Se un cliente rinuncia alla raccolta di dati, tutte le raccolte di dati devono cessare immediatamente. Se un cliente rinuncia alla personalizzazione, non dovrebbe esserci alcuna personalizzazione nella pagina successiva che visita.

## Passaggi successivi

Il presente documento ha trattato la struttura e l&#39;uso [!UICONTROL Consensi e preferenze] gruppo di campi. Per ulteriori informazioni sugli altri campi forniti dal gruppo di campi, vedere il documento [[!UICONTROL Consenso per privacy, personalizzazione e preferenze di marketing] tipo di dati](../../data-types/consents.md).
