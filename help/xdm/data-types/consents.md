---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;consenso;consenso;preferenze;preferenze;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consenso;consenso
title: Tipo di dati consenso e preferenze
description: Il tipo di dati Consent for Privacy, Personalization and Marketing Preferences (Consenso per privacy, personalizzazione e preferenze di marketing) ha lo scopo di supportare la raccolta di autorizzazioni e preferenze dei clienti generate dalle piattaforme di gestione dei consensi (CMP, Consent Management Platform) e da altre sorgenti dalle operazioni sui dati.
topic: guida
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
translation-type: tm+mt
source-git-commit: 4e9395b4551842cf75b0d1a4ec36c85930c42da5
workflow-type: tm+mt
source-wordcount: '1838'
ht-degree: 1%

---

# [!DNL Consents & Preferences] tipo di dati

Il tipo di dati [!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] (in seguito denominato &quot;tipo di dati &quot;[!DNL Consents & Preferences]&quot;) è un tipo di dati [!DNL Experience Data Model] (XDM) destinato a supportare la raccolta di autorizzazioni e preferenze del cliente generate dalle piattaforme di gestione del consenso (CMP) e da altre fonti delle operazioni sui dati.

Il presente documento illustra la struttura e l&#39;uso previsto dei campi forniti dal tipo di dati [!DNL Consents & Preferences].

## Prerequisiti {#prerequisites}

Questo documento richiede una comprensione funzionante di XDM e l&#39;utilizzo degli schemi in [!DNL Experience Platform]. Prima di continuare, controlla la seguente documentazione:

