---
title: Gestire gli eventi di visualizzazione in Web SDK
description: Questo articolo spiega cosa sono gli eventi di visualizzazione e come utilizzarli in Web SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Gestire gli eventi di visualizzazione in Web SDK

Gli eventi di visualizzazione vengono utilizzati dall’SDK per web per informare il servizio di personalizzazione o analisi quando in una pagina viene visualizzato un contenuto di personalizzazione specifico.

L’invio di eventi di visualizzazione migliora la precisione delle metriche di personalizzazione e offre una panoramica accurata di ciò che gli utenti visualizzano sulla pagina.

Web SDK consente di inviare eventi di visualizzazione in due modi:

* [Automaticamente](#send-automatically), immediatamente dopo il rendering del contenuto personalizzato sulla pagina. Consulta la documentazione su come [rendering di contenuti personalizzati](rendering-personalization-content.md) per ulteriori informazioni.
* [Manualmente](#send-sendEvent-calls), tramite successiva `sendEvent` chiamate.

>[!NOTE]
>
>Gli eventi di visualizzazione non vengono inviati automaticamente quando si chiama il `applyPropositions` funzione.

## Invia automaticamente eventi di visualizzazione {#send-automatically}

L’invio automatico di eventi di visualizzazione fornisce metriche di analisi più precise, in quanto l’evento viene inviato immediatamente dopo il caricamento della personalizzazione. Questa implementazione dispone anche di un metodo di implementazione più semplice.

Per inviare automaticamente gli eventi di visualizzazione dopo il rendering del contenuto personalizzato sulla pagina, devi configurare i seguenti parametri:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` o non specificato

L’SDK per web invia gli eventi di visualizzazione subito dopo aver eseguito il rendering di qualsiasi personalizzazione a seguito di una `sendEvent` chiamare.

## Inviare eventi di visualizzazione nelle chiamate sendEvent successive {#send-sendEvent-calls}

Confrontato con [automaticamente](#send-automatically) invio di eventi di visualizzazione, quando li includi in `sendEvent` chiamate è inoltre possibile includere ulteriori informazioni sul caricamento della pagina nella chiamata. Queste potrebbero essere informazioni aggiuntive, che non erano disponibili quando si richiedeva il contenuto personalizzato.

Inoltre, l’invio di eventi di visualizzazione in `sendEvent` Le chiamate di minimizzano gli errori di tasso di mancato recapito quando si utilizza Adobe Analytics.

>[!IMPORTANT]
>
>Quando si utilizzano proposte sottoposte a rendering manuale, gli eventi di visualizzazione sono supportati solo tramite `sendEvent` chiamate. In questo caso non è possibile inviare automaticamente eventi di visualizzazione.

### Inviare eventi di visualizzazione per le proposte sottoposte a rendering automatico {#auto-rendered-propositions}

Per inviare eventi di visualizzazione per le proposte sottoposte a rendering automatico, devi configurare i seguenti parametri nel `sendEvent` chiama:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` per l’hit di inizio pagina

Per inviare gli eventi di visualizzazione, chiama `sendEvent` con `personalization.includePendingDisplayNotifications: true`

### Inviare eventi di visualizzazione per le proposte sottoposte a rendering manuale {#manually-rendered-propositions}

Per inviare eventi di visualizzazione per le proposte sottoposte a rendering manuale, è necessario includerli nella `_experience.decisioning.propositions` Campo XDM, incluso `id`, `scope`, e `scopeDetails` campi dalle proposte.

Inoltre, imposta `include _experience.decisioning.propositionEventType.display` campo a `1`.
