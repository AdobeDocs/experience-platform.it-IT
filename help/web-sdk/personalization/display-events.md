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

* [Automaticamente](#send-automatically), subito dopo il rendering del contenuto personalizzato sulla pagina. Per ulteriori informazioni, consulta la documentazione su come [eseguire il rendering di contenuti personalizzati](rendering-personalization-content.md).
* [Manualmente](#send-sendEvent-calls), tramite `sendEvent` chiamate successive.

>[!NOTE]
>
>Gli eventi di visualizzazione non vengono inviati automaticamente quando si chiama la funzione `applyPropositions`.

## Invia automaticamente eventi di visualizzazione {#send-automatically}

L’invio automatico di eventi di visualizzazione fornisce metriche di analisi più precise, in quanto l’evento viene inviato immediatamente dopo il caricamento della personalizzazione. Questa implementazione dispone anche di un metodo di implementazione più semplice.

Per inviare automaticamente gli eventi di visualizzazione dopo il rendering del contenuto personalizzato sulla pagina, devi configurare i seguenti parametri:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` o non specificato

Web SDK invia gli eventi di visualizzazione subito dopo aver eseguito il rendering di qualsiasi personalizzazione in seguito a una chiamata `sendEvent`.

## Inviare eventi di visualizzazione nelle chiamate sendEvent successive {#send-sendEvent-calls}

Rispetto a [eventi di visualizzazione inviati automaticamente](#send-automatically), quando li includi nelle chiamate `sendEvent` successive hai anche la possibilità di includere ulteriori informazioni sul caricamento della pagina nella chiamata. Queste potrebbero essere informazioni aggiuntive, che non erano disponibili quando si richiedeva il contenuto personalizzato.

Inoltre, l&#39;invio di eventi di visualizzazione nelle chiamate di `sendEvent` riduce al minimo gli errori di tasso di mancato recapito quando si utilizza Adobe Analytics.

>[!IMPORTANT]
>
>Quando si utilizzano proposte sottoposte a rendering manuale, gli eventi di visualizzazione sono supportati solo tramite chiamate `sendEvent`. In questo caso non è possibile inviare automaticamente eventi di visualizzazione.

### Inviare eventi di visualizzazione per le proposte sottoposte a rendering automatico {#auto-rendered-propositions}

Per inviare eventi di visualizzazione per le proposte sottoposte a rendering automatico, è necessario configurare i seguenti parametri nella chiamata `sendEvent`:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` per l&#39;hit di inizio pagina

Per inviare gli eventi di visualizzazione, chiamare `sendEvent` con `personalization.includePendingDisplayNotifications: true`

### Inviare eventi di visualizzazione per le proposte sottoposte a rendering manuale {#manually-rendered-propositions}

Per inviare eventi di visualizzazione per le proposte sottoposte a rendering manuale, è necessario includerli nel campo XDM `_experience.decisioning.propositions`, inclusi i campi `id`, `scope` e `scopeDetails` delle proposte.

Impostare inoltre il campo `include _experience.decisioning.propositionEventType.display` su `1`.