* [Panoramica del sistema XDM](http://www.adobe.com/go/xdm-home-en)
* [Nozioni di base sulla composizione dello schema](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Struttura del tipo di dati {#structure}

>[!IMPORTANT]
>
>Il tipo di dati [!DNL Consents & Preferences] è progettato per coprire una serie di casi d’uso relativi al consenso e alla gestione delle preferenze. Di conseguenza, in questo documento viene descritto l&#39;utilizzo dei campi del tipo di dati in termini generali e vengono forniti solo suggerimenti su come interpretare l&#39;utilizzo di tali campi. Consulta il team legale per la privacy per allineare la struttura del tipo di dati con il modo in cui l’organizzazione interpreta e presenta ai clienti queste scelte di consenso e preferenza.

Il tipo di dati [!DNL Consents & Preferences] fornisce diversi campi utilizzati per acquisire le informazioni di **consenso** e **preferenza**.

Un consenso è un’opzione che consente al cliente di specificare come utilizzare i propri dati. La maggior parte dei consensi ha un aspetto legale, in quanto alcune giurisdizioni richiedono l’ottenimento di un’autorizzazione prima che i dati possano essere utilizzati in un modo particolare, o richiedono che il cliente abbia la possibilità di interrompere tale uso (rinuncia) se non è richiesto il consenso positivo.

Una preferenza è un’opzione che consente al cliente di specificare come devono essere gestiti i diversi aspetti della propria esperienza con un marchio. Questi rientrano in due categorie:

* **Preferenze** di personalizzazione: Preferenze relative al modo in cui il marchio deve personalizzare le esperienze consegnate a un cliente.
* **Preferenze** di marketing: Preferenze relative all’autorizzazione o meno di un marchio a contattare un cliente attraverso vari canali.

La schermata seguente mostra come la struttura del tipo di dati è rappresentata nell’interfaccia utente di Platform:

![](../images/data-types/consents.png)

>[!TIP]
>
>Consulta la guida [esplorazione delle risorse XDM](../ui/explore.md) in per i passaggi su come cercare una risorsa XDM ed esaminarne la struttura nell’interfaccia utente di Platform.

Il seguente JSON mostra un esempio del tipo di dati che il tipo di dati [!DNL Consents & Preferences] può elaborare. Le informazioni sull&#39;uso specifico di ciascuno di questi campi sono fornite nelle sezioni seguenti.

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

`collect` rappresenta il consenso del cliente alla raccolta dei dati.

```json
"collect" : {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornito dal cliente per questo caso d’uso. Per i valori e le definizioni accettati, consultare l&#39; [appendice](#choice-values) . |

### `adID`

`adID` rappresenta il consenso del cliente circa la possibilità di utilizzare un ID inserzionista (IDFA o GAID) per collegare il cliente tra app su questo dispositivo.

```json
"adID" : {
  "val": "y"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `val` | La scelta del consenso fornito dal cliente per questo caso d’uso. Per i valori e le definizioni accettati, consultare l&#39; [appendice](#choice-values) . |

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

### `personalize` {#personalize}

`personalize` acquisisce le preferenze del cliente riguardo a quali modi i loro dati possono essere utilizzati per la personalizzazione. I clienti possono rinunciare a casi d’uso di personalizzazione specifici o rinunciare completamente alla personalizzazione.

>[!IMPORTANT]
>
>`personalize` non copre i casi d’uso di marketing. Ad esempio, se un cliente rinuncia alla personalizzazione per tutti i canali, non deve smettere di ricevere comunicazioni attraverso tali canali. Piuttosto, i messaggi che ricevono devono essere generici e non basati sul loro profilo.
>
>Nello stesso esempio, se un cliente rinuncia al marketing diretto per tutti i canali (tramite `marketing`, spiegato nella [sezione successiva](#marketing)), non deve ricevere alcun messaggio, anche se è consentita la personalizzazione.

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
| `email` | Indica se il cliente accetta di ricevere messaggi e-mail. |
| `push` | Indica se il cliente consente la ricezione di notifiche push. |
| `sms` | Indica se il cliente accetta di ricevere messaggi di testo. |
| `val` | La preferenza fornita dal cliente per il caso d’uso specificato. Nei casi in cui non sia necessario chiedere al cliente di fornire il consenso, il valore di questo campo deve indicare la base su cui deve avvenire il caso d’uso del marketing. Per i valori e le definizioni accettati, consultare l&#39; [appendice](#choice-values) . |
| `time` | Una marca temporale ISO 8601 di quando la preferenza di marketing è cambiata, se applicabile. Tieni presente che se la marca temporale per una singola preferenza è la stessa di quella fornita in `metadata`, questo campo non deve essere impostato per tale preferenza. |
| `reason` | Quando un cliente rinuncia a un caso di utilizzo marketing, questo campo stringa rappresenta il motivo per cui il cliente ha rinunciato. |

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

## Acquisizione di dati con il tipo di dati {#ingest}

Per utilizzare il tipo di dati [!DNL Consents & Preferences] per acquisire i dati di consenso dai clienti, è necessario creare un set di dati basato su uno schema contenente tale tipo di dati.

Per istruzioni su come assegnare tipi di dati ai campi, consulta l’esercitazione su [creazione di uno schema nell’interfaccia utente](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) . Dopo aver creato uno schema contenente un campo con il tipo di dati [!DNL Consents & Preferences], consulta la sezione relativa alla [creazione di un set di dati](../../catalog/datasets/user-guide.md#create) nella guida utente del set di dati, seguendo i passaggi necessari per creare un set di dati con uno schema esistente.

>[!IMPORTANT]
>
>Se desideri inviare i dati di consenso a [!DNL Real-time Customer Profile], è necessario creare uno schema abilitato [!DNL Profile] in base alla classe [!DNL XDM Individual Profile] che contiene il tipo di dati [!DNL Consents & Preferences]. Anche il set di dati creato in base a tale schema deve essere abilitato per [!DNL Profile]. Fai riferimento alle esercitazioni collegate sopra per passaggi specifici relativi ai requisiti [!DNL Real-time Customer Profile] per schemi e set di dati.
>
>Inoltre, è necessario assicurarsi che i criteri di unione siano configurati per assegnare priorità ai set di dati contenenti i dati di consenso e preferenza più recenti, in modo che i profili cliente vengano aggiornati correttamente. Per ulteriori informazioni, consulta la panoramica sui [criteri di unione](../../rtcdp/profile/merge-policies.md) .

## Gestione delle modifiche di consenso e preferenza

Quando un cliente modifica i propri consensi o preferenze sul sito web, queste modifiche devono essere raccolte e applicate immediatamente utilizzando l&#39; [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). Se un cliente rinuncia alla raccolta di dati, tutte le raccolte di dati devono cessare immediatamente. Se un cliente rinuncia alla personalizzazione, non dovrebbe esserci alcuna personalizzazione nella pagina successiva che visita.

## Appendice {#appendix}

Le sezioni seguenti forniscono informazioni di riferimento aggiuntive relative al tipo di dati [!DNL Consents & Preferences].

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

### Schema completo [!DNL Consents & Preferences] {#full-schema}

Per visualizzare lo schema completo del tipo di dati [!DNL Consents & Preferences], fai riferimento al [repository XDM ufficiale](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
