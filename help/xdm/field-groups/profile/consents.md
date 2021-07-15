---
solution: Experience Platform
title: Gruppo di campi schema Consensi e Preferenze
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Consensi e Preferenze .
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '2316'
ht-degree: 2%

---

# [!UICONTROL Gruppo Consensi e ] campi Preferenze

[!UICONTROL Consensi e ]preferenze è un gruppo di campi standard per la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md), utilizzato per acquisire le informazioni sul consenso e sulle preferenze del cliente.

>[!NOTE]
>
>Poiché questo gruppo di campi è compatibile solo con [!DNL XDM Individual Profile], non può essere utilizzato per gli schemi [!DNL XDM ExperienceEvent]. Se desideri includere i dati di consenso e preferenza nello schema Evento esperienza, aggiungi allo schema il tipo di dati [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences]](../../data-types/consents.md) tramite un gruppo di campi [personalizzato](../../ui/resources/field-groups.md#create).

## Struttura del gruppo di campi {#structure}

>[!IMPORTANT]
>
>Il gruppo di campi [!UICONTROL Consensi e Preferenze] è progettato per coprire una serie di casi d&#39;uso di gestione del consenso e delle preferenze. Di conseguenza, in questo documento viene descritto l&#39;utilizzo dei campi del gruppo di campi in termini generali e vengono forniti solo suggerimenti su come interpretare l&#39;utilizzo di tali campi. Consulta il team legale per la privacy per allineare la struttura del gruppo di campi con il modo in cui l’organizzazione interpreta e presenta ai clienti queste scelte di consenso e preferenza.

Il gruppo di campi [!UICONTROL Consensi e Preferenze] fornisce diversi campi utilizzati per acquisire le informazioni relative a **consenso** e **preferenza**.

Un consenso è un’opzione che consente al cliente di specificare come utilizzare i propri dati. La maggior parte dei consensi ha un aspetto legale, in quanto alcune giurisdizioni richiedono l’ottenimento di un’autorizzazione prima che i dati possano essere utilizzati in un modo particolare, o richiedono che il cliente abbia la possibilità di interrompere tale uso (rinuncia) se non è richiesto il consenso positivo.

Una preferenza è un’opzione che consente al cliente di specificare come devono essere gestiti i diversi aspetti della propria esperienza con un marchio. Questi rientrano in due categorie:

* **Preferenze** di personalizzazione: Preferenze relative al modo in cui il marchio deve personalizzare le esperienze consegnate a un cliente.
* **Preferenze** di marketing: Preferenze relative all’autorizzazione o meno di un marchio a contattare un cliente attraverso vari canali.

La schermata seguente mostra come la struttura del gruppo di campi è rappresentata nell’interfaccia utente di Platform:

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consulta la guida [esplorazione delle risorse XDM](../../ui/explore.md) in per i passaggi su come cercare una risorsa XDM ed esaminarne la struttura nell’interfaccia utente di Platform.

Il seguente JSON mostra un esempio del tipo di dati che il gruppo di campi [!UICONTROL Consensi e Preferenze] può elaborare. Le informazioni sull&#39;uso specifico di ciascuno di questi campi sono fornite nelle sezioni seguenti.

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
* [Generare dati di esempio nell’API](../../api/sample-data.md)


## Casi di utilizzo del campo

I casi d’uso previsti per ciascuno di questi campi sono descritti nelle sezioni seguenti.

### `collect`

`collect` rappresenta il consenso del cliente alla raccolta dei dati.

```json
"collect" : {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornito dal cliente per questo caso d’uso. Per i valori e le definizioni accettati, consultare l&#39; [appendice](#choice-values) . |

{style=&quot;table-layout:auto&quot;}

### `share`

`share` rappresenta il consenso del cliente per sapere se i suoi dati possono essere condivisi con (o venduti a) seconde o terze parti.

```json
"share" : {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornito dal cliente per questo caso d’uso. Per i valori e le definizioni accettati, consultare l&#39; [appendice](#choice-values) . |

{style=&quot;table-layout:auto&quot;}

### `personalize` {#personalize}

`personalize` acquisisce le preferenze del cliente riguardo a quali modi i loro dati possono essere utilizzati per la personalizzazione. I clienti possono rinunciare a casi d’uso di personalizzazione specifici o rinunciare completamente alla personalizzazione.

>[!IMPORTANT]
`personalize` non copre i casi d’uso di marketing. Ad esempio, se un cliente rinuncia alla personalizzazione per tutti i canali, non deve smettere di ricevere comunicazioni attraverso tali canali. Piuttosto, i messaggi che ricevono devono essere generici e non basati sul loro profilo.
Nello stesso esempio, se un cliente rinuncia al marketing diretto per tutti i canali (tramite `marketing`, spiegato nella [sezione successiva](#marketing)), non deve ricevere alcun messaggio, anche se è consentita la personalizzazione.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `content` | Rappresenta le preferenze del cliente per i contenuti personalizzati sul sito web o sull&#39;applicazione. |
| `val` | Preferenza di personalizzazione fornita dal cliente per il caso d’uso specificato. Nei casi in cui al cliente non venga richiesto di fornire il consenso, il valore di questo campo deve indicare la base su cui dovrebbe avvenire la personalizzazione. Per i valori e le definizioni accettati, consultare l&#39; [appendice](#choice-values) . |

{style=&quot;table-layout:auto&quot;}

### `marketing` {#marketing}

`marketing` acquisisce le preferenze dei clienti per quanto riguarda le finalità di marketing per le quali i loro dati possono essere utilizzati. I clienti possono rinunciare a casi d’uso di marketing specifici o rinunciare completamente al marketing diretto.

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `preferred` | Indica il canale preferito dal cliente per la ricezione delle comunicazioni. Vedere l&#39; [appendice](#preferred-values) per i valori accettati. |
| `any` | Rappresenta le preferenze del cliente per il marketing diretto nel suo insieme. La preferenza di consenso fornita in questo campo è considerata come la preferenza &quot;predefinita&quot; per qualsiasi canale di marketing, a meno che non venga bypassata da altri sottocampi forniti in `marketing`. Se prevedi di utilizzare opzioni di consenso più granulari, escludi questo campo.<br><br>Se il valore è impostato su  `n`, tutte le impostazioni di personalizzazione più specifiche devono essere ignorate. Se il valore è impostato su `y`, anche tutte le opzioni di personalizzazione a grana fine devono essere trattate come `y`, a meno che non siano impostate esplicitamente su `n`. Se il valore non viene impostato, i valori per ogni opzione di personalizzazione devono essere rispettati come specificato. |
| `email` | Indica se il cliente accetta di ricevere messaggi e-mail. Il cliente può anche fornire preferenze per le sottoscrizioni individuali all&#39;interno di questo canale. Per ulteriori informazioni, consulta la sezione su [abbonamenti](#subscriptions) di seguito. |
| `push` | Indica se il cliente consente la ricezione di notifiche push. Il cliente può anche fornire preferenze per le sottoscrizioni individuali all&#39;interno di questo canale. Per ulteriori informazioni, consulta la sezione su [abbonamenti](#subscriptions) di seguito. |
| `sms` | Indica se il cliente accetta di ricevere messaggi di testo. Il cliente può anche fornire preferenze per le sottoscrizioni individuali all&#39;interno di questo canale. Per ulteriori informazioni, consulta la sezione su [abbonamenti](#subscriptions) di seguito. |
| `val` | La preferenza fornita dal cliente per il caso d’uso specificato. Nei casi in cui non sia necessario chiedere al cliente di fornire il consenso, il valore di questo campo deve indicare la base su cui deve avvenire il caso d’uso del marketing. Per i valori e le definizioni accettati, consultare l&#39; [appendice](#choice-values) . |
| `time` | Una marca temporale ISO 8601 di quando la preferenza di marketing è cambiata, se applicabile. Tieni presente che se la marca temporale per una singola preferenza è la stessa di quella fornita in `metadata`, questo campo non deve essere impostato per tale preferenza. |
| `reason` | Quando un cliente rinuncia a un caso di utilizzo marketing, questo campo stringa rappresenta il motivo per cui il cliente ha rinunciato. |

{style=&quot;table-layout:auto&quot;}

#### `subscriptions` {#subscriptions}

Le proprietà `email`, `push` e `sms` dell&#39;oggetto `marketing` sono in grado di rappresentare le sottoscrizioni dei clienti per tali singoli canali. A questo scopo, aggiungi una proprietà `subscriptions` al canale di marketing in questione.

```json
"marketing": {
  "email": {
    "val": "y",
    "subscriptions": {
      "daily-mail": {
        "val": "y",
        "type": "paid",
        "subscribers": {
          "john@xyz.com": {
            "time": "2019-01-01T15:52:25+00:00",
            "source": "website"
          }
        }
      },
      "shipped": {
        "val": "y",

        "subscribers": {
          "john@xyz.com": {
            "time": "2021-01-01T08:32:53+07:00",
            "source": "website"
          },
          "jane@xyz.com": {
            "time": "2020-02-03T07:54:21+07:00",
            "source": "call center",
          }
        }
      }
    }
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `type` | Tipo di sottoscrizione. Può trattarsi di una qualsiasi stringa descrittiva, purché non contenga più di 15 caratteri. |
| `subscribers` | Un campo di tipo mappa facoltativo che rappresenta un insieme di identificatori (ad esempio indirizzi e-mail o numeri di telefono) che hanno effettuato la sottoscrizione a una particolare sottoscrizione. Ogni chiave in questo oggetto rappresenta l&#39;identificatore in questione e contiene due sottoproprietà: <ul><li>`time`: Una marca temporale ISO 8601 del momento in cui l’identità è stata sottoscritta, se applicabile.</li><li>`source`: Origine dell&#39;utente che ha effettuato l&#39;abbonamento. Può trattarsi di una qualsiasi stringa descrittiva, purché non contenga più di 15 caratteri.</li></ul> |

{style=&quot;table-layout:auto&quot;}


### `metadata`

`metadata` acquisisce metadati generali sul consenso e le preferenze del cliente ogni volta che sono stati aggiornati per l&#39;ultima volta.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Proprietà | Descrizione |
| --- | --- |
| `time` | Una marca temporale ISO 8601 per l&#39;ultima volta che è stato aggiornato il consenso e le preferenze del cliente. Questo campo può essere utilizzato invece di applicare marche temporali alle singole preferenze per ridurre carico e complessità. Se si fornisce un valore `time` sotto una singola preferenza, la marca temporale `metadata` viene ignorata rispetto a quella specifica preferenza. |

{style=&quot;table-layout:auto&quot;}

### `idSpecific`

`idSpecific` può essere utilizzato quando un determinato consenso o preferenza non si applica universalmente a un cliente, ma è limitato a un singolo dispositivo o ID. Ad esempio, un cliente può negare la ricezione di e-mail a un indirizzo, consentendo al contempo potenzialmente l’invio di e-mail a un altro.

>[!IMPORTANT]
I consensi e le preferenze a livello di canale (ovvero quelli forniti sotto `consents` al di fuori di `idSpecific`) si applicano agli ID all&#39;interno di quel canale. Pertanto, tutti i consensi e le preferenze a livello di canale influiscono direttamente sul rispetto delle impostazioni equivalenti per ID o dispositivi:
* Se il cliente ha rinunciato a livello di canale, tutti i consensi o le preferenze equivalenti in `idSpecific` vengono ignorati.
* Se il consenso o la preferenza a livello di canale non è impostato o il cliente ha acconsentito, vengono rispettati i consensi o le preferenze equivalenti in `idSpecific`.


Ogni chiave nell’oggetto `idSpecific` rappresenta uno spazio dei nomi di identità specifico riconosciuto dal servizio Adobe Experience Platform Identity. Sebbene sia possibile definire namespace personalizzati per classificare identificatori diversi, si consiglia di utilizzare uno dei namespace standard forniti dal servizio Identity per ridurre le dimensioni di archiviazione per Profilo cliente in tempo reale. Per ulteriori informazioni sugli spazi dei nomi delle identità, consulta la [panoramica dello spazio dei nomi delle identità](../../../identity-service/namespaces.md) nella documentazione del servizio Identity.

Le chiavi di ciascun oggetto namespace rappresentano i valori di identità univoci per i quali il cliente ha impostato le preferenze. Ogni valore di identità può contenere un set completo di consensi e preferenze, formattato nello stesso modo di `consents`.

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
  "ECID" : {
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

All&#39;interno degli oggetti `marketing` forniti nella sezione `idSpecific`, i campi `any` e `preferred` non sono supportati. Questi campi possono essere configurati solo a livello utente. Inoltre, le `idSpecific` preferenze di marketing per i campi `email`, `sms` e `push` non supportano i campi `subscriptions`.

Esiste anche un consenso che può essere fornito solo nella sezione `idSpecific` : `adID`. Questo campo è trattato nella sottosezione seguente.

#### `adID`

Il consenso `adID` rappresenta il consenso del cliente circa la possibilità di utilizzare un ID inserzionista (IDFA o GAID) per collegare il cliente tra le app su questo dispositivo. Questo valore può essere configurato solo sotto lo spazio dei nomi `ECID` identity nella sezione `idSpecific` e non può essere impostato per altri namespace o a livello di utente per questo gruppo di campi.

```json
"idSpecific": {
  "ECID" : {
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
Non devi impostare questo valore direttamente, poiché l’SDK di Adobe Experience Platform Mobile lo imposta automaticamente quando appropriato.

## Acquisizione di dati tramite il gruppo di campi {#ingest}

Per utilizzare il gruppo di campi [!UICONTROL Consensi e Preferenze] per acquisire i dati di consenso dai clienti, è necessario creare un set di dati basato su uno schema che contiene tale gruppo di campi.

Per istruzioni su come assegnare gruppi di campi ai campi, consulta l’esercitazione su [creazione di uno schema nell’interfaccia utente](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) . Dopo aver creato uno schema contenente un campo con il gruppo di campi [!UICONTROL Consensi e Preferenze], consulta la sezione relativa alla creazione di un set di dati](../../../catalog/datasets/user-guide.md#create) nella guida utente del set di dati, seguendo i passaggi necessari per creare un set di dati con uno schema esistente.[

>[!IMPORTANT]
Se desideri inviare i dati di consenso a [!DNL Real-time Customer Profile], è necessario creare uno schema abilitato [!DNL Profile] in base alla classe [!DNL XDM Individual Profile] che contiene il gruppo di campi [!UICONTROL Consensi e Preferenze]. Anche il set di dati creato in base a tale schema deve essere abilitato per [!DNL Profile]. Fai riferimento alle esercitazioni collegate sopra per passaggi specifici relativi ai requisiti [!DNL Real-time Customer Profile] per schemi e set di dati.
Inoltre, è necessario assicurarsi che i criteri di unione siano configurati per assegnare priorità ai set di dati contenenti i dati di consenso e preferenza più recenti, in modo che i profili cliente vengano aggiornati correttamente. Per ulteriori informazioni, consulta la panoramica sui [criteri di unione](../../../rtcdp/profile/merge-policies.md) .

## Gestione delle modifiche di consenso e preferenza

Quando un cliente modifica i propri consensi o preferenze sul sito web, queste modifiche devono essere raccolte e applicate immediatamente utilizzando l&#39; [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Se un cliente rinuncia alla raccolta di dati, tutte le raccolte di dati devono cessare immediatamente. Se un cliente rinuncia alla personalizzazione, non dovrebbe esserci alcuna personalizzazione nella pagina successiva che visita.

## Appendice {#appendix}

Le sezioni seguenti forniscono informazioni di riferimento aggiuntive relative al gruppo di campi [!UICONTROL Consensi e Preferenze].

### Valori accettati per `val` {#choice-values}

La tabella seguente illustra i valori accettati per `val`:

| Valore | Title | Descrizione |
| --- | --- | --- |
| `y` | Sì | Il cliente ha acconsentito o preferenza. In altre parole, **do** acconsentono all&#39;uso dei propri dati come indicato dal consenso o dalla preferenza in questione. |
| `n` | No | Il cliente ha rinunciato al consenso o alla preferenza. In altre parole, **non** acconsentono all&#39;uso dei propri dati come indicato dal consenso o dalla preferenza in questione. |
| `p` | Verifica in sospeso | Il sistema non ha ancora ricevuto un consenso o un valore di preferenza finale. Viene utilizzato più spesso come parte di un consenso che richiede una verifica in due fasi. Ad esempio, se un cliente sceglie di ricevere le e-mail, il consenso viene impostato su `p` fino a quando non seleziona un collegamento in un’e-mail per verificare di aver fornito l’indirizzo e-mail corretto, al punto in cui il consenso viene aggiornato a `y`.<br><br>Se questo consenso o preferenza non utilizza un processo di verifica a due set, la  `p` scelta può essere invece utilizzata per indicare che il cliente non ha ancora risposto al prompt del consenso. Ad esempio, puoi impostare automaticamente il valore su `p` nella prima pagina di un sito web, prima che il cliente risponda al prompt del consenso. Nelle giurisdizioni che non richiedono un consenso esplicito, puoi anche utilizzarlo per indicare che il cliente non ha esplicitamente rinunciato (in altre parole, si presume che il consenso sia). |
| `u` | Sconosciuto | Le informazioni sul consenso o sulle preferenze del cliente sono sconosciute. |
| `LI` | Interesse legittimo | Il legittimo interesse commerciale a raccogliere ed elaborare tali dati per lo scopo specificato supera il potenziale danno che essi comportano per l&#39;individuo. |
| `CT` | Contratto | La raccolta dei dati per lo scopo specificato è necessaria per adempiere agli obblighi contrattuali con la persona fisica. |
| `CP` | Rispetto di un obbligo giuridico | La raccolta dei dati per lo scopo specificato è necessaria per soddisfare gli obblighi legali dell&#39;impresa. |
| `VI` | Interesse fondamentale del singolo | La raccolta dei dati per lo scopo specifico è necessaria per tutelare gli interessi vitali dell&#39;individuo. |
| `PI` | Interesse pubblico | La raccolta dei dati per lo scopo specificato è necessaria per svolgere un compito di interesse pubblico o nell&#39;esercizio di un&#39;autorità ufficiale. |

{style=&quot;table-layout:auto&quot;}

### Valori accettati per `preferred` {#preferred-values}

La tabella seguente illustra i valori accettati per `preferred`:

| Valore | Descrizione |
| --- | --- |
| `email` | Messaggi e-mail. |
| `push` | Notifiche push. |
| `inApp` | Messaggi in-app. |
| `sms` | Messaggi SMS. |
| `phone` | Interazioni telefoniche. |
| `phyMail` | Posta fisica. |
| `inVehicle` | Messaggi di bordo. |
| `inHome` | Messaggi interni. |
| `iot` | Internet dei messaggi di cose (IoT). |
| `social` | Contenuto social media. |
| `other` | Canale che non rientra in una categoria standard. |
| `none` | Nessun canale preferito. |
| `unknown` | Il canale preferito è sconosciuto. |

{style=&quot;table-layout:auto&quot;}

### Schema completo [!UICONTROL Consensi e preferenze] {#full-schema}

Per visualizzare lo schema completo del gruppo di campi [!UICONTROL Consensi e Preferenze], consulta l’ [archivio XDM ufficiale](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
