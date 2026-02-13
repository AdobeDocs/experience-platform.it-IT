---
title: Panoramica sui casi di utilizzo di Personalization
description: Scopri come implementare casi di utilizzo di personalizzazione utilizzando Adobe Experience Platform Web SDK, inclusi modelli per il rendering del contenuto e la visualizzazione del tracciamento.
keywords: personalizzazione;sendEvent;renderDecisions;applyPropositions;decisionScopes;display events;flicker;
exl-id: 6beccbfd-fddb-4e19-8a56-caba276e1643
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Panoramica sui casi di utilizzo di Personalization

Adobe Experience Platform Web SDK consente un&#39;ampia varietà di casi di utilizzo di personalizzazione per le proprietà web. Supporta architetture flessibili (lato client, lato server e ibride) che consentono di richiedere decisioni ed eseguire il rendering dei contenuti in base alle esigenze del sito.

## Rendering di contenuti personalizzati

Il Web SDK può recuperare le decisioni di personalizzazione (note anche come _proposte_) e aiutarti a renderle sulla pagina. Il rendering è asincrono, pertanto evita di assumere un intervallo specifico per l’applicazione del contenuto.

Scegli il pattern che corrisponde agli elementi della proposta che ricevi:

1. **Esegui automaticamente il rendering delle proposte di azione DOM**: da utilizzare quando le proposte includono `dom-action` elementi con selettori e tipi di azione che Web SDK può applicare automaticamente. Consulta [Eseguire automaticamente il rendering delle proposte di azione DOM](render-auto-pers-content.md).
1. **Esegui rendering delle offerte HTML senza selettori utilizzando applyPropositions**: utilizza quando ricevi contenuti HTML, ma devi specificare dove e come applicarli (selettore + tipo di azione) tramite metadati. Consulta [Rendering delle offerte HTML senza selettori](render-html-offers.md).
1. **Proposte di rendering manuali**: da utilizzare quando è necessario il controllo completo della logica di rendering (ad esempio, la composizione dell&#39;interfaccia utente da JSON o l&#39;applicazione di regole business personalizzate). Consulta [Eseguire manualmente il rendering delle proposte](render-manual-propositions.md).

>[!TIP]
>
>Questi pattern possono essere combinati. Ad esempio, puoi abilitare il rendering automatico delle azioni DOM ed eseguire manualmente il rendering del contenuto da ambiti decisionali specifici.

## Argomenti correlati comuni

La maggior parte delle implementazioni di personalizzazione riguardano i seguenti argomenti comuni:

* **Impedisci visualizzazione momentanea di altri contenuti** (facoltativo): nascondi e mostra i contenitori durante la personalizzazione. Vedi [Gestione visualizzazione momentanea di altri contenuti](manage-flicker.md).
* **Tieni traccia di ciò che è stato visualizzato**: registra gli eventi di visualizzazione per il contenuto sottoposto a rendering. Vedi [Gestione eventi di visualizzazione](display-events.md).
* **Recupero dall&#39;alto della pagina / metriche dal basso della pagina**: richiedi decisioni in anticipo, quindi includi la misurazione in un secondo momento. Consulta [Configurare gli eventi di inizio e fine pagina](top-bottom-page-events.md).

## Esempi di Web SDK

Oltre alle pagine dei documenti in questa cartella, Adobe gestisce un archivio di applicazioni di esempio a cui puoi fare riferimento. Vedi [Esempi di Web SDK](https://github.com/adobe/alloy-samples/) su GitHub per ulteriori scenari di personalizzazione, tra cui:

* Personalizzazione lato client
* Personalizzazione lato server
* Personalizzazione ibrida
* Personalization nelle applicazioni a pagina singola
