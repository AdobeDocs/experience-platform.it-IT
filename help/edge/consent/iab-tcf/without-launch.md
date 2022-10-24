---
title: Integrare il supporto IAB TCF 2.0 utilizzando l’SDK web Adobe Experience Platform
description: Scopri come configurare il supporto IAB TCF 2.0 per il tuo sito web senza utilizzare tag.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Integrare il supporto IAB TCF 2.0 con Platform Web SDK

Questa guida mostra come integrare il framework per la trasparenza e il consenso di Interactive Advertising Bureau, versione 2.0 (IAB TCF 2.0) con l’SDK web di Adobe Experience Platform senza l’utilizzo di tag. Per una panoramica dell’integrazione con IAB TCF 2.0, consulta la sezione [panoramica](./overview.md). Per una guida sull’integrazione con i tag, consulta la sezione [Guida IAB TCF 2.0 per i tag](./with-launch.md).

## Introduzione

Questa guida utilizza `__tcfapi` per accedere alle informazioni sul consenso. Potrebbe essere più facile integrarsi direttamente con il provider di gestione cloud (CMP). Tuttavia, le informazioni contenute in questa guida potrebbero essere comunque utili perché le CMP forniscono generalmente funzionalità simili all’API TCF.

>[!NOTE]
>
>Questi esempi presuppongono che al momento dell&#39;esecuzione del codice, `window.__tcfapi` è definito nella pagina . Le CMP possono fornire un gancio dove è possibile eseguire queste funzioni quando `__tcfapi` l&#39;oggetto è pronto.

Per utilizzare IAB TCF 2.0 con tag e l’estensione Adobe Experience Platform Web SDK, è necessario disporre di uno schema XDM. Se non hai impostato nessuno dei due, inizia visualizzando questa pagina prima di procedere.

Inoltre, questa guida richiede una buona conoscenza di Adobe Experience Platform Web SDK. Per un rinfresco rapido, leggere il [Panoramica di Adobe Experience Platform Web SDK](../../home.md) e [Domande frequenti](../../web-sdk-faq.md) documentazione.

## Abilitazione del consenso predefinito

Se desideri trattare tutti gli utenti sconosciuti allo stesso modo, puoi impostare il consenso predefinito su `pending` o `out`. Questo mette in coda o elimina gli eventi esperienza fino alla ricezione delle preferenze di consenso.

Per ulteriori informazioni sul consenso predefinito, consulta la [sezione consenso predefinito](../../fundamentals/configuring-the-sdk.md#default-consent) nella documentazione di configurazione di Platform Web SDK.

### Impostazione del consenso predefinito in base a `gdprApplies`

Alcune CMP consentono di determinare se il Regolamento generale sulla protezione dei dati (RGPD) si applica al cliente. Se desideri dare il consenso ai clienti in cui non si applica il RGPD, puoi utilizzare il `gdprApplies` flag nella chiamata API TCF.

L&#39;esempio seguente mostra un modo per eseguire questa operazione:

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

In questo esempio, la `configure` viene chiamato dopo il `tcData` è ottenuto dall’API TCF. Se `gdprApplies` è true, il consenso predefinito è impostato su `pending`. Se `gdprApplies` è false, il consenso predefinito è impostato su `in`. Assicurati di compilare il `alloyConfiguration` con la configurazione.

>[!NOTE]
>
>Quando il consenso predefinito è impostato su `in`, `setConsent` può ancora essere utilizzato per registrare le preferenze di consenso dei clienti.

## Utilizzo dell&#39;evento setConsent

L’API IAB TCF 2.0 fornisce un evento per quando il cliente aggiorna il consenso. Ciò si verifica quando il cliente inizialmente imposta le proprie preferenze e quando le aggiorna.

L&#39;esempio seguente mostra un modo per eseguire questa operazione:

```javascript
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

Questo blocco di codice ascolta il `useractioncomplete` , quindi imposta il consenso, passando la stringa di consenso e la `gdprApplies` bandiera. Se disponi di identità personalizzate per i clienti, assicurati di compilare il campo `identityMap` variabile. Consulta la guida su [consenso](../../consent/supporting-consent.md) per ulteriori informazioni sulla chiamata `setConsent`.

## Inclusione delle informazioni sul consenso in sendEvent

All’interno degli schemi XDM, puoi archiviare le informazioni sulle preferenze di consenso da Experience Events. Esistono due modi per aggiungere queste informazioni a ogni evento.

Innanzitutto, puoi fornire lo schema XDM pertinente su ogni `sendEvent` chiama. L&#39;esempio seguente mostra un modo per eseguire questa operazione:

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

Questo esempio ottiene le informazioni sul consenso per l’API TCF e quindi invia un evento con le informazioni sul consenso aggiunte allo schema XDM. Consulta la sezione [eventi di tracciamento](../../fundamentals/tracking-events.md) guida per comprendere cosa dovrebbe essere `sendEvent` opzioni di comando.

L’altro modo per aggiungere le informazioni sul consenso a ogni richiesta è con il `onBeforeEventSend` callback. Leggi la sezione su [modifica globale degli eventi](../../fundamentals/tracking-events.md#modifying-events-globally) nella documentazione sugli eventi di tracciamento per ulteriori informazioni su come eseguire questa operazione.

## Passaggi successivi

Ora che hai imparato a utilizzare IAB TCF 2.0 con l’estensione Platform Web SDK, puoi anche scegliere di integrarsi con altre soluzioni di Adobe come Adobe Analytics o Adobe Real-time Customer Data Platform. Consulta la sezione [Panoramica di IAB Transparency and Consent Framework 2.0](./overview.md) per ulteriori informazioni.
