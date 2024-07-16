---
title: setConsent
description: Utilizzato in ogni pagina per tenere traccia delle preferenze di consenso degli utenti.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 2%

---


# `setConsent`

Il comando `setConsent` indica all&#39;SDK Web se deve inviare dati (consenso), ignorare dati (rinuncia) o utilizzare [`defaultConsent`](configure/defaultconsent.md) (consenso sconosciuto).

L’SDK per web supporta i seguenti standard:

* **[Standard di Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: sono supportati sia gli standard 1.0 che 2.0.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: se utilizzi questo standard, il profilo cliente in tempo reale del visitatore viene aggiornato con le informazioni sul consenso se l&#39;implementazione è configurata correttamente:
   1. Lo schema di profilo individuale XDM contiene il gruppo di campi Consenso [IAB TCF 2.0](/help/xdm/field-groups/profile/iab.md).
   1. Lo schema Experience Event contiene il gruppo di campi Consenso [IAB TCF 2.0](/help/xdm/field-groups/event/iab.md).
   1. Includi le informazioni sul consenso IAB nell&#39;evento [oggetto XDM](sendevent/xdm.md). L’SDK per web non include automaticamente le informazioni sul consenso durante l’invio dei dati dell’evento.

Dopo aver utilizzato questo comando, Web SDK scrive le preferenze dell’utente in un cookie. La prossima volta che l’utente carica il sito web nel browser, l’SDK recupera queste preferenze persistenti per determinare se gli eventi possono essere inviati a Adobe.

L’Adobe consiglia di memorizzare le preferenze della finestra di dialogo di consenso separatamente dal consenso dell’SDK per web. L’SDK per web non offre un modo per recuperare il consenso. Per assicurarsi che le preferenze utente rimangano sincronizzate con l&#39;SDK, è possibile chiamare il comando `setConsent` a ogni caricamento di pagina. L’SDK web effettua una chiamata al server solo quando cambia il consenso.

## Utilizzo di `defaultConsent` insieme a `setConsent` {#using-consent}

L’SDK per web offre due comandi di configurazione del consenso complementari:

* [`defaultConsent`](configure/defaultconsent.md): questo comando ha lo scopo di acquisire le preferenze di consenso dei clienti Adobe utilizzando Web SDK.
* [`setConsent`](setconsent.md): questo comando ha lo scopo di acquisire le preferenze di consenso dei visitatori del tuo sito.

Se utilizzate insieme, queste impostazioni possono portare a risultati diversi di raccolta dati e impostazione dei cookie, a seconda dei valori configurati.

Vedi la tabella seguente per capire quando si verifica la raccolta dei dati e quando vengono impostati i cookie, in base alle impostazioni del consenso.

| defaultConsent | setConsent | La raccolta dei dati avviene | Web SDK imposta i cookie del browser |
|---------|----------|---------|---------|
| `in` | `in` | Sì | Sì |
| `in` | `out` | No | Sì |
| `in` | Non impostato | Sì | Sì |
| `pending` | `in` | Sì | Sì |
| `pending` | `out` | No | Sì |
| `pending` | Non impostato | No | No |
| `out` | `in` | Sì | Sì |
| `out` | `out` | No | Sì |
| `out` | Non impostato | No | No |

I seguenti cookie vengono impostati quando la configurazione del consenso consente:

| Nome | Età massima | Descrizione |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 giorni) | Presente quando [`idMigrationEnabled`](configure/idmigrationenabled.md) è abilitato. È utile per la transizione a Web SDK quando alcune parti del sito utilizzano ancora `visitor.js`. |
| **Cookie demdex** | 15552000 (180 giorni) | Presente se la sincronizzazione ID è abilitata. L’Audience Manager imposta questo cookie per assegnare un ID univoco a un visitatore del sito. Il cookie demdex aiuta Audience Manager a eseguire funzioni di base come l’identificazione dei visitatori, la sincronizzazione degli ID, la segmentazione, la modellazione, il reporting e così via. |
| **kndctr_orgid_cluster** | 1800 (30 minuti) | Memorizza l&#39;area dell&#39;Edge Network che soddisfa le richieste dell&#39;utente corrente. L’area viene utilizzata nel percorso URL in modo che l’Edge Network possa indirizzare la richiesta all’area corretta. Se un utente si connette con un indirizzo IP diverso o in una sessione diversa, la richiesta viene nuovamente indirizzata all’area più vicina. |
| **kndct_orgid_identity** | 34128000 (395 giorni) | Memorizza l’ECID, così come altre informazioni relative all’ECID. |
| **kndctr_orgid_consent** | 15552000 (180 giorni) | Memorizza le preferenze di consenso degli utenti per il sito Web. |
| **s_ecid** | 63115200 (2 anni) | Contiene una copia dell&#39;ID Experience Cloud ([!DNL ECID]) o del MID. Il MID viene memorizzato in una coppia chiave/valore con sintassi `s_ecid=MCMID\|<ECID>`. |

## Impostare il consenso utilizzando l’estensione tag Web SDK

L’impostazione del consenso viene eseguita come azione all’interno di una regola nell’interfaccia dei tag di raccolta dati di Adobe Experience Platform.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Imposta consenso]**.
1. Imposta i campi desiderati a destra, tra cui **[!UICONTROL Standard]** e **[!UICONTROL Consenso generale]**.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

In questa azione puoi includere più oggetti di consenso.

## Impostare il consenso utilizzando la libreria JavaScript dell’SDK per web

Esegui il comando `setConsent` quando chiami l&#39;istanza configurata dell&#39;SDK Web. In questo comando è possibile includere i seguenti oggetti:

