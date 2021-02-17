---
keywords: ' Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;consenso;preferenze;preferenze;preferenze;privacyOptOuts;marketingPreferences;optOutType;baseOfProcessing;consenso;Consent'
title: Consensi e tipi di dati delle preferenze
description: Il tipo di dati Consent for Privacy, Personalization and Marketing Preferences (Consenso per privacy, Personalizzazione e Preferenze marketing) è inteso a supportare la raccolta di autorizzazioni e preferenze del cliente generate dalle piattaforme di gestione del consenso (CMP) e da altre fonti dalle operazioni sui dati.
topic: guide
translation-type: tm+mt
source-git-commit: 865379292985037b184d92e5d3fc1abc1873e962
workflow-type: tm+mt
source-wordcount: '2060'
ht-degree: 1%

---


# [!DNL Consents & Preferences] tipo di dati

Il tipo di dati [!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] (in seguito denominato &quot;tipo di dati &quot;[!DNL Consents & Preferences]&quot;) è un tipo di dati [!DNL Experience Data Model] (XDM) che è destinato a supportare la raccolta di autorizzazioni e preferenze del cliente generate dalle piattaforme di gestione del consenso (CMP) e da altre fonti dalle operazioni di dati.

Questo documento descrive la struttura e l&#39;uso previsto dei campi forniti dal tipo di dati [!DNL Consents & Preferences].

## Prerequisiti {#prerequisites}

Questo documento richiede una buona conoscenza di XDM e l&#39;utilizzo degli schemi in [!DNL Experience Platform]. Prima di continuare, consulta la seguente documentazione:

