---
keywords: Experience Platform;home;argomenti popolari; avvisi
description: Puoi abbonarti agli avvisi durante la creazione di un flusso di dati per ricevere messaggi di avviso sullo stato, il successo o l’errore dell’esecuzione del flusso.
title: Iscriviti agli avvisi contestuali nell’interfaccia utente
hide: true
hidefromtoc: true
source-git-commit: a81d21f615206e644044c2f0f546a458d1aebbf3
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Iscriviti per inviare messaggi di avviso per monitorare i flussi di dati sorgente nell’interfaccia utente

Adobe Experience Platform ti consente di abbonarti a avvisi basati su eventi relativi alle attività Adobe Experience Platform. Gli avvisi riducono o eliminano la necessità di eseguire il polling [[!DNL Observability Insights] API](../../../observability/api/overview.md) per verificare se un processo è stato completato, se è stata raggiunta una determinata fase cardine all’interno di un flusso di lavoro o se si sono verificati errori.

Puoi abbonarti agli avvisi durante la creazione di un flusso di dati per ricevere messaggi di avviso sullo stato, il successo o l’errore dell’esecuzione del flusso.

Questo documento fornisce passaggi su come sottoscrivere avvisi e ricevere messaggi di avviso per le esecuzioni di flusso.

## Introduzione

Questo documento richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Osservabilità](../../../observability/home.md): [!DNL Observability Insights] consente di monitorare le attività di Platform mediante l’utilizzo di metriche statistiche e notifiche di eventi.
   * [Avvisi](../../../observability/alerts/overview.md): Quando viene raggiunto un certo set di condizioni nelle operazioni di Platform (ad esempio un potenziale problema in caso di superamento di una soglia), Platform può inviare messaggi di avviso a tutti gli utenti dell’organizzazione che si sono abbonati.

## Iscriviti agli avvisi nell’interfaccia utente {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Iscriviti agli avvisi di origine"
>abstract="Gli avvisi consentono di ricevere notifiche in base allo stato dei flussi di dati sorgente. Puoi impostare le notifiche di avviso per ottenere aggiornamenti se il flusso di dati è stato avviato, ha avuto esito positivo, non è riuscito o non ha acquisito dati."
>text="Learn more in documentation"
