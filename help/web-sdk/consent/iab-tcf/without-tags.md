---
title: Integrare il supporto IAB TCF 2.0 utilizzando Adobe Experience Platform Web SDK
description: Scopri come impostare il supporto IAB TCF 2.0 per il tuo sito web senza utilizzare i tag.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Integrare il supporto IAB TCF 2.0 con Platform Web SDK

Questa guida illustra come integrare Interactive Advertising Bureau Transparency &amp; Consent Framework, versione 2.0 (IAB TCF 2.0) con Adobe Experience Platform Web SDK senza utilizzare i tag. Per una panoramica dell’integrazione con IAB TCF 2.0, leggi [panoramica](./overview.md). Per una guida su come effettuare l’integrazione con i tag, leggi [Guida IAB TCF 2.0 per i tag](./with-tags.md).

## Introduzione

Questa guida utilizza `__tcfapi` interfaccia per accedere alle informazioni sul consenso. Potrebbe essere più semplice eseguire l’integrazione diretta con il provider di gestione cloud (CMP). Tuttavia, le informazioni contenute in questa guida potrebbero essere ancora utili perché le CMP in genere forniscono funzionalità simili all’API TCF.

>[!NOTE]
>
>In questi esempi si presuppone che, al momento dell&#39;esecuzione del codice, `window.__tcfapi` è definito nella pagina. Le CMP possono fornire un hook in cui eseguire queste funzioni quando `__tcfapi` l&#39;oggetto è pronto.

Per utilizzare IAB TCF 2.0 con i tag e l’estensione Adobe Experience Platform Web SDK, è necessario disporre di uno schema XDM. Se non hai impostato nessuno di questi, inizia visualizzando questa pagina prima di procedere.

Inoltre, questa guida richiede una buona conoscenza di Adobe Experience Platform Web SDK. Per un rapido aggiornamento, leggere [Panoramica di Adobe Experience Platform Web SDK](../../home.md) e [Domande frequenti](../../faq.md) documentazione.

## Abilitazione del consenso predefinito

Se desideri trattare tutti gli utenti sconosciuti allo stesso modo, puoi impostare [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) a `pending` o `out`. In questo modo gli eventi esperienza vengono messi in coda o eliminati finché non vengono ricevute le preferenze di consenso.

### Impostazione del consenso predefinito in base a `gdprApplies`

Alcune CMP consentono di determinare se al cliente si applica il Regolamento generale sulla protezione dei dati (RGPD). Se desideri presumere il consenso per i clienti ai quali non si applica il RGPD, puoi utilizzare `gdprApplies` flag nella chiamata API TCF.

L’esempio seguente mostra un modo per farlo:

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

In questo esempio, la proprietà `configure` viene chiamato dopo il comando `tcData` viene ottenuto dall’API TCF. Se `gdprApplies` è true, il consenso predefinito è impostato su `pending`. Se `gdprApplies` è false, il consenso predefinito è impostato su `in`. Assicurati di compilare il `alloyConfiguration` con la configurazione.

>[!NOTE]
>
>Quando il consenso predefinito è impostato su `in`, il `setConsent` Questo comando può ancora essere utilizzato per registrare le preferenze di consenso dei clienti.

## Utilizzo dell&#39;evento setConsent

L’API IAB TCF 2.0 fornisce un evento per quando il consenso viene aggiornato dal cliente. Ciò si verifica quando il cliente imposta inizialmente le sue preferenze e quando aggiorna le sue preferenze.

L’esempio seguente mostra un modo per farlo:

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

Questo blocco di codice ascolta `useractioncomplete` e quindi imposta il consenso, trasmettendo la stringa di consenso e il `gdprApplies` flag. Se disponi di identità personalizzate per i clienti, assicurati di compilare il `identityMap` variabile. Consulta la guida su [consenso di supporto](../../consent/supporting-consent.md) per ulteriori informazioni sulla chiamata `setConsent`.

## Inclusione delle informazioni sul consenso in sendEvent

All’interno degli schemi XDM, puoi archiviare le informazioni sulle preferenze del consenso dagli eventi Experience. Esistono due modi per aggiungere queste informazioni a ogni evento.

Innanzitutto, puoi fornire lo schema XDM pertinente su ogni `sendEvent` chiamare. L’esempio seguente mostra un modo per farlo:

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

Questo esempio ottiene le informazioni sul consenso per l’API TCF e quindi invia un evento con le informazioni sul consenso aggiunte allo schema XDM.

L’altro modo per aggiungere le informazioni sul consenso a ogni richiesta è con [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) callback.

## Passaggi successivi

Ora che hai imparato a utilizzare IAB TCF 2.0 con l’estensione Platform Web SDK, puoi anche scegliere di integrarla con altre soluzioni di Adobe come Adobe Analytics o Adobe Real-time Customer Data Platform. Consulta la [Panoramica di IAB Transparency &amp; Consent Framework 2.0](./overview.md) per ulteriori informazioni.