* [Panoramica del sistema XDM](http://www.adobe.com/go/xdm-home-en)
* [Nozioni di base sulla composizione dello schema](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Struttura del tipo di dati {#structure}

>[!IMPORTANT]
>
>Il tipo di dati [!DNL Consents & Preferences] è progettato per coprire una serie di casi di utilizzo di consenso e gestione delle preferenze. Di conseguenza, questo documento descrive l&#39;uso dei campi del tipo di dati in termini generali e formula solo suggerimenti su come interpretare l&#39;uso di tali campi. Consulta il team legale per la privacy per allineare la struttura del tipo di dati con il modo in cui l&#39;organizzazione interpreta e presenta ai clienti le scelte di consenso e preferenza.

Il tipo di dati [!DNL Consents & Preferences] fornisce diversi campi utilizzati per acquisire le informazioni di **consenso** e **preferenza**.

Un consenso è un&#39;opzione che consente al cliente di specificare come possono essere utilizzati i propri dati. La maggior parte dei consensi hanno un aspetto legale, in quanto alcune giurisdizioni richiedono l&#39;autorizzazione prima che i dati possano essere utilizzati in un modo particolare, o richiedono che il cliente abbia la possibilità di interrompere tale uso (rinuncia) se non è richiesto il consenso positivo.

Una preferenza è un&#39;opzione che consente al cliente di specificare in che modo devono essere gestiti i diversi aspetti della propria esperienza con un marchio. Questi rientrano in due categorie:

* **Preferenze** di personalizzazione: Preferenze relative alla modalità in cui il marchio deve personalizzare le esperienze distribuite a un cliente.
* **Preferenze** di marketing: Preferenze relative alla possibilità o meno di contattare un cliente attraverso vari canali.

La schermata seguente mostra come la struttura del tipo di dati è rappresentata nell’interfaccia utente della piattaforma:

![](../images/data-types/consents.png)

>[!TIP]
>
>Per informazioni su come cercare risorse XDM e controllarne la struttura nell&#39;interfaccia utente della piattaforma, consultate la guida [Esplora risorse XDM](../ui/explore.md).

Il seguente JSON mostra un esempio del tipo di dati che il tipo di dati [!DNL Consents & Preferences] può elaborare. Le informazioni sull&#39;uso specifico di ciascuno di questi campi sono fornite nelle sezioni che seguono.

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "adID": {
      "val": "VI"
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "u"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  }
}
```

>[!TIP]
>
>È possibile generare dati JSON di esempio per qualsiasi schema XDM definito in  Experience Platform, al fine di visualizzare in che modo i dati relativi al consenso e alle preferenze dei clienti devono essere mappati. Per ulteriori informazioni, consulta la seguente documentazione:
>
>* [Generazione di dati di esempio nell’interfaccia utente](../ui/sample.md)
>* [Generazione di dati di esempio nell&#39;API](../api/sample-data.md)


## `consents` {#choices}

`consents` contiene diversi campi che descrivono il consenso e le preferenze di un cliente. Tali campi sono descritti in dettaglio nelle sottosezioni seguenti.

```json
"consents": {
  "collect": {
    "val": "y",
  },
  "adID": {
    "val": "VI"
  },
  "share": {
    "val": "y",
  },
  "personalize": {
    "content": {
      "val": "y"
    }
  },
  "marketing": {
    "preferred": "email",
    "any": {
      "val": "u"
    },
    "email": {
      "val": "n",
      "reason": "Too Frequent",
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### `collect`

`collect` rappresenta il consenso del cliente per la raccolta dei dati.

```json
"collect" : {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornita dal cliente per questo caso di utilizzo. Vedere l&#39; [appendice](#choice-values) per i valori e le definizioni accettati. |

### `adID`

`adID` rappresenta il consenso del cliente circa la possibilità di utilizzare un ID pubblicitario (IDFA o GAID) per collegare il cliente tra le app su questo dispositivo.

```json
"adID" : {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornita dal cliente per questo caso di utilizzo. Vedere l&#39; [appendice](#choice-values) per i valori e le definizioni accettati. |

### `share`

`share` rappresenta il consenso del cliente per sapere se i suoi dati possono essere condivisi con (o venduti a) terze parti.

```json
"share" : {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornita dal cliente per questo caso di utilizzo. Vedere l&#39; [appendice](#choice-values) per i valori e le definizioni accettati. |

### `personalize` {#personalize}

`personalize` acquisisce le preferenze dei clienti in merito alle modalità in cui i loro dati possono essere utilizzati per la personalizzazione. I clienti possono scegliere di non partecipare a casi d&#39;uso specifici per la personalizzazione, o rinunciare completamente alla personalizzazione.

>[!IMPORTANT]
>
>`personalize` non copre i casi di utilizzo marketing. Ad esempio, se un cliente rinuncia alla personalizzazione per tutti i canali, non deve smettere di ricevere comunicazioni attraverso tali canali. Piuttosto, i messaggi che ricevono devono essere generici e non basati sul loro profilo.
>
>Nello stesso esempio, se un cliente rinuncia al marketing diretto per tutti i canali (attraverso `marketing`, spiegato nella [sezione successiva](#marketing)), non deve ricevere alcun messaggio, anche se è consentita la personalizzazione.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `content` | Rappresenta le preferenze del cliente per il contenuto personalizzato sul sito Web o l’applicazione. |
| `val` | La preferenza di personalizzazione fornita dal cliente per il caso di utilizzo specificato. Nei casi in cui al cliente non venga richiesto di fornire il consenso, il valore di questo campo deve indicare la base su cui dovrebbe avvenire la personalizzazione. Vedere l&#39; [appendice](#choice-values) per i valori e le definizioni accettati. |

### `marketing` {#marketing}

`marketing` acquisisce le preferenze dei clienti in merito alle finalità di marketing per le quali i loro dati possono essere utilizzati. I clienti possono scegliere di non partecipare a specifici casi di utilizzo del marketing o di non partecipare al marketing diretto.

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
| `preferred` | Indica il canale preferito dal cliente per la ricezione delle comunicazioni. Per i valori accettati, vedere l&#39; [appendice](#preferred-values). |
| `any` | Rappresenta le preferenze del cliente per il marketing diretto nel suo insieme. La preferenza di consenso fornita in questo campo è considerata la preferenza &quot;predefinita&quot; per qualsiasi canale di marketing, a meno che non venga ignorata da altri sottocampi forniti in `marketing`. Se prevedete di utilizzare opzioni di consenso più dettagliate, si consiglia di escludere questo campo.<br><br>Se il valore è impostato su  `n`, tutte le impostazioni di personalizzazione più specifiche devono essere ignorate. Se il valore è impostato su `y`, anche tutte le opzioni di personalizzazione con granulometria più fine devono essere trattate come `y`, a meno che non siano impostate esplicitamente su `n`. Se il valore non è impostato, i valori per ciascuna opzione di personalizzazione devono essere rispettati come specificato. |
| `email` | Indica se il cliente accetta di ricevere messaggi e-mail. |
| `push` | Indica se il cliente consente la ricezione di notifiche push. |
| `sms` | Indica se il cliente accetta di ricevere messaggi di testo. |
| `val` | La preferenza fornita dal cliente per il caso di utilizzo specificato. Nei casi in cui il cliente non debba essere invitato a fornire il consenso, il valore di questo campo deve indicare la base su cui dovrebbe avvenire il caso di utilizzo del marketing. Vedere l&#39; [appendice](#choice-values) per i valori e le definizioni accettati. |
| `time` | Una marca temporale ISO 8601 di quando la preferenza di marketing è cambiata, se applicabile. Tenere presente che se la marca temporale di una preferenza singola è la stessa fornita in `metadata`, il campo non deve essere impostato per tale preferenza. |
| `reason` | Quando un cliente rinuncia a un caso di utilizzo marketing, questo campo stringa rappresenta il motivo per cui il cliente ha rinunciato. |

### `metadata`

`metadata` acquisisce i metadati generali relativi al consenso e alle preferenze del cliente ogni volta che sono stati aggiornati per l&#39;ultima volta.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Proprietà | Descrizione |
| --- | --- |
| `time` | Una marca temporale ISO 8601 per l&#39;ultima volta che è stato aggiornato un qualsiasi consenso e preferenze del cliente. Questo campo può essere utilizzato invece di applicare marche temporali alle singole preferenze per ridurre il carico e la complessità. Se si fornisce un valore `time` in una singola preferenza, la marca temporale `metadata` di tale preferenza viene ignorata. |

### `idSpecific`

`idSpecific` può essere utilizzato quando un determinato consenso o preferenza non si applica universalmente a un cliente, ma è limitato a un solo dispositivo o ID. Ad esempio, un cliente può scegliere di non ricevere e-mail a un indirizzo, consentendo al contempo la ricezione di e-mail su un altro.

>[!IMPORTANT]
>
>Le autorizzazioni e le preferenze a livello di canale (ossia quelle fornite sotto `consents` al di fuori di `idSpecific`) si applicano agli ID all’interno di tale canale. Pertanto, tutti i permessi e le preferenze a livello di canale influiscono direttamente sul rispetto delle impostazioni ID o specifiche del dispositivo:
>
>* Se il cliente ha rinunciato a livello di canale, qualsiasi consenso o preferenza equivalente in `idSpecific` viene ignorato.
>* Se il consenso o la preferenza a livello di canale non è impostato, o se il cliente ha acconsentito, il consenso o le preferenze equivalenti in `idSpecific` sono rispettate.


Ogni chiave nell&#39;oggetto `idSpecific` rappresenta uno spazio dei nomi identità specifico riconosciuto da Adobe Experience Platform Identity Service. Sebbene sia possibile definire spazi dei nomi personalizzati per classificare identificatori diversi, si consiglia di utilizzare uno degli spazi dei nomi standard forniti dal servizio identità per ridurre le dimensioni di archiviazione per il profilo cliente in tempo reale. Per ulteriori informazioni sugli spazi dei nomi di identità, vedere la [panoramica dello spazio dei nomi di identità](../../identity-service/namespaces.md) nella documentazione del servizio identità.

Le chiavi di ciascun oggetto namespace rappresentano i valori di identità univoci per i quali il cliente ha impostato le preferenze. Ogni valore di identità può contenere un set completo di autorizzazioni e preferenze, formattate allo stesso modo di `consents`.

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
  }
}
```

## Inserimento di dati con il tipo di dati {#ingest}

Per utilizzare il tipo di dati [!DNL Consents & Preferences] per acquisire i dati di consenso dai clienti, è necessario creare un dataset basato su uno schema che contiene tale tipo di dati.

Per informazioni sull&#39;assegnazione dei tipi di dati ai campi, vedere l&#39;esercitazione sulla [creazione di uno schema nell&#39;interfaccia utente](http://www.adobe.com/go/xdm-schema-editor-tutorial-en). Dopo aver creato uno schema contenente un campo con il tipo di dati [!DNL Consents & Preferences], fare riferimento alla sezione relativa alla creazione di un dataset](../../catalog/datasets/user-guide.md#create)nella guida utente del dataset, seguendo la procedura per creare un dataset con uno schema esistente.[

>[!IMPORTANT]
>
>Se si desidera inviare i dati di consenso a [!DNL Real-time Customer Profile], è necessario creare uno schema abilitato [!DNL Profile] basato sulla classe [!DNL XDM Individual Profile] che contiene il tipo di dati [!DNL Consents & Preferences]. Anche il dataset creato in base a tale schema deve essere abilitato per [!DNL Profile]. Per i passaggi specifici relativi ai requisiti [!DNL Real-time Customer Profile] per gli schemi e i set di dati, fare riferimento alle esercitazioni precedentemente collegate.
>
>Inoltre, per poter aggiornare correttamente i profili dei clienti, devi anche verificare che i criteri di unione siano configurati per assegnare priorità ai set di dati contenenti i dati di consenso e preferenze più recenti. Per ulteriori informazioni, vedere la panoramica relativa alle [policy di unione](../../rtcdp/profile/merge-policies.md).

## Gestione delle modifiche di consenso e preferenza

Quando un cliente modifica il proprio consenso o le proprie preferenze sul sito Web, queste modifiche devono essere raccolte e applicate immediatamente mediante l&#39; [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). Se un cliente rinuncia alla raccolta dei dati, la raccolta deve cessare immediatamente. Se un cliente si oppone alla personalizzazione, non dovrebbe essere presente alcuna personalizzazione nella pagina successiva che visita.

## Appendice {#appendix}

Le sezioni seguenti forniscono informazioni di riferimento aggiuntive relative al tipo di dati [!DNL Consents & Preferences].

### Valori accettati per `val` {#choice-values}

La tabella seguente delinea i valori accettati per `val`:

| Valore | Title | Descrizione |
| --- | --- | --- |
| `y` | Sì | Il cliente ha scelto il consenso o la preferenza. In altre parole, essi **acconsentono** all&#39;uso dei loro dati come indicato dal consenso o dalla preferenza in questione. |
| `n` | No | Il cliente ha rifiutato il consenso o la preferenza. In altre parole, essi **non acconsentono** all&#39;uso dei loro dati come indicato dal consenso o dalla preferenza in questione. |
| `p` | Verifica in sospeso | Il sistema non ha ancora ricevuto un consenso o un valore di preferenza finale. Questo viene utilizzato più spesso come parte di un consenso che richiede una verifica in due fasi. Ad esempio, se un cliente sceglie di ricevere e-mail, il consenso viene impostato su `p` fino a quando non seleziona un collegamento in un&#39;e-mail per verificare che abbia fornito l&#39;indirizzo e-mail corretto, al momento in cui il consenso verrà aggiornato a `y`.<br><br>Se questo consenso o preferenza non utilizza un processo di verifica a due set, la  `p` scelta può essere utilizzata per indicare che il cliente non ha ancora risposto al prompt del consenso. Ad esempio, potete impostare automaticamente il valore su `p` nella prima pagina di un sito Web, prima che il cliente abbia risposto al prompt del consenso. Nelle giurisdizioni che non richiedono un consenso esplicito, l&#39;utente può anche utilizzarlo per indicare che il cliente non ha esplicitamente rinunciato (in altre parole, il consenso è assunto). |
| `u` | Sconosciuto | Le informazioni sul consenso o sulle preferenze del cliente sono sconosciute. |
| `LI` | Interesse legittimo | Il legittimo interesse commerciale a raccogliere ed elaborare tali dati per lo scopo specificato supera il potenziale danno che comporta per l&#39;individuo. |
| `CT` | Contratto | La raccolta di dati per lo scopo specificato è necessaria per adempiere agli obblighi contrattuali con l&#39;individuo. |
| `CP` | Rispetto di un obbligo giuridico | La raccolta di dati per lo scopo specificato è necessaria per soddisfare gli obblighi legali dell&#39;impresa. |
| `VI` | Interesse vitale del singolo | La raccolta di dati per lo scopo specificato è necessaria per proteggere gli interessi vitali dell&#39;individuo. |
| `PI` | Interesse pubblico | La raccolta di dati per lo scopo specificato è necessaria per svolgere un compito di interesse pubblico o nell&#39;esercizio di un&#39;autorità ufficiale. |

### Valori accettati per `preferred` {#preferred-values}

La tabella seguente delinea i valori accettati per `preferred`:

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

### Schema [!DNL Consents & Preferences] completo {#full-schema}

Per visualizzare lo schema completo per il tipo di dati [!DNL Consents & Preferences], fare riferimento alla directory archivio XDM [ufficiale](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
