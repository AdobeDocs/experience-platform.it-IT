---
title: setConsent
description: Utilizzato in ogni pagina per tenere traccia delle preferenze di consenso degli utenti.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 2%

---


# `setConsent`

Il comando `setConsent` indica al Web SDK se deve inviare dati (consenso), ignorare dati (rinuncia) o utilizzare [`defaultConsent`](configure/defaultconsent.md) (consenso sconosciuto).

Il Web SDK supporta i seguenti standard:

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: sono supportati sia gli standard 1.0 che 2.0.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: se utilizzi questo standard, il profilo cliente in tempo reale del visitatore viene aggiornato con le informazioni sul consenso se l&#39;implementazione è configurata correttamente:
   1. Lo schema di profilo individuale XDM contiene il gruppo di campi Consenso [IAB TCF 2.0](/help/xdm/field-groups/profile/iab.md).
   1. Lo schema Experience Event contiene il gruppo di campi Consenso [IAB TCF 2.0](/help/xdm/field-groups/event/iab.md).
   1. Includi le informazioni sul consenso IAB nell&#39;evento [oggetto XDM](sendevent/xdm.md). Il Web SDK non include automaticamente le informazioni sul consenso durante l’invio dei dati dell’evento.

Quando si utilizza questo comando, il Web SDK scrive le preferenze dell&#39;utente nel cookie [`kndctr_<orgId>_consent`](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk). Questo cookie viene impostato indipendentemente dalle preferenze di consenso del visitatore, perché memorizza le preferenze di consenso del visitatore. La prossima volta che l’utente carica il sito web nel browser, SDK recupera queste preferenze persistenti per determinare se gli eventi possono essere inviati ad Adobe.

Adobe consiglia di memorizzare le preferenze della finestra di dialogo sul consenso separatamente dal consenso per Web SDK. Il Web SDK non offre un modo per recuperare il consenso. Per assicurarsi che le preferenze utente rimangano sincronizzate con SDK, è possibile chiamare il comando `setConsent` a ogni caricamento di pagina. Il Web SDK effettua una chiamata al server solo quando cambia il consenso.

## Considerazioni sulla sincronizzazione delle identità {#identity-considerations}

Il comando `setConsent` utilizza solo `ECID` dalla mappa delle identità, in quanto il comando opera a livello di dispositivo. Altre identità della mappa delle identità non vengono prese in considerazione dal comando `setConsent`.

## Utilizzo di `defaultConsent` insieme a `setConsent` {#using-consent}

Il Web SDK offre due comandi di configurazione del consenso complementari:

* [`defaultConsent`](configure/defaultconsent.md): questo comando imposta automaticamente la preferenza di consenso predefinita del visitatore prima di chiamare `setConsent`.
* `setConsent` (pagina corrente): questo comando imposta esplicitamente la preferenza di consenso del visitatore.

Se utilizzate insieme, queste impostazioni possono portare a risultati diversi di raccolta dati e impostazione cookie, a seconda dei valori configurati:

| `defaultConsent` | `setConsent` | La raccolta dei dati avviene | Web SDK imposta i cookie del browser |
| --- | --- | --- | --- |
| `in` | `in` | Sì | Sì |
| `in` | `out` | No | Sì |
| `in` | Non impostato | Sì | Sì |
| `pending` | `in` | Sì | Sì |
| `pending` | `out` | No | Sì |
| `pending` | Non impostato | No | No |
| `out` | `in` | Sì | Sì |
| `out` | `out` | No | Sì |
| `out` | Non impostato | No | No |

Per un elenco completo dei cookie che è possibile impostare, vedere [Cookie di Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) nella guida Servizi di base.

## Utilizzo del comando `setConsent`

Eseguire il comando `setConsent` quando si chiama l&#39;istanza configurata del Web SDK. In questo comando è possibile includere i seguenti oggetti:

