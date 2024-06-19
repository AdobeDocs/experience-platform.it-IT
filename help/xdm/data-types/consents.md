---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;consenso;preferenze;Preferenze;privacyOptOuts;marketingPreferences;optOutType;baseDiElaborazione;consenso;consenso;consenso
title: Tipo di dati Consensi e preferenze
description: Il tipo di dati Consenso per la privacy, la personalizzazione e le preferenze di marketing ha lo scopo di supportare la raccolta di autorizzazioni e preferenze del cliente generate dalle piattaforme di gestione del consenso (CMP, Consent Management Platforms) e da altre origini dalle operazioni sui dati.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '2278'
ht-degree: 0%

---

# [!UICONTROL Consensi e preferenze] tipo di dati

Il [!UICONTROL Consenso per le preferenze di privacy, personalizzazione e marketing] tipo di dati (in seguito denominato &quot;tipo di dati&quot;)[!UICONTROL Consensi e preferenze] data type&quot;) è un [!DNL Experience Data Model] (XDM) tipo di dati che ha lo scopo di supportare la raccolta di autorizzazioni e preferenze del cliente generate dalle piattaforme di gestione del consenso (CMP, Consent Management Platforms) e da altre origini dalle operazioni dei tuoi dati.

Il presente documento descrive la struttura e l&#39;uso previsto dei campi forniti dal [!UICONTROL Consensi e preferenze] tipo di dati.

## Prerequisiti {#prerequisites}

Questo documento richiede una buona conoscenza di XDM e dell’utilizzo degli schemi in [!DNL Experience Platform]. Prima di continuare, consulta la seguente documentazione:

