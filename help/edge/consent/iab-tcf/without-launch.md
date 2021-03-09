---
title: Integrare il supporto IAB TCF 2.0 utilizzando l’SDK web Adobe Experience Platform
description: Scopri come configurare il supporto IAB TCF 2.0 per il tuo sito web senza utilizzare Adobe Experience Platform Launch.
seo-description: Scopri come configurare il consenso IAB TCF 2.0 con Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Integrare il supporto IAB TCF 2.0 con Platform Web SDK

Questa guida mostra come integrare il framework per la trasparenza e il consenso di Interactive Advertising Bureau, versione 2.0 (IAB TCF 2.0) con l’SDK Web di Adobe Experience Platform senza utilizzare il Experience Platform Launch. Per una panoramica dell’integrazione con IAB TCF 2.0, consulta la sezione [panoramica](./overview.md). Per una guida su come integrare con il Experience Platform Launch, leggi la guida [IAB TCF 2.0 per Experience Platform Launch](./with-launch.md).

## Introduzione

Questa guida utilizza l’ interfaccia `__tcfapi` per accedere alle informazioni sul consenso. Potrebbe essere più facile integrarsi direttamente con il provider di gestione cloud (CMP). Tuttavia, le informazioni contenute in questa guida potrebbero essere comunque utili perché le CMP forniscono generalmente funzionalità simili all’API TCF.

>[!NOTE]
>
>Questi esempi presuppongono che al momento dell’esecuzione del codice, `window.__tcfapi` sia definito nella pagina. Le CMP possono fornire un hook in cui è possibile eseguire queste funzioni quando l&#39;oggetto `__tcfapi` è pronto.

Per utilizzare IAB TCF 2.0 con l’estensione Experience Platform Launch e Adobe Experience Platform Web SDK, è necessario disporre di uno schema XDM. Se non hai impostato nessuno dei due, inizia visualizzando questa pagina prima di procedere.

Inoltre, questa guida richiede una buona conoscenza di Adobe Experience Platform Web SDK. Per un aggiornamento rapido, consulta la [Panoramica dell’SDK web Adobe Experience Platform](../../home.md) e la documentazione [Domande frequenti](../../web-sdk-faq.md) .

## Abilitazione del consenso predefinito

Se desideri trattare tutti gli utenti sconosciuti allo stesso modo, puoi impostare il consenso predefinito su `pending` o `out`. Questo mette in coda o elimina gli eventi esperienza fino alla ricezione delle preferenze di consenso.

Per ulteriori informazioni sul consenso predefinito, consulta la sezione [consenso predefinito](../../fundamentals/configuring-the-sdk.md#default-consent) nella documentazione di configurazione di Platform Web SDK.

### Impostazione del consenso predefinito in base a `gdprApplies`

Alcune CMP consentono di determinare se il Regolamento generale sulla protezione dei dati (RGPD) si applica al cliente. Se desideri dare il consenso ai clienti in cui non è applicabile il RGPD, puoi utilizzare il flag `gdprApplies` nella chiamata API TCF.

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

In questo esempio, il comando `configure` viene chiamato dopo che `tcData` è stato ottenuto dall&#39;API TCF. Se `gdprApplies` è true, il consenso predefinito è impostato su `pending`. Se `gdprApplies` è false, il consenso predefinito è impostato su `in`. Assicurati di inserire la variabile `alloyConfiguration` con la tua configurazione.

>[!NOTE]
>
>Quando il consenso predefinito è impostato su `in`, il comando `setConsent` può ancora essere utilizzato per registrare le preferenze di consenso dei clienti.

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

Questo blocco di codice ascolta l’evento `useractioncomplete` e quindi imposta il consenso, passando la stringa di consenso e il flag `gdprApplies`. Se disponi di identità personalizzate per i clienti, assicurati di inserire la variabile `identityMap` . Per ulteriori informazioni sulla chiamata a `setConsent`, consulta la guida relativa al [supporto del consenso](../../consent/supporting-consent.md) .

## Inclusione delle informazioni sul consenso in sendEvent

All’interno degli schemi XDM, puoi archiviare le informazioni sulle preferenze di consenso da Experience Events. Esistono due modi per aggiungere queste informazioni a ogni evento.

Innanzitutto, puoi fornire lo schema XDM pertinente su ogni chiamata `sendEvent`. L&#39;esempio seguente mostra un modo per eseguire questa operazione:

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

Questo esempio ottiene le informazioni sul consenso per l’API TCF e quindi invia un evento con le informazioni sul consenso aggiunte allo schema XDM. Per informazioni sulle opzioni di comando `sendEvent`, consulta la guida [eventi di tracciamento](../../fundamentals/tracking-events.md) .

L&#39;altro modo per aggiungere le informazioni sul consenso a ogni richiesta è con il callback `onBeforeEventSend` . Per ulteriori informazioni su come eseguire questa operazione, leggi la sezione su [modificare gli eventi a livello globale](../../fundamentals/tracking-events.md#modifying-events-globally) all&#39;interno della documentazione sugli eventi di tracciamento .

## Passaggi successivi

Ora che hai imparato a utilizzare IAB TCF 2.0 con l’estensione Platform Web SDK, puoi anche scegliere di integrarsi con altre soluzioni di Adobe come Adobe Analytics o Real-time Customer Data Platform. Per ulteriori informazioni, consulta la [panoramica IAB Transparency &amp; Consent Framework 2.0](./overview.md) .