* **`consent[]`**: matrice di `consent` oggetti. L’oggetto consenso è formattato in modo diverso a seconda dello standard e della versione scelti. Consulta le schede seguenti per esempi di ciascun oggetto di consenso, a seconda dello standard di consenso.
* **`identityMap`**: oggetto che controlla come viene generato un ECID e a quali ID sono associate le informazioni sul consenso. L&#39;Adobe consiglia di includere questo oggetto quando `setConsent` viene eseguito prima di altri comandi, ad esempio [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: oggetto contenente [sostituzioni della configurazione dello stream di dati](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Oggetto `consent` standard Adobe 2.0

Se utilizzi Adobe Experience Platform, devi includere un gruppo di campi dello schema di privacy nello schema del profilo. Consulta [Governance, privacy e sicurezza in Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) per ulteriori informazioni sullo standard Adobe 2.0. Puoi aggiungere dati all&#39;interno dell&#39;oggetto valore seguente corrispondenti allo schema del campo `consents` del gruppo di campi del profilo [!UICONTROL Consensi e preferenze].

* **`standard`**: lo standard di consenso scelto. Impostare questa proprietà su `"Adobe"` per lo standard Adobe 2.0.
* **`version`**: stringa che rappresenta la versione dello standard di consenso. Impostare questa proprietà su `"2.0"` per lo standard Adobe 2.0.
* **`value`**: oggetto contenente i valori di consenso.
   * **`value.collect.val`**: valore del consenso. Impostare su `"y"` quando gli utenti acconsentono e su `"n"` quando gli utenti rinunciano.
   * **`value.metadata.time`**: la marca temporale dell&#39;ultimo aggiornamento delle impostazioni di consenso da parte degli utenti.

```js
// Set consent using the Adobe 2.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### Oggetto `consent` standard IAB TCF 2.0

Per registrare le preferenze di consenso dell’utente fornite tramite lo standard Interactive Advertising Bureau Europe (IAB) Transparency and Consent Framework (TCF), imposta la stringa di consenso come mostrato di seguito.

Se il consenso è impostato in questo modo, Real-Time Customer Profile viene aggiornato con le informazioni sul consenso. Affinché ciò funzioni, lo schema XDM del profilo deve contenere il gruppo di campi dello schema di privacy del profilo [](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Durante l’invio di eventi, le informazioni sul consenso IAB devono essere aggiunte manualmente all’oggetto XDM dell’evento. L’SDK per web non include automaticamente le informazioni sul consenso negli eventi.

Per inviare le informazioni sul consenso negli eventi, è necessario aggiungere il gruppo di campi Privacy evento esperienza allo schema [!DNL XDM ExperienceEvent] abilitato per [!DNL Profile]. Consulta la sezione sull&#39;aggiornamento dello schema ExperienceEvent](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) nella guida alla preparazione del set di dati per i passaggi su come configurare questo elemento.[

* **`standard`**: lo standard di consenso scelto. Impostare questa proprietà su `"IAB TCF"` per lo standard IAB TCF 2.0.
* **`version`**: stringa che rappresenta la versione dello standard di consenso. Impostare questa proprietà su `"2.0"` per lo standard IAB TCF 2.0.
* **`value`**: stringa contenente il valore del consenso.
* **`gdprApplies`**: valore booleano che determina se il RGPD si applica a questo valore di consenso. Il valore predefinito è `true`.
* **`gdprContainsPersonalData`**: valore booleano che determina se i dati evento associati all&#39;utente contengono dati personali. Il valore predefinito è `false`.

```js
// Set consent using the IAB TCF 2.0 standard
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

>[!TAB Adobe 1.0]

### Oggetto `consent` standard Adobe 1.0

* **`standard`**: lo standard di consenso scelto. Impostare questa proprietà su `"Adobe"` per lo standard Adobe 1.0.
* **`version`**: stringa che rappresenta la versione dello standard di consenso. Impostare questa proprietà su `"1.0"` per lo standard Adobe 1.0.
* **`value.general`**: valore del consenso. Impostare su `"in"` quando gli utenti acconsentono e su `"out"` quando gli utenti rinunciano.

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]

### Invio di più standard in una richiesta {#multiple-standards}

L’SDK per web supporta anche l’invio di più oggetti di consenso in una richiesta, come illustrato nell’esempio seguente.

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "2021-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```


## Persistenza delle preferenze di consenso {#persistence}

Dopo aver comunicato le preferenze utente all&#39;SDK Web utilizzando il comando `setConsent`, l&#39;SDK mantiene le preferenze utente a un cookie. La prossima volta che l’utente carica il sito web nel browser, l’SDK web recupererà e utilizzerà queste preferenze persistenti per determinare se gli eventi possono essere inviati o meno a Adobe.

Per visualizzare la finestra di dialogo di consenso con le preferenze correnti, è necessario memorizzare le preferenze utente in modo indipendente. Non è possibile recuperare le preferenze utente dall’SDK per web. Per assicurarsi che le preferenze utente rimangano sincronizzate con l&#39;SDK, è possibile chiamare il comando `setConsent` a ogni caricamento di pagina. L’SDK web effettua una chiamata al server solo se le preferenze sono cambiate.

## Sincronizzazione delle identità durante la configurazione del consenso {#sync-identities}

Quando il consenso predefinito (impostato tramite il parametro [defaultConsent](configure/defaultconsent.md)) è impostato su `pending` o `out`, l&#39;impostazione `setConsent` potrebbe essere la prima richiesta che viene inviata e stabilisce l&#39;identità. Per questo motivo, potrebbe essere importante sincronizzare le identità alla prima richiesta. È possibile aggiungere la mappa delle identità al comando `setConsent` come nel comando `sendEvent`. Consulta [using identityMap](../identity/overview.md#using-identitymap) per un esempio di come includere la mappa delle identità nel comando.
