---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;consenso;consenso;preferenze;preferenze;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consenso;consenso
title: Tipo di dati consenso e preferenze
description: Il tipo di dati Consent for Privacy, Personalization and Marketing Preferences (Consenso per privacy, personalizzazione e preferenze di marketing) ha lo scopo di supportare la raccolta di autorizzazioni e preferenze dei clienti generate dalle piattaforme di gestione dei consensi (CMP, Consent Management Platform) e da altre sorgenti dalle operazioni sui dati.
topic-legacy: guide
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: 65ad76bb4a5318b03d79d68d3c7e030d7878cf30
workflow-type: tm+mt
source-wordcount: '2058'
ht-degree: 2%

---

# [!UICONTROL Consensi e preferenze] tipo di dati

La [!UICONTROL Consenso per privacy, personalizzazione e preferenze di marketing] tipo di dati (in seguito denominato &quot;[!UICONTROL Consensi e preferenze] &quot;) è un [!DNL Experience Data Model] (XDM) tipo di dati destinato a supportare la raccolta di autorizzazioni e preferenze del cliente generate dalle piattaforme di gestione dei consensi (CMP, Consent Management Platforms) e da altre sorgenti dalle operazioni sui dati.

Il presente documento riguarda la struttura e l&#39;uso previsto dei campi forniti dalla [!UICONTROL Consensi e preferenze] tipo di dati.

## Prerequisiti {#prerequisites}

Questo documento richiede una comprensione funzionante di XDM e l&#39;utilizzo degli schemi in [!DNL Experience Platform]. Prima di continuare, controlla la seguente documentazione:

