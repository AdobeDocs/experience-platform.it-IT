---
solution: Experience Platform
title: Gruppo di campi schema Consensi e preferenze
description: Scopri il gruppo di campi schema Consensi e preferenze.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# [!UICONTROL Consensi e preferenze] gruppo di campi

[!UICONTROL Consensi e preferenze] è un gruppo di campi standard per [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) che acquisisce informazioni sul consenso e sulle preferenze di un singolo cliente.

>[!NOTE]
>
>Poiché questo gruppo di campi è compatibile solo con [!DNL XDM Individual Profile], non può essere utilizzato per [!DNL XDM ExperienceEvent] schemi. Se desideri includere i dati sul consenso e sulle preferenze nello schema Experience Event, aggiungi [[!UICONTROL Consenso per le preferenze di privacy, personalizzazione e marketing] tipo di dati](../../data-types/consents.md) allo schema tramite l’utilizzo di un [gruppo di campi personalizzato](../../ui/resources/field-groups.md#create) invece.

## Struttura del gruppo di campi {#structure}

Il [!UICONTROL Consensi e preferenze] gruppo di campi fornisce un singolo campo di tipo oggetto, `consents`, per acquisire informazioni su consenso e preferenze. Questo campo estende [[!UICONTROL Consenso per le preferenze di privacy, personalizzazione e marketing] tipo di dati](../../data-types/consents.md), rimozione di `adID` e aggiungendo un `idSpecific` campo mappa.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consulta la guida su [esplorazione delle risorse XDM](../../ui/explore.md) per i passaggi su come cercare qualsiasi risorsa XDM e ispezionarne la struttura nell’interfaccia utente di Platform.

Il codice JSON seguente mostra un esempio del tipo di dati che [!UICONTROL Consensi e preferenze] gruppo di campi può elaborare. Per informazioni su come utilizzare la maggior parte dei campi forniti dal gruppo di campi, consulta la guida sulla [Tipo di dati Consensi e preferenze](../../data-types/consents.md). Le sottosezioni seguenti si concentrano sugli attributi univoci aggiunti dal gruppo di campi al tipo di dati.

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
>Puoi generare dati JSON di esempio per qualsiasi schema XDM definito in Experience Platform per aiutare a visualizzare in che modo devono essere mappati i dati sul consenso dei clienti e sulle preferenze. Per ulteriori informazioni, consulta la seguente documentazione:
>
>* [Generare dati di esempio nell’interfaccia utente](../../ui/sample.md)
>* [Generare dati di esempio nell’API](../../api/sample-data.md)

### `idSpecific`

`idSpecific` può essere utilizzato quando un particolare consenso o preferenza non si applica universalmente a un cliente, ma è limitato a un singolo dispositivo o ID. Ad esempio, un cliente può rinunciare alla ricezione di e-mail a un indirizzo, consentendo potenzialmente l’invio di e-mail a un altro.

>[!IMPORTANT]
>
>Consensi e preferenze a livello di canale (ovvero quelli forniti in `consents` all&#39;esterno di `idSpecific`) si applica a tutti gli ID all&#39;interno di quel canale. Pertanto, tutti i consensi e le preferenze a livello di canale influiscono direttamente sul rispetto delle impostazioni equivalenti specifiche per ID o dispositivo:
>
>* Se il cliente ha rinunciato a livello di canale, qualsiasi consenso o preferenza equivalente in `idSpecific` vengono ignorati.
>* Se il consenso o la preferenza a livello di canale non è impostata, o il cliente ha acconsentito, allora il consenso o le preferenze equivalenti in `idSpecific` sono onorati.

Ogni chiave nella `idSpecific` L’oggetto rappresenta uno spazio dei nomi di identità specifico riconosciuto da Adobe Experience Platform Identity Service. Sebbene sia possibile definire spazi dei nomi personalizzati per categorizzare diversi identificatori, si consiglia di utilizzare uno degli spazi dei nomi standard forniti da Identity Service per ridurre le dimensioni di archiviazione per Real-Time Customer Profile. Per ulteriori informazioni sugli spazi dei nomi di identità, consulta [panoramica dello spazio dei nomi delle identità](../../../identity-service/features/namespaces.md) nella documentazione del servizio Identity.

Le chiavi di ciascun oggetto spazio dei nomi rappresentano i valori di identità univoci per i quali il cliente ha impostato le preferenze. Ogni valore di identità può contenere un set completo di consensi e preferenze, formattato come `consents`.

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

Entro `marketing` oggetti forniti in `idSpecific` sezione, il `any` e `preferred` non sono supportati. Questi campi possono essere configurati solo a livello di utente. Inoltre, la `idSpecific` preferenze di marketing per `email`, `sms`, e `push` non supportano `subscriptions` campi.

Esiste anche un consenso che può essere fornito solo nel `idSpecific` sezione: `adID`. Questo campo è trattato nella sottosezione seguente.

#### `adID`

Il `adID` Il consenso rappresenta il consenso del cliente per indicare se è possibile utilizzare un ID inserzionista (IDFA o GAID) per collegare il cliente tra le app su questo dispositivo. Questo valore può essere configurato solo in `ECID` spazio dei nomi delle identità in `idSpecific` e non può essere impostata per altri namespace o a livello di utente per questo gruppo di campi.

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
>Non è previsto che questo valore venga impostato direttamente, poiché l’SDK di Adobe Experience Platform Mobile lo imposta automaticamente quando appropriato.

## Acquisizione di dati tramite il gruppo di campi {#ingest}

Per utilizzare il [!UICONTROL Consensi e preferenze] per acquisire i dati sul consenso dai clienti, devi creare un set di dati basato su uno schema che contiene tale gruppo di campi.

Guarda il tutorial su [creazione di uno schema nell’interfaccia utente](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) per i passaggi su come assegnare gruppi di campi ai campi. Dopo aver creato uno schema contenente un campo con il [!UICONTROL Consensi e preferenze] gruppo di campi, fare riferimento alla sezione [creazione di un set di dati](../../../catalog/datasets/user-guide.md#create) nella guida utente del set di dati, segui i passaggi per creare un set di dati con uno schema esistente.

>[!IMPORTANT]
>
>Se desideri inviare i dati sul consenso a [!DNL Real-Time Customer Profile], è necessario creare un’ [!DNL Profile]schema abilitato in base al [!DNL XDM Individual Profile] classe che contiene [!UICONTROL Consensi e preferenze] gruppo di campi. Il set di dati creato in base a tale schema deve essere abilitato anche per [!DNL Profile]. Fai riferimento ai tutorial collegati in precedenza per i passaggi specifici relativi a [!DNL Real-Time Customer Profile] requisiti per schemi e set di dati.
>
>Inoltre, devi anche assicurarti che i criteri di unione siano configurati per assegnare la priorità ai set di dati che contengono i dati di consenso e preferenze più recenti, al fine di aggiornare correttamente i profili dei clienti. Consulta la panoramica su [criteri di unione](../../../rtcdp/profile/merge-policies.md) per ulteriori informazioni.

## Gestione delle modifiche di consenso e preferenze

Quando un cliente modifica i propri consensi o preferenze sul sito web, queste modifiche devono essere raccolte e immediatamente applicate utilizzando [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Se un cliente rinuncia alla raccolta dei dati, tutta la raccolta dei dati deve cessare immediatamente. Se un cliente rinuncia alla personalizzazione, significa che non dovrebbe essere presente alcuna personalizzazione nella pagina successiva in cui visita.

## Passaggi successivi

Il presente documento riguarda la struttura e l&#39;uso del [!UICONTROL Consensi e preferenze] gruppo di campi. Per ulteriori informazioni sugli altri campi forniti dal gruppo di campi, vedere il documento relativo [[!UICONTROL Consenso per le preferenze di privacy, personalizzazione e marketing] tipo di dati](../../data-types/consents.md).
