---
solution: Experience Platform
title: Gruppo di campi schema Consensi e preferenze
description: Scopri il gruppo di campi schema Consensi e preferenze.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# [!UICONTROL Consensi e preferenze] gruppo di campi

[!UICONTROL Consensi e preferenze] è un gruppo di campi standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) che acquisisce informazioni sul consenso e sulle preferenze per un singolo cliente.

>[!NOTE]
>
>Poiché questo gruppo di campi è compatibile solo con [!DNL XDM Individual Profile], non può essere utilizzato per [!DNL XDM ExperienceEvent] schemi. Se desideri includere i dati sul consenso e sulle preferenze nello schema Experience Event, aggiungi allo schema il tipo di dati [[!UICONTROL Consenso per privacy, Personalization e preferenze di marketing]](../../data-types/consents.md) tramite un [gruppo di campi personalizzato](../../ui/resources/field-groups.md#create).

## Struttura del gruppo di campi {#structure}

Il gruppo di campi [!UICONTROL Consensi e preferenze] fornisce un singolo campo di tipo oggetto, `consents`, per acquisire informazioni sul consenso e sulle preferenze. Questo campo estende il tipo di dati [[!UICONTROL Consenso per privacy, Personalization e preferenze di marketing]](../../data-types/consents.md), rimuovendo il campo `adID` e aggiungendo un campo mappa `idSpecific`.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consulta la guida su [esplorazione delle risorse XDM](../../ui/explore.md) in per i passaggi su come cercare qualsiasi risorsa XDM e ispezionarne la struttura nell&#39;interfaccia utente di Platform.

Il seguente codice JSON mostra un esempio del tipo di dati che il gruppo di campi [!UICONTROL Consensi e preferenze] può elaborare. Per informazioni su come utilizzare la maggior parte dei campi forniti dal gruppo di campi, fare riferimento alla guida sul tipo di dati [Consensi e preferenze](../../data-types/consents.md). Le sottosezioni seguenti si concentrano sugli attributi univoci aggiunti dal gruppo di campi al tipo di dati.

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
>* [Genera dati di esempio nell&#39;interfaccia utente](../../ui/sample.md)
>* [Genera dati di esempio nell&#39;API](../../api/sample-data.md)

### `idSpecific`

`idSpecific` può essere utilizzato quando un particolare consenso o preferenza non si applica universalmente a un cliente, ma è limitato a un singolo dispositivo o ID. Ad esempio, un cliente può rinunciare alla ricezione di e-mail a un indirizzo, consentendo potenzialmente l’invio di e-mail a un altro.

>[!IMPORTANT]
>
>I consensi e le preferenze a livello di canale (ovvero quelli forniti in `consents` al di fuori di `idSpecific`) si applicano a tutti gli ID all&#39;interno di quel canale. Pertanto, tutti i consensi e le preferenze a livello di canale influiscono direttamente sul rispetto delle impostazioni equivalenti specifiche per ID o dispositivo:
>
>* Se il cliente ha rinunciato a livello di canale, tutti i consensi o le preferenze equivalenti in `idSpecific` vengono ignorati.
>* Se il consenso o la preferenza a livello di canale non è impostata o il cliente ha acconsentito, vengono rispettati i consensi o le preferenze equivalenti in `idSpecific`.

Ogni chiave nell&#39;oggetto `idSpecific` rappresenta uno spazio dei nomi di identità specifico riconosciuto da Adobe Experience Platform Identity Service. Sebbene sia possibile definire spazi dei nomi personalizzati per categorizzare diversi identificatori, si consiglia di utilizzare uno degli spazi dei nomi standard forniti da Identity Service per ridurre le dimensioni di archiviazione per Real-Time Customer Profile. Per ulteriori informazioni sugli spazi dei nomi di identità, consulta la [panoramica dello spazio dei nomi di identità](../../../identity-service/features/namespaces.md) nella documentazione di Identity Service.

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

All&#39;interno di `marketing` oggetti forniti nella sezione `idSpecific`, i campi `any` e `preferred` non sono supportati. Questi campi possono essere configurati solo a livello di utente. Inoltre, le preferenze di marketing `idSpecific` per `email`, `sms` e `push` non supportano i campi `subscriptions`.

È inoltre possibile fornire un consenso solo nella sezione `idSpecific`: `adID`. Questo campo è trattato nella sottosezione seguente.

#### `adID`

Il consenso `adID` rappresenta il consenso del cliente per l&#39;utilizzo di un ID inserzionista (IDFA o GAID) per collegare il cliente tra le app su questo dispositivo. Questo valore può essere configurato solo nello spazio dei nomi dell&#39;identità `ECID` nella sezione `idSpecific` e non può essere impostato per altri spazi dei nomi o a livello di utente per questo gruppo di campi.

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

Per utilizzare il gruppo di campi [!UICONTROL Consensi e preferenze] per acquisire i dati sul consenso dai clienti, è necessario creare un set di dati basato su uno schema che contiene tale gruppo di campi.

Consulta l&#39;esercitazione sulla [creazione di uno schema nell&#39;interfaccia utente](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) per i passaggi su come assegnare gruppi di campi ai campi. Dopo aver creato uno schema contenente un campo con il gruppo di campi [!UICONTROL Consensi e preferenze], consulta la sezione sulla [creazione di un set di dati](../../../catalog/datasets/user-guide.md#create) nella guida utente del set di dati, seguendo i passaggi per creare un set di dati con uno schema esistente.

>[!IMPORTANT]
>
>Per inviare i dati sul consenso a [!DNL Real-Time Customer Profile], è necessario creare uno schema abilitato per [!DNL Profile] basato sulla classe [!DNL XDM Individual Profile] che contiene il gruppo di campi [!UICONTROL Consensi e preferenze]. Il set di dati creato in base a tale schema deve essere abilitato anche per [!DNL Profile]. Fare riferimento ai tutorial collegati in precedenza per i passaggi specifici relativi ai requisiti di [!DNL Real-Time Customer Profile] per schemi e set di dati.
>
>Inoltre, devi anche assicurarti che i criteri di unione siano configurati per assegnare la priorità ai set di dati che contengono i dati di consenso e preferenze più recenti, al fine di aggiornare correttamente i profili dei clienti. Per ulteriori informazioni, consulta la panoramica sui [criteri di unione](../../../rtcdp/profile/merge-policies.md).

## Gestione delle modifiche di consenso e preferenze

Quando un cliente cambia il proprio consenso o le proprie preferenze sul sito Web, le modifiche devono essere raccolte e applicate immediatamente tramite [Adobe Experience Platform Web SDK](../../../web-sdk/commands/setconsent.md). Se un cliente rinuncia alla raccolta dei dati, tutta la raccolta dei dati deve cessare immediatamente. Se un cliente rinuncia alla personalizzazione, significa che non dovrebbe essere presente alcuna personalizzazione nella pagina successiva in cui visita.

## Passaggi successivi

Questo documento descrive la struttura e l&#39;utilizzo del gruppo di campi [!UICONTROL Consensi e preferenze]. Per ulteriori informazioni sugli altri campi forniti dal gruppo di campi, consulta il documento sul tipo di dati [[!UICONTROL Consenso per privacy, Personalization e preferenze di marketing]](../../data-types/consents.md).
