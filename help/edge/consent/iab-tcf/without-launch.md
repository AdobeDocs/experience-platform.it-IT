---
title: Integrare il supporto per IAB TCF 2.0 con Adobe Experience Platform Web SDK
description: Scoprite come configurare il supporto per IAB TCF 2.0 per il sito Web senza utilizzare  Adobe Experience Platform Launch.
seo-description: Scoprite come impostare il consenso IAB TCF 2.0 con Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---


# Integrare il supporto per IAB TCF 2.0 con l&#39;SDK Web della piattaforma

Questa guida mostra come integrare il Interactive Advertising Bureau Transparency &amp; Consent Framework, versione 2.0 (IAB TCF 2.0) con Adobe Experience Platform Web SDK senza utilizzare il Experience Platform Launch. Per una panoramica dell&#39;integrazione con IAB TCF 2.0, leggere la [panoramica](./overview.md). Per una guida sull&#39;integrazione con il Experience Platform Launch, leggere la guida [IAB TCF 2.0 per Experience Platform Launch](./with-launch.md).

## Introduzione

Questa guida utilizza l&#39;interfaccia `__tcfapi` per accedere alle informazioni di consenso. Potrebbe essere più semplice per l’integrazione diretta con il vostro provider di gestione cloud (CMP). Tuttavia, le informazioni contenute in questa guida potrebbero essere comunque utili perché i CMP forniscono in genere funzionalità simili alle API TCF.

>[!NOTE]
>
>Questi esempi presuppongono che, al momento dell&#39;esecuzione del codice, `window.__tcfapi` sia definito sulla pagina. I CMP possono fornire un gancio in cui eseguire queste funzioni quando l&#39;oggetto `__tcfapi` è pronto.

Per utilizzare IAB TCF 2.0 con Experience Platform Launch e estensione AEP Web SDK, è necessario disporre di uno schema XDM. Se non avete impostato nessuno dei due, iniziate a visualizzare la pagina prima di continuare.

Inoltre, questa guida richiede una buona conoscenza di Adobe Experience Platform Web SDK. Per un aggiornamento rapido, leggete la [Adobe Experience Platform Web SDK overview](../../home.md) e la [Domande frequenti](../../web-sdk-faq.md) documentazione.

## Abilitazione del consenso predefinito

Se desiderate trattare tutti gli utenti sconosciuti allo stesso modo, potete impostare il consenso predefinito su `pending`. Questo mette in coda Eventi esperienza fino alla ricezione delle preferenze di consenso.

Per ulteriori informazioni sul consenso predefinito, fare riferimento alla sezione [consenso predefinito](../../fundamentals/configuring-the-sdk.md#default-consent) nella documentazione di configurazione dell&#39;SDK Web per la piattaforma.

### Impostazione del consenso predefinito in base a `gdprApplies`

Alcuni CMP consentono di determinare se il Regolamento generale sulla protezione dei dati (General Data Protection Regulation, GDPR) si applica al cliente. Se desiderate dare il consenso ai clienti per i quali il GDPR non si applica, potete utilizzare il flag `gdprApplies` nella chiamata TCF API.

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

In questo esempio, il comando `configure` viene chiamato dopo che `tcData` è stato ottenuto dall&#39;API TCF. Se `gdprApplies` è true, il consenso predefinito è impostato su `pending`. Se `gdprApplies` è false, il consenso predefinito è impostato su `in`. Assicurarsi di compilare la variabile `alloyConfiguration` con la configurazione.

>[!NOTE]
>
>Se il consenso predefinito è impostato su `in`, il comando `setConsent` può essere comunque utilizzato per registrare le preferenze di consenso dei clienti.

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

Questo blocco di codice ascolta l&#39;evento `useractioncomplete`, quindi imposta il consenso, passando la stringa di consenso e il flag `gdprApplies`. Se disponete di identità personalizzate per i vostri clienti, accertatevi di compilare la variabile `identityMap`. Fare riferimento alla guida relativa al [consenso di supporto](../../consent/supporting-consent.md) per ulteriori informazioni sulle chiamate `setConsent`.

## Inclusione delle informazioni sul consenso in sendEvent

All&#39;interno degli schemi XDM, potete memorizzare le informazioni sulle preferenze di consenso da Eventi esperienza. Esistono due modi per aggiungere queste informazioni a ogni evento.

Innanzitutto, è possibile fornire lo schema XDM pertinente su ogni chiamata `sendEvent`. L&#39;esempio seguente mostra un modo per eseguire questa operazione:

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

Questo esempio ottiene le informazioni di consenso per l&#39;API TCF, quindi invia un evento con le informazioni di consenso aggiunte allo schema XDM. Vedere la guida [eventi di tracciamento](../../fundamentals/tracking-events.md) per comprendere cosa deve essere presente nelle opzioni del comando `sendEvent`.

L&#39;altro modo per aggiungere le informazioni sul consenso a ogni richiesta è con il callback `onBeforeEventSend`. Leggi la sezione sulla [modifica degli eventi globalmente](../../fundamentals/tracking-events.md#modifying-events-globally) nella documentazione degli eventi di tracciamento per ulteriori informazioni su come eseguire questa operazione.

## Passaggi successivi

Ora che hai imparato a utilizzare IAB TCF 2.0 con l&#39;estensione AEP Web SDK, puoi anche scegliere di integrarsi con altre soluzioni  Adobe come  Adobe Analytics o la piattaforma Real-time Customer Data. Per ulteriori informazioni, vedere la [panoramica su IAB Transparency &amp; Consent Framework 2.0](./overview.md).