* [Panoramica del sistema XDM](https://www.adobe.com/go/xdm-home-en)
* [Nozioni di base sulla composizione dello schema](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Struttura del tipo di dati {#structure}

>[!IMPORTANT]
>
>Il [!UICONTROL Consensi e preferenze] il tipo di dati è progettato per coprire una serie di casi di utilizzo della gestione del consenso e delle preferenze. Di conseguenza, questo documento descrive l’utilizzo dei campi del tipo di dati in termini generali e fornisce solo suggerimenti su come interpretare l’utilizzo di tali campi. Consulta il team legale della tua privacy per allineare la struttura del tipo di dati con il modo in cui la tua organizzazione interpreta e presenta ai clienti queste scelte di consenso e preferenze.

Il [!UICONTROL Consensi e preferenze] Il tipo di dati fornisce diversi campi utilizzati per acquisire **consenso** e **preferenza** informazioni.

Il consenso è un’opzione che consente al cliente di specificare in che modo i suoi dati possono essere utilizzati. La maggior parte dei consensi ha un aspetto legale, in quanto alcune giurisdizioni richiedono di ottenere l&#39;autorizzazione prima che i dati possano essere utilizzati in un modo particolare, o richiedono che il cliente abbia la possibilità di interrompere tale utilizzo (opt-out) se non è richiesto il consenso affermativo.

Una preferenza è un’opzione che consente al cliente di specificare in che modo devono essere gestiti i diversi aspetti della sua esperienza con un marchio. Questi rientrano in due categorie:

* **Preferenze di personalizzazione**: preferenze relative al modo in cui il brand deve personalizzare le esperienze consegnate a un cliente.
* **Preferenze di marketing**: preferenze relative al fatto che a un marchio sia consentito contattare un cliente tramite vari canali.

La schermata seguente mostra come la struttura del tipo di dati è rappresentata nell’interfaccia utente di Platform:

![](../images/data-types/consents.png)

>[!TIP]
>
>Consulta la guida su [esplorazione delle risorse XDM](../ui/explore.md) per i passaggi su come cercare qualsiasi risorsa XDM e ispezionarne la struttura nell’interfaccia utente di Platform.

Il codice JSON seguente mostra un esempio del tipo di dati che [!UICONTROL Consensi e preferenze] tipo di dati può elaborare. Le informazioni sull’uso specifico di ciascuno di questi campi sono fornite nelle sezioni seguenti.

```json
{
  "consents": {
    "collect": {
      "val": "VI",
    },
    "adID": {
      "idType": "IDFA",
      "val": "y"
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
    }
  }
}
```

>[!TIP]
>
>Puoi generare dati JSON di esempio per qualsiasi schema XDM definito in Experience Platform per aiutare a visualizzare in che modo devono essere mappati i dati sul consenso dei clienti e sulle preferenze. Per ulteriori informazioni, consulta la seguente documentazione:
>
>* [Generare dati di esempio nell’interfaccia utente](../ui/sample.md)
>* [Generare dati di esempio nell’API](../api/sample-data.md)

## `consents` {#choices}

`consents` contiene diversi campi che descrivono i consensi e le preferenze di un cliente. Questi campi sono descritti più dettagliatamente nelle sottosezioni seguenti.

```json
"consents": {
  "collect": {
    "val": "VI",
  },
  "adID": {
    "idType": "IDFA",
    "val": "y"
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

`collect` rappresenta il consenso del cliente alla raccolta dei propri dati.

```json
"collect": {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornito dal cliente per questo caso d’uso. Consulta la [appendice](#choice-values) per i valori e le definizioni accettati. |

{style="table-layout:auto"}

### `adID`

`adID` rappresenta il consenso del cliente sulla possibilità di utilizzare un ID inserzionista per collegare il cliente tra le app su questo dispositivo.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `idType` | Il tipo di ID annuncio, `IDFA` per l’ID di Apple per gli inserzionisti o `GAID` per l’ID inserzionista di Google, noto anche come ID inserzionista Android (AAID). |
| `val` | La scelta del consenso fornito dal cliente per questo caso d’uso. Consulta la [appendice](#choice-values) per i valori e le definizioni accettati. |

{style="table-layout:auto"}

### `share`

`share` rappresenta il consenso del cliente alla condivisione (o vendita) dei propri dati con seconde o terze parti.

```json
"share": {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornito dal cliente per questo caso d’uso. Consulta la [appendice](#choice-values) per i valori e le definizioni accettati. |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` acquisisce le preferenze del cliente relative ai modi in cui i suoi dati possono essere utilizzati per la personalizzazione. I clienti possono rinunciare a casi di utilizzo di personalizzazione specifici o rinunciare completamente alla personalizzazione.

>[!IMPORTANT]
>
>`personalize` non copre i casi di utilizzo del marketing. Ad esempio, se un cliente rinuncia alla personalizzazione per tutti i canali, non deve interrompere la ricezione di comunicazioni attraverso tali canali. Piuttosto, i messaggi che ricevono devono essere generici e non basati sul loro profilo.
>
>Nello stesso esempio, se un cliente rinuncia al marketing diretto per tutti i canali (tramite `marketing`, illustrato nella [sezione successiva](#marketing)), il cliente non deve ricevere messaggi, anche se la personalizzazione è consentita.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `content` | Rappresenta le preferenze del cliente per i contenuti personalizzati sul sito web o sull’applicazione. |
| `val` | Preferenza di personalizzazione fornita dal cliente per il caso d’uso specificato. Nei casi in cui al cliente non debba essere richiesto di fornire il consenso, il valore di questo campo deve indicare la base su cui deve aver luogo la personalizzazione. Consulta la [appendice](#choice-values) per i valori e le definizioni accettati. |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` acquisisce le preferenze dei clienti relative alle finalità di marketing per le quali i loro dati possono essere utilizzati. I clienti possono rinunciare a casi di utilizzo di marketing specifici o rinunciare completamente al marketing diretto.

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
| `preferred` | Indica il canale preferito dal cliente per la ricezione delle comunicazioni. Consulta la [appendice](#preferred-values) per i valori accettati. |
| `any` | Rappresenta le preferenze del cliente per il marketing diretto nel suo complesso. La preferenza di consenso fornita in questo campo è considerata la preferenza &quot;predefinita&quot; per qualsiasi canale di marketing, a meno che non sia sostituita da ulteriori sottocampi forniti in `marketing`. Se prevedi di utilizzare opzioni di consenso più granulari, si consiglia di escludere questo campo.<br><br>Se il valore è impostato su `n`, quindi tutte le impostazioni di personalizzazione più specifiche dovrebbero essere ignorate. Se il valore è impostato su `y`, anche tutte le opzioni di personalizzazione a granularità più fine devono essere trattate come `y`, a meno che non sia impostato esplicitamente su `n`. Se il valore non è impostato, i valori per ogni opzione di personalizzazione devono essere rispettati come specificato. |
| `email` | Indica se il cliente accetta di ricevere messaggi e-mail. |
| `push` | Indica se il cliente consente la ricezione di notifiche push. |
| `sms` | Indica se il cliente accetta di ricevere SMS. |
| `val` | Preferenza fornita dal cliente per il caso d’uso specificato. Nei casi in cui al cliente non deve essere richiesto di fornire il consenso, il valore di questo campo dovrebbe indicare la base su cui dovrebbe basarsi il caso di utilizzo di marketing. Consulta la [appendice](#choice-values) per i valori e le definizioni accettati. |
| `time` | Una marca temporale ISO 8601 indicante quando la preferenza di marketing è cambiata, se applicabile. Tieni presente che se la marca temporale per una singola preferenza è la stessa di quella fornita in `metadata`, questo campo non deve essere impostato per tale preferenza. |
| `reason` | Quando un cliente rinuncia a un caso di utilizzo di marketing, questo campo stringa rappresenta il motivo per cui il cliente ha rinunciato. |

{style="table-layout:auto"}

### `metadata`

`metadata` acquisisce metadati generali sui consensi e le preferenze del cliente ogni volta che sono stati aggiornati per l’ultima volta.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Proprietà | Descrizione |
| --- | --- |
| `time` | Una marca temporale ISO 8601 per l’ultimo aggiornamento dei consensi e delle preferenze del cliente. Questo campo può essere utilizzato invece di applicare marche temporali alle singole preferenze per ridurre il carico e la complessità. Fornire un `time` in una singola preferenza sostituisce il `metadata` timestamp per quella particolare preferenza. |

{style="table-layout:auto"}

## Acquisizione di dati tramite il tipo di dati {#ingest}

Per utilizzare il [!UICONTROL Consensi e preferenze] tipo di dati per acquisire i dati sul consenso dei clienti, devi creare un set di dati basato su uno schema che contiene tale tipo di dati.

Guarda il tutorial su [creazione di uno schema nell’interfaccia utente](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) per i passaggi su come assegnare tipi di dati ai campi. Dopo aver creato uno schema contenente un campo con il [!UICONTROL Consensi e preferenze] tipo di dati, consulta la sezione su [creazione di un set di dati](../../catalog/datasets/user-guide.md#create) nella guida utente del set di dati, segui i passaggi per creare un set di dati con uno schema esistente.

>[!IMPORTANT]
>
>Se desideri inviare i dati sul consenso a [!DNL Real-Time Customer Profile], è necessario creare un’ [!DNL Profile]schema abilitato in base al [!DNL XDM Individual Profile] classe che contiene [!UICONTROL Consensi e preferenze] tipo di dati. Il set di dati creato in base a tale schema deve essere abilitato anche per [!DNL Profile]. Fai riferimento ai tutorial collegati in precedenza per i passaggi specifici relativi a [!DNL Real-Time Customer Profile] requisiti per schemi e set di dati.
>
>Inoltre, devi anche assicurarti che i criteri di unione siano configurati per assegnare la priorità ai set di dati che contengono i dati di consenso e preferenze più recenti, al fine di aggiornare correttamente i profili dei clienti. Consulta la panoramica su [criteri di unione](../../rtcdp/profile/merge-policies.md) per ulteriori informazioni.

## Gestione delle modifiche di consenso e preferenze

Quando un cliente modifica i propri consensi o preferenze sul sito web, queste modifiche devono essere raccolte e immediatamente applicate utilizzando [Adobe Experience Platform Web SDK](../../web-sdk/commands/setconsent.md). Se un cliente rinuncia alla raccolta dei dati, tutta la raccolta dei dati deve cessare immediatamente. Se un cliente rinuncia alla personalizzazione, significa che non dovrebbe essere presente alcuna personalizzazione nella pagina successiva in cui visita.

## Appendice {#appendix}

Le sezioni seguenti forniscono informazioni di riferimento aggiuntive relative ai [!UICONTROL Consensi e preferenze] tipo di dati.

### Valori accettati per `val` {#choice-values}

La tabella seguente illustra i valori accettati per `val`:

| Valore | Titolo | Descrizione |
| --- | --- | --- |
| `y` | Sì (consenso) | Il cliente ha acconsentito al consenso o alla preferenza. In altre parole, **fare** acconsentire all’uso dei propri dati come indicato dal consenso o dalla preferenza in questione. |
| `n` | No (rinuncia) | Il cliente ha rinunciato al consenso o alla preferenza. In altre parole, **non** acconsentire all’uso dei propri dati come indicato dal consenso o dalla preferenza in questione. |
| `p` | Verifica in sospeso | Il sistema non ha ancora ricevuto il consenso o il valore della preferenza finale. Questo viene spesso utilizzato come parte di un consenso che richiede una verifica in due fasi. Ad esempio, se un cliente acconsente alla ricezione di e-mail, il consenso viene impostato su `p` fino a quando non seleziona un collegamento in un’e-mail per verificare di aver fornito l’indirizzo e-mail corretto, dopodiché il consenso verrà aggiornato a `y`.<br><br>Se tale consenso o preferenza non utilizza un processo di verifica a due insiemi, il `p` La scelta può invece essere utilizzata per indicare che il cliente non ha ancora risposto al prompt del consenso. Ad esempio, puoi impostare automaticamente il valore su `p` sulla prima pagina di un sito web, prima che il cliente abbia risposto al prompt del consenso. Nelle giurisdizioni che non richiedono il consenso esplicito, è possibile utilizzarlo anche per indicare che il cliente non ha esplicitamente rinunciato (in altre parole, si presume il consenso). |
| `u` | Sconosciuto | Le informazioni sul consenso o sulle preferenze del cliente sono sconosciute. |
| `dy` | Predefinito di Sì (consenso) | Il cliente non ha fornito un valore di consenso e viene trattato come un consenso (&quot;Sì&quot;) per impostazione predefinita. In altre parole, si presume il consenso fino a quando il cliente non indica il contrario.<br><br>Tieni presente che se le leggi o le modifiche all’informativa sulla privacy della tua azienda determinano modifiche alle impostazioni predefinite di alcuni o di tutti gli utenti, devi aggiornare manualmente tutti i profili contenenti i valori predefiniti. |
| `dn` | Predefinito per No (rinuncia) | Il cliente non ha fornito un valore di consenso e per impostazione predefinita viene trattato come una rinuncia (&quot;No&quot;). In altre parole, si presume che il cliente abbia negato il consenso fino a quando non indica diversamente.<br><br>Tieni presente che se le leggi o le modifiche all’informativa sulla privacy della tua azienda determinano modifiche alle impostazioni predefinite di alcuni o di tutti gli utenti, devi aggiornare manualmente tutti i profili contenenti i valori predefiniti. |
| `LI` | Interesse legittimo | Il legittimo interesse commerciale a raccogliere e trattare tali dati per lo scopo specificato supera il potenziale danno che essi comportano per l’individuo. |
| `CT` | Contratto | La raccolta dei dati per lo scopo specificato è necessaria per adempiere agli obblighi contrattuali con la persona. |
| `CP` | Rispetto di un obbligo legale | La raccolta dei dati per lo scopo specificato è necessaria per soddisfare gli obblighi legali dell&#39;impresa. |
| `VI` | Interesse vitale dell&#39;individuo | La raccolta di dati per lo scopo specificato è necessaria per proteggere gli interessi vitali dell&#39;individuo. |
| `PI` | Interesse pubblico | La raccolta di dati per lo scopo specificato è necessaria per svolgere un compito di interesse pubblico o nell&#39;esercizio di pubblici poteri. |

{style="table-layout:auto"}

### Valori accettati per `preferred` {#preferred-values}

La tabella seguente illustra i valori accettati per `preferred`. Il `preferred` i valori indicano il canale preferito dal cliente per ricevere comunicazioni che li informerebbero sulla raccolta di dati, sulle politiche sulla privacy e sulle opzioni di personalizzazione.

| Valore | Descrizione |
| --- | --- |
| `email` | Questa preferenza indica il consenso del cliente a ricevere messaggi tramite e-mail. |
| `push` | Questa preferenza indica il consenso del cliente alla ricezione di notifiche push. Si tratta di messaggi o avvisi inviati direttamente al loro dispositivo, spesso un’app mobile. |
| `inApp` | Questa preferenza indica il consenso del cliente alla ricezione dei messaggi in-app. Questi messaggi vengono inviati all’interno di un’app mobile o web e forniscono informazioni mentre l’utente è attivamente coinvolto con l’app. |
| `sms` | Questa preferenza indica il consenso del cliente alla ricezione di messaggi tramite SMS (Short Message Service). Si tratta di messaggi di testo inviati al cellulare. |
| `phone` | Questa preferenza indica il consenso del cliente a ricevere comunicazioni attraverso interazioni telefoniche. |
| `phyMail` | Questa preferenza indica il consenso del cliente a ricevere il materiale tramite posta fisica. |
| `inVehicle` | Questa preferenza indica il consenso del cliente a ricevere notifiche mentre si trova nel suo veicolo. Questi messaggi possono essere trasmessi attraverso i sistemi di infotainment del veicolo o altri canali di comunicazione a bordo del veicolo. |
| `inHome` | Questa preferenza indica il consenso del cliente alla ricezione dei messaggi mentre si trova a casa. Questi messaggi possono essere inviati tramite dispositivi smart home o altri canali di comunicazione basati su home. |
| `iot` | Questa preferenza indica il consenso del cliente a ricevere messaggi relativi all’Internet of Things (IoT). Questi messaggi possono essere inviati tramite dispositivi e sistemi collegati all&#39;interno del proprio ambiente. |
| `social` | Questa preferenza indica il consenso del cliente a ricevere comunicazioni tramite le piattaforme di social media. |
| `other` | Questa preferenza include i canali che non rientrano nelle categorie standard. Rappresenta canali di comunicazione alternativi o specializzati che possono essere specifici per un particolare business o settore. |
| `none` | Questa preferenza indica che il cliente non dispone di un canale di comunicazione preferito. |
| `unknown` | Questa preferenza indica che il canale di comunicazione preferito dal cliente non è noto o non è stato specificato. Ciò potrebbe verificarsi se il cliente non ha fornito informazioni esplicite sul consenso o sulle preferenze. |

{style="table-layout:auto"}

### Completo [!UICONTROL Consensi e preferenze] schema {#full-schema}

Per visualizzare lo schema completo per [!UICONTROL Consensi e preferenze] tipo di dati, fare riferimento al [archivio XDM ufficiale](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
