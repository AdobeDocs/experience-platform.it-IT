---
title: Utilizzo di IAB TCF 2.0 senza Launch
seo-title: Impostazione del consenso IAB TCF 2.0 con Adobe Experience Platform Web SDK
description: Scopri come impostare il consenso IAB TCF 2.0 con Adobe Experience Platform Web SDK
seo-description: Scopri come impostare il consenso IAB TCF 2.0 con Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 48cebe994b450b0dac5e6f256ab81827a7e8a0d5
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# Utilizzo di IAB TCF 2.0 con l&#39;estensione Adobe Experience Platform Web SDK

Questa guida illustra come integrare il Interactive Advertising Bureau Transparency &amp; Consent Framework, versione 2.0 (IAB TCF 2.0) con l’SDK Web di Adobe Experience Platform senza utilizzare il Experience Platform Launch. Per una panoramica dell&#39;integrazione con IAB TCF 2.0, leggere la [panoramica](./overview.md). Per una guida sull&#39;integrazione con il Experience Platform Launch, leggere la guida [IAB TCF 2.0 per Experience Platform Launch](./with-launch.md).

## Introduzione

Questa guida utilizza l&#39; `__tcfapi` interfaccia per accedere alle informazioni sul consenso. Potrebbe essere più semplice per l’integrazione diretta con il vostro provider di gestione cloud (CMP). Tuttavia, le informazioni contenute in questa guida potrebbero essere comunque utili perché i CMP forniscono in genere funzionalità simili alle API TCF.

>[!NOTE]
>
>Questi esempi presuppongono che, al momento dell&#39;esecuzione del codice, `window.__tcfapi` sia definito sulla pagina. I CMP possono fornire un gancio in cui eseguire queste funzioni quando l&#39; `__tcfapi` oggetto è pronto.

Per utilizzare IAB TCF 2.0 con Experience Platform Launch e estensione AEP Web SDK, è necessario disporre di uno schema XDM. Se non avete impostato nessuno dei due, prima di procedere visualizzate la guida [di avvio rapido JavaScript per](../../getting-started/quick-start-without-launch.md) Adobe Experience Platform Web SDK.

Inoltre, questa guida richiede una buona conoscenza dell’SDK Web per Adobe Experience Platform. Per un aggiornamento rapido, consulta la panoramica [](../../home.md) Adobe Experience Platform Web SDK e la documentazione sulle domande [](../../getting-started/web-sdk-faq.md) frequenti.

## Abilitazione del consenso predefinito

Se desiderate trattare tutti gli utenti sconosciuti allo stesso modo, potete impostare il consenso predefinito su `pending`. Questo mette in coda Eventi esperienza fino alla ricezione delle preferenze di consenso.

Per ulteriori informazioni sul consenso predefinito, consulta la sezione relativa al consenso [predefinito](../../fundamentals/configuring-the-sdk.md#default-consent) nella documentazione di configurazione dell’SDK Web per la piattaforma.

### Impostazione del consenso predefinito in base a `gdprApplies`

Alcuni CMP consentono di determinare se il Regolamento generale sulla protezione dei dati (General Data Protection Regulation, GDPR) si applica al cliente. Se desiderate dare il consenso ai clienti per i quali il GDPR non si applica, potete utilizzare il `gdprApplies` flag nella chiamata API TCF.

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

In questo esempio, il `configure` comando viene chiamato dopo che l&#39;oggetto `tcData` è stato ottenuto dall&#39;API TCF. Se `gdprApplies` è vero, il consenso predefinito è impostato su `pending`. Se `gdprApplies` è false, il consenso predefinito è impostato su `in`. Accertatevi di compilare la `alloyConfiguration` variabile con la configurazione.

>[!NOTE]
>
>Quando il consenso predefinito è impostato su `in`, il `setConsent` comando può essere comunque utilizzato per registrare le preferenze di consenso dei clienti.

## Utilizzo dell&#39;evento setConsent

L&#39;API IAB TCF 2.0 fornisce un evento per il momento in cui il consenso viene aggiornato dal cliente. Ciò si verifica quando il cliente inizialmente imposta le proprie preferenze e quando aggiorna le proprie preferenze.

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

Questo blocco di codice ascolta l’ `useractioncomplete` evento e imposta il consenso, passando la stringa di consenso e il `gdprApplies` flag. Se disponete di identità personalizzate per i vostri clienti, accertatevi di compilare la `identityMap` variabile. Per ulteriori informazioni sulle chiamate, fare riferimento alla guida sul consenso [](../../fundamentals/supporting-consent.md) di supporto `setConsent`.

## Inclusione delle informazioni sul consenso in sendEvent

All&#39;interno degli schemi XDM, potete memorizzare le informazioni sulle preferenze di consenso da Eventi esperienza. Esistono due modi per aggiungere queste informazioni a ogni evento.

Innanzitutto, è possibile fornire lo schema XDM pertinente a ogni `sendEvent` chiamata. L&#39;esempio seguente mostra un modo per eseguire questa operazione:

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

Questo esempio ottiene le informazioni di consenso per l&#39;API TCF, quindi invia un evento con le informazioni di consenso aggiunte allo schema XDM. Consulta la guida agli eventi [di](../../fundamentals/tracking-events.md) tracciamento per comprendere cosa dovrebbero essere le opzioni di `sendEvent` comando.

L&#39;altro modo per aggiungere le informazioni sul consenso a ogni richiesta è con il `onBeforeEventSend` callback. Per ulteriori informazioni su come [modificare gli eventi a livello globale](../../fundamentals/tracking-events.md#modifying-events-globally) , consulta la sezione relativa alla documentazione relativa agli eventi di tracciamento.

## Passaggi successivi

Ora che hai imparato a utilizzare IAB TCF 2.0 con l&#39;estensione Adobe Experience Platform Web SDK, puoi anche scegliere di integrarsi con altre soluzioni  Adobe come  Adobe Analytics o la piattaforma dati cliente in tempo reale. Per ulteriori informazioni, consulta [la panoramica](./overview.md) IAB Transparency &amp; Consent Framework 2.0.