* **`consent[]`**: matrice di `consent` oggetti. L’oggetto consenso è formattato in modo diverso a seconda dello standard e della versione scelti. Consulta le schede seguenti per esempi di ciascun oggetto di consenso, a seconda dello standard di consenso.
* **`identityMap`**: oggetto che controlla come viene generato un ECID e a quali ID sono associate le informazioni sul consenso. Adobe consiglia di includere questo oggetto quando `setConsent` viene eseguito prima di altri comandi, ad esempio [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: oggetto contenente [sostituzioni della configurazione dello stream di dati](configure/edgeconfigoverrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Oggetto `consent` standard Adobe 2.0

Se invii dati a Adobe Experience Platform, includi un gruppo di campi dello schema di privacy nello schema del profilo. Consulta [Governance, privacy e sicurezza in Adobe Experience Platform](/help/landing/governance-privacy-security/overview.md) per ulteriori informazioni sullo standard Adobe 2.0. È possibile aggiungere dati all&#39;interno dell&#39;oggetto valore seguente corrispondenti allo schema del campo `consents` del gruppo di campi profilo [!UICONTROL Consents and Preferences].

* **`standard`**: lo standard di consenso scelto. Imposta questa proprietà su `"Adobe"` per lo standard Adobe 2.0.
* **`version`**: stringa che rappresenta la versione dello standard di consenso. Imposta questa proprietà su `"2.0"` per lo standard Adobe 2.0.
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

Se il consenso è impostato in questo modo, Real-Time Customer Profile viene aggiornato con le informazioni sul consenso. Affinché ciò funzioni, lo schema XDM del profilo deve contenere il gruppo di campi dello schema di privacy del profilo [&#128279;](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Durante l’invio di eventi, le informazioni sul consenso IAB devono essere aggiunte manualmente all’oggetto XDM dell’evento. Il Web SDK non include automaticamente le informazioni sul consenso negli eventi.

Per inviare le informazioni sul consenso negli eventi, è necessario aggiungere il gruppo di campi Privacy evento esperienza allo schema [!DNL Profile] abilitato per [!DNL XDM ExperienceEvent]. Consulta la sezione sull&#39;aggiornamento dello schema ExperienceEvent[&#x200B; nella guida alla preparazione del set di dati per i passaggi su come configurare questo elemento.](/help/landing/governance-privacy-security/consent/iab/dataset.md#event-schema)

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

L’API IAB TCF 2.0 fornisce un evento per quando il consenso viene aggiornato dal cliente. Ciò si verifica quando il cliente imposta inizialmente le sue preferenze e quando aggiorna le sue preferenze. È possibile aggiungere un listener di eventi per eseguire il comando `setConsent`:

```js
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

Il blocco di codice riportato sopra ascolta l&#39;evento `useractioncomplete` e quindi imposta il consenso, passando la stringa di consenso e il flag `gdprApplies`. Se hai identità personalizzate per i clienti, assicurati di compilare la variabile `identityMap`.

>[!TAB Adobe 1.0]

### Oggetto `consent` standard Adobe 1.0

* **`standard`**: lo standard di consenso scelto. Imposta questa proprietà su `"Adobe"` per lo standard Adobe 1.0.
* **`version`**: stringa che rappresenta la versione dello standard di consenso. Imposta questa proprietà su `"1.0"` per lo standard Adobe 1.0.
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

Il Web SDK supporta anche l’invio di più oggetti di consenso in una richiesta, come illustrato nell’esempio seguente.

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
                time: "YYYY-03-17T15:48:42-07:00"
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

Dopo aver comunicato le preferenze utente al Web SDK utilizzando il comando `setConsent`, SDK mantiene le preferenze utente a un cookie. Al successivo caricamento del sito web nel browser, il Web SDK recupera e utilizza queste preferenze persistenti per determinare se gli eventi possono essere inviati o meno ad Adobe.

Memorizza le preferenze dell’utente in modo indipendente in modo da poter visualizzare la finestra di dialogo del consenso con le preferenze correnti. Non è possibile recuperare le preferenze utente dal Web SDK. Per assicurarsi che le preferenze utente rimangano sincronizzate con SDK, è possibile chiamare il comando `setConsent` a ogni caricamento di pagina. Il Web SDK effettua una chiamata al server solo se le preferenze cambiano.

## Impostare il consenso utilizzando l’estensione tag Web SDK

L&#39;estensione tag Web SDK equivalente a questo comando è l&#39;azione [**[!UICONTROL Set consent]**](/help/tags/extensions/client/web-sdk/actions/set-consent.md).