* [Panoramica del sistema XDM](https://www.adobe.com/go/xdm-home-en)
* [Nozioni di base sulla composizione dello schema](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Struttura del tipo di dati {#structure}

>[!IMPORTANT]
>
>La [!UICONTROL Consensi e preferenze] il tipo di dati è progettato per coprire una serie di casi d’uso di gestione del consenso e delle preferenze. Di conseguenza, in questo documento viene descritto l&#39;utilizzo dei campi del tipo di dati in termini generali e vengono forniti solo suggerimenti su come interpretare l&#39;utilizzo di tali campi. Consulta il team legale per la privacy per allineare la struttura del tipo di dati con il modo in cui l’organizzazione interpreta e presenta ai clienti queste scelte di consenso e preferenza.

La [!UICONTROL Consensi e preferenze] Il tipo di dati fornisce diversi campi utilizzati per l’acquisizione **consenso** e **preferenza** informazioni.

Un consenso è un’opzione che consente al cliente di specificare come utilizzare i propri dati. La maggior parte dei consensi ha un aspetto legale, in quanto alcune giurisdizioni richiedono l’ottenimento di un’autorizzazione prima che i dati possano essere utilizzati in un modo particolare, o richiedono che il cliente abbia la possibilità di interrompere tale uso (rinuncia) se non è richiesto il consenso positivo.

Una preferenza è un’opzione che consente al cliente di specificare come devono essere gestiti i diversi aspetti della propria esperienza con un marchio. Questi rientrano in due categorie:

* **Preferenze di personalizzazione**: Preferenze relative al modo in cui il marchio deve personalizzare le esperienze consegnate a un cliente.
* **Preferenze di marketing**: Preferenze relative all’autorizzazione o meno di un marchio a contattare un cliente attraverso vari canali.

La schermata seguente mostra come la struttura del tipo di dati è rappresentata nell’interfaccia utente di Platform:

![](../images/data-types/consents.png)

>[!TIP]
>
>Consulta la guida su [esplorazione delle risorse XDM](../ui/explore.md) per informazioni su come cercare una risorsa XDM ed esaminarne la struttura nell’interfaccia utente di Platform.

Il seguente JSON mostra un esempio del tipo di dati che [!UICONTROL Consensi e preferenze] tipo di dati può essere elaborato. Le informazioni sull&#39;uso specifico di ciascuno di questi campi sono fornite nelle sezioni seguenti.

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
>Puoi generare dati JSON di esempio per qualsiasi schema XDM definito in Experience Platform, in modo da visualizzare in che modo i dati di consenso e preferenza dei clienti devono essere mappati. Per ulteriori informazioni, consulta la seguente documentazione:
>
>* [Generare dati di esempio nell’interfaccia utente](../ui/sample.md)
>* [Generare dati di esempio nell’API](../api/sample-data.md)


## `consents` {#choices}

`consents` contiene diversi campi che descrivono il consenso e le preferenze di un cliente. Questi campi sono descritti in dettaglio nelle sottosezioni seguenti.

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

`collect` rappresenta il consenso del cliente alla raccolta dei dati.

```json
"collect": {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornito dal cliente per questo caso d’uso. Consulta la sezione [appendice](#choice-values) per i valori e le definizioni accettati. |

{style=&quot;table-layout:auto&quot;}

### `adID`

`adID` rappresenta il consenso del cliente riguardo alla possibilità di utilizzare un ID inserzionista per collegare il cliente tra app su questo dispositivo.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `idType` | Il tipo di ID annuncio, `IDFA` per Apple ID per inserzionisti o `GAID` per Google Advertiser ID, noto anche come Android Advertiser ID (AAID). |
| `val` | La scelta del consenso fornito dal cliente per questo caso d’uso. Consulta la sezione [appendice](#choice-values) per i valori e le definizioni accettati. |

{style=&quot;table-layout:auto&quot;}

### `share`

`share` rappresenta il consenso del cliente per sapere se i suoi dati possono essere condivisi con (o venduti a) seconde o terze parti.

```json
"share": {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornito dal cliente per questo caso d’uso. Consulta la sezione [appendice](#choice-values) per i valori e le definizioni accettati. |

{style=&quot;table-layout:auto&quot;}

### `personalize` {#personalize}

`personalize` acquisisce le preferenze del cliente riguardo a quali modi i loro dati possono essere utilizzati per la personalizzazione. I clienti possono rinunciare a casi d’uso di personalizzazione specifici o rinunciare completamente alla personalizzazione.

>[!IMPORTANT]
>
>`personalize` non copre i casi d’uso di marketing. Ad esempio, se un cliente rinuncia alla personalizzazione per tutti i canali, non deve smettere di ricevere comunicazioni attraverso tali canali. Piuttosto, i messaggi che ricevono devono essere generici e non basati sul loro profilo.
>
>Nello stesso esempio, se un cliente rinuncia al marketing diretto per tutti i canali (tramite `marketing`, spiegata nel [sezione successiva](#marketing)), il cliente non deve ricevere alcun messaggio, anche se è consentita la personalizzazione.

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
| `val` | Preferenza di personalizzazione fornita dal cliente per il caso d’uso specificato. Nei casi in cui al cliente non venga richiesto di fornire il consenso, il valore di questo campo deve indicare la base su cui dovrebbe avvenire la personalizzazione. Consulta la sezione [appendice](#choice-values) per i valori e le definizioni accettati. |

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
| `preferred` | Indica il canale preferito dal cliente per la ricezione delle comunicazioni. Consulta la sezione [appendice](#preferred-values) per i valori accettati. |
| `any` | Rappresenta le preferenze del cliente per il marketing diretto nel suo insieme. La preferenza di consenso fornita in questo campo è considerata la preferenza &quot;predefinita&quot; per qualsiasi canale di marketing, a meno che non venga bypassata da altri sottocampi forniti in `marketing`. Se prevedi di utilizzare opzioni di consenso più granulari, escludi questo campo.<br><br>Se il valore è impostato su `n`, quindi tutte le impostazioni di personalizzazione più specifiche devono essere ignorate. Se il valore è impostato su `y`, tutte le opzioni di personalizzazione a grana più fine devono essere trattate come `y`, a meno che non sia esplicitamente impostato su `n`. Se il valore non viene impostato, i valori per ogni opzione di personalizzazione devono essere rispettati come specificato. |
| `email` | Indica se il cliente accetta di ricevere messaggi e-mail. |
| `push` | Indica se il cliente consente la ricezione di notifiche push. |
| `sms` | Indica se il cliente accetta di ricevere messaggi di testo. |
| `val` | La preferenza fornita dal cliente per il caso d’uso specificato. Nei casi in cui non sia necessario chiedere al cliente di fornire il consenso, il valore di questo campo deve indicare la base su cui deve avvenire il caso d’uso del marketing. Consulta la sezione [appendice](#choice-values) per i valori e le definizioni accettati. |
| `time` | Una marca temporale ISO 8601 di quando la preferenza di marketing è cambiata, se applicabile. Tieni presente che se la marca temporale per una singola preferenza è la stessa di quella fornita in `metadata`, quindi questo campo non deve essere impostato per quella preferenza. |
| `reason` | Quando un cliente rinuncia a un caso di utilizzo marketing, questo campo stringa rappresenta il motivo per cui il cliente ha rinunciato. |

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
| `time` | Una marca temporale ISO 8601 per l&#39;ultima volta che è stato aggiornato il consenso e le preferenze del cliente. Questo campo può essere utilizzato invece di applicare marche temporali alle singole preferenze per ridurre carico e complessità. Fornire un `time` il valore in una singola preferenza sostituisce `metadata` marca temporale per quella particolare preferenza. |

{style=&quot;table-layout:auto&quot;}

## Acquisizione di dati con il tipo di dati {#ingest}

Per utilizzare il [!UICONTROL Consensi e preferenze] tipo di dati per acquisire i dati di consenso dai clienti, devi creare un set di dati basato su uno schema che contenga tale tipo di dati.

Guarda l’esercitazione su [creazione di uno schema nell’interfaccia utente](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) per i passaggi su come assegnare tipi di dati ai campi. Una volta creato uno schema contenente un campo con [!UICONTROL Consensi e preferenze] tipo di dati, consulta la sezione [creazione di un set di dati](../../catalog/datasets/user-guide.md#create) nella guida utente del set di dati, segui i passaggi necessari per creare un set di dati con uno schema esistente.

>[!IMPORTANT]
>
>Se desideri inviare i dati di consenso a [!DNL Real-time Customer Profile], è necessario creare un [!DNL Profile]schema abilitato basato su [!DNL XDM Individual Profile] la classe che contiene [!UICONTROL Consensi e preferenze] tipo di dati. Anche il set di dati creato in base a tale schema deve essere abilitato per [!DNL Profile]. Per i passaggi specifici relativi a [!DNL Real-time Customer Profile] requisiti per schemi e set di dati.
>
>Inoltre, è necessario assicurarsi che i criteri di unione siano configurati per assegnare priorità ai set di dati contenenti i dati di consenso e preferenza più recenti, in modo che i profili cliente vengano aggiornati correttamente. Vedi la panoramica su [criteri di unione](../../rtcdp/profile/merge-policies.md) per ulteriori informazioni.

## Gestione delle modifiche di consenso e preferenza

Quando un cliente modifica il proprio consenso o le proprie preferenze sul sito web, queste modifiche devono essere raccolte e applicate immediatamente utilizzando il [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). Se un cliente rinuncia alla raccolta di dati, tutte le raccolte di dati devono cessare immediatamente. Se un cliente rinuncia alla personalizzazione, non dovrebbe esserci alcuna personalizzazione nella pagina successiva che visita.

## Appendice {#appendix}

Le sezioni seguenti forniscono informazioni di riferimento aggiuntive riguardanti [!UICONTROL Consensi e preferenze] tipo di dati.

### Valori accettati per `val` {#choice-values}

La tabella seguente illustra i valori accettati per `val`:

| Valore | Title | Descrizione |
| --- | --- | --- |
| `y` | Sì (opt-in) | Il cliente ha acconsentito o preferenza. In altre parole, **fare** il consenso all&#39;uso dei loro dati come indicato dal consenso o dalla preferenza in questione. |
| `n` | No (rinuncia) | Il cliente ha rinunciato al consenso o alla preferenza. In altre parole, **non** il consenso all&#39;uso dei loro dati come indicato dal consenso o dalla preferenza in questione. |
| `p` | Verifica in sospeso | Il sistema non ha ancora ricevuto un consenso o un valore di preferenza finale. Viene utilizzato più spesso come parte di un consenso che richiede una verifica in due fasi. Ad esempio, se un cliente sceglie di ricevere e-mail, il consenso viene impostato su `p` fino a quando non selezionano un collegamento in un’e-mail per verificare di aver fornito l’indirizzo e-mail corretto, al momento in cui il consenso viene aggiornato a `y`.<br><br>Se questo consenso o preferenza non utilizza un processo di verifica a due set, il `p` La scelta può essere invece utilizzata per indicare che il cliente non ha ancora risposto al prompt del consenso. Ad esempio, puoi impostare automaticamente il valore su `p` nella prima pagina di un sito web, prima che il cliente risponda al prompt del consenso. Nelle giurisdizioni che non richiedono un consenso esplicito, puoi anche utilizzarlo per indicare che il cliente non ha esplicitamente rinunciato (in altre parole, si presume che il consenso sia). |
| `u` | Sconosciuto | Le informazioni sul consenso o sulle preferenze del cliente sono sconosciute. |
| `dy` | Impostazione predefinita di Sì (opt-in) | Il cliente non ha fornito direttamente il valore del consenso e viene trattato come un consenso (&quot;Sì&quot;) per impostazione predefinita. In altre parole, si presume il consenso finché il cliente non indica il contrario.<br><br>Tieni presente che se le leggi o le modifiche all’informativa sulla privacy della tua azienda determinano modifiche alle impostazioni predefinite di alcuni o tutti gli utenti, devi aggiornare manualmente tutti i profili contenenti valori predefiniti. |
| `dn` | Predefinito di No (rinuncia) | Il cliente non ha fornito direttamente il valore del consenso e viene trattato come una rinuncia (&quot;No&quot;) per impostazione predefinita. In altre parole, si presume che il cliente abbia negato il consenso fino a quando non ha indicato diversamente.<br><br>Tieni presente che se le leggi o le modifiche all’informativa sulla privacy della tua azienda determinano modifiche alle impostazioni predefinite di alcuni o tutti gli utenti, devi aggiornare manualmente tutti i profili contenenti valori predefiniti. |
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

### Completo [!UICONTROL Consensi e preferenze] schema {#full-schema}

Per visualizzare lo schema completo per [!UICONTROL Consensi e preferenze] tipo di dati, consulta [archivio XDM ufficiale](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
