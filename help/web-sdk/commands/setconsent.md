---
title: setConsent
description: Utilizzato in ogni pagina per tenere traccia del consenso dell’utente.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# setConsent

Il `setConsent` comunica all&#39;SDK Web se deve inviare dati (consenso), ignorare dati (rinuncia) o utilizzare [`defaultConsent`](configure/defaultconsent.md) (consenso sconosciuto).

L’SDK per web supporta i seguenti standard:

* **[Standard Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: sono supportati sia gli standard 1.0 che 2.0.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: se utilizzi questo standard, Real-Time Customer Profile del visitatore viene aggiornato con le informazioni sul consenso se l’implementazione è configurata correttamente:
   1. Lo schema di profilo individuale XDM contiene il [Gruppo di campi Consenso IAB TCF 2.0](/help/xdm/field-groups/profile/iab.md).
   1. Lo schema Experience Event contiene [Gruppo di campi Consenso IAB TCF 2.0](/help/xdm/field-groups/event/iab.md).
   1. Includi le informazioni sul consenso IAB nell’evento [Oggetto XDM](sendevent/xdm.md). L’SDK per web non include automaticamente le informazioni sul consenso durante l’invio dei dati dell’evento.

Dopo aver utilizzato questo comando, Web SDK scrive le preferenze dell’utente in un cookie. La prossima volta che l’utente carica il sito web nel browser, l’SDK recupera queste preferenze persistenti per determinare se gli eventi possono essere inviati a Adobe.

L’Adobe consiglia di memorizzare le preferenze della finestra di dialogo di consenso separatamente dal consenso dell’SDK per web. L’SDK per web non offre un modo per recuperare il consenso. Per fare in modo che le preferenze utente rimangano sincronizzate con l&#39;SDK, puoi chiamare il `setConsent` a ogni caricamento di pagina. L’SDK web effettua una chiamata al server solo quando cambia il consenso.

## Impostare il consenso utilizzando l’estensione tag Web SDK

L’impostazione del consenso viene eseguita come azione all’interno di una regola nell’interfaccia dei tag di raccolta dati di Adobe Experience Platform.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Impostare il consenso]**.
1. Imposta i campi desiderati a destra, tra cui **[!UICONTROL Standard]** e **[!UICONTROL Consenso generale]**.
1. Clic **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

In questa azione puoi includere più oggetti di consenso.

## Impostare il consenso utilizzando la libreria JavaScript dell’SDK web

Esegui il `setConsent` quando si chiama l’istanza configurata dell’SDK per web. In questo comando è possibile includere i seguenti oggetti:

* **`consent[]`**: array di `consent` oggetti. L’oggetto consenso è formattato in modo diverso a seconda dello standard e della versione scelti.
* **`identityMap`**: oggetto che controlla come viene generato un ECID e a quali informazioni sul consenso degli ID è associato. L’Adobe consiglia di includere questo oggetto quando `setConsent` viene eseguito prima di altri comandi, ad esempio [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: oggetto contenente [sostituzioni della configurazione dello stream di dati](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Norma dell’Adobe 2.0 `consent` oggetto

* **`standard`**: lo standard di consenso scelto. Imposta questa proprietà su `"Adobe"` per la norma Adobe 2.0.
* **`version`**: stringa che rappresenta la versione dello standard di consenso. Imposta questa proprietà su `"2.0"` per la norma Adobe 2.0.
* **`value`**: oggetto contenente i valori del consenso.
   * **`value.collect.val`**: valore del consenso. I valori validi sono `"y"` (consenso) e `"n"` (rinuncia).
   * **`value.metadata.time`**: marca temporale con cui l’utente ha impostato il valore del consenso.

```js
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

### IAB TCF 2.0 standard `consent` oggetto

* **`standard`**: lo standard di consenso scelto. Imposta questa proprietà su `"IAB TCF"` per lo standard IAB TCF 2.0.
* **`version`**: stringa che rappresenta la versione dello standard di consenso. Imposta questa proprietà su `"2.0"` per lo standard IAB TCF 2.0.
* **`value`**: stringa contenente il valore del consenso.
* **`gdprApplies`**: valore booleano che determina se il RGPD si applica a questo valore di consenso. Il valore predefinito è `true`.
* **`gdprContainsPersonalData`**: valore booleano che determina se i dati evento associati a questo utente contengono dati personali. Il valore predefinito è `false`.

```js
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

### Norma dell&#39;Adobe 1.0 `consent` oggetto

* **`standard`**: lo standard di consenso scelto. Imposta questa proprietà su `"Adobe"` per la norma Adobe 1.0.
* **`version`**: stringa che rappresenta la versione dello standard di consenso. Imposta questa proprietà su `"1.0"` per la norma Adobe 1.0.
* **`value.general`**: valore del consenso. I valori validi sono `"in"` (consenso) e `"out"` (rinuncia).

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
