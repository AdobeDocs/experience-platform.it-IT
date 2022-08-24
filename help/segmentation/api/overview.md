---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;API;api;
title: Guida all’API del servizio di segmentazione
topic-legacy: guide
description: L’API del servizio di segmentazione consente agli sviluppatori di gestire in modo programmatico le operazioni di segmentazione in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: b48ead4255d50585cd315436ccb9727d86142d4c
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 2%

---

# Guida all’API del servizio di segmentazione

[!DNL Adobe Experience Platform Segmentation Service] consente di generare segmenti e generare tipi di pubblico in [!DNL Adobe Experience Platform] dal [!DNL Real-time Customer Profile] dati.

La [!DNL Segmentation Service] L’API fornisce più endpoint che consentono di gestire in modo programmatico le operazioni di segmentazione in [!DNL Experience Platform]. Questo documento di panoramica fornisce presentazioni di alto livello per ciascuno di questi endpoint e fornisce collegamenti alle relative guide degli endpoint associate per ulteriori dettagli. Prima di leggere le singole guide dei punti finali, fare riferimento alla sezione [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, consulta [Riferimento API del servizio di segmentazione](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Tipi di pubblico

I tipi di pubblico sono un insieme di persone che condividono comportamenti e/o caratteristiche simili. Questi possono essere generati utilizzando Platform o da fonti esterne. È possibile utilizzare `/audiences` per recuperare tutti i tipi di pubblico, creare un nuovo pubblico, recuperare i dettagli di un pubblico specifico, aggiornare un pubblico specifico o eliminare un pubblico specifico.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consulta la sezione [guida all’endpoint per i tipi di pubblico](./audiences.md).

## Esportare i processi

I processi di esportazione sono processi asincroni utilizzati per mantenere i membri dei segmenti di pubblico nei set di dati. È possibile utilizzare `/export/jobs` endpoint per recuperare tutti i processi di esportazione, creare un nuovo processo di esportazione, recuperare i dettagli di un processo di esportazione specifico o annullare un processo di esportazione specifico.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consulta la sezione [guida all’endpoint dei processi di esportazione](./export-jobs.md).

## Anteprime e stime

Le anteprime forniscono un elenco impaginato di profili qualificati per una definizione di segmento, che consente di confrontare i risultati rispetto alle aspettative. È possibile utilizzare `/preview` endpoint per creare un nuovo processo di anteprima o cercare i risultati di un processo di anteprima specifico.

Le stime forniscono informazioni statistiche per le definizioni dei segmenti, come la dimensione del pubblico prevista, l’intervallo di affidabilità e la deviazione standard dell’errore. È possibile utilizzare `/estimate` per visualizzare una stima della definizione di un segmento.

Per ulteriori informazioni sull’utilizzo di questi endpoint, consulta la sezione [guida alle anteprime e alle stime degli endpoint](./previews-and-estimates.md).

## Pianificazioni

Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente i processi di segmentazione batch una volta al giorno. È possibile utilizzare `/config/schedules` per recuperare un elenco di pianificazioni, creare una nuova pianificazione, recuperare i dettagli di una pianificazione specifica, aggiornare una pianificazione specifica o eliminare una pianificazione specifica.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consulta la sezione [guida agli endpoint programmati](./schedules.md).

## Definizioni dei segmenti

Le definizioni dei segmenti definiscono quali profili faranno parte dei segmenti di pubblico. È possibile utilizzare `/segment/definitions` endpoint per la gestione delle definizioni dei segmenti.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consulta la sezione [guida endpoint per le definizioni dei segmenti](./segment-definitions.md).

## Processi dei segmenti

Il processo dei processi di segmento ha stabilito in precedenza le definizioni dei segmenti per generare un segmento di pubblico. È possibile utilizzare `/segment/jobs` endpoint per la gestione dei processi dei segmenti.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consulta la sezione [guida all’endpoint dei processi di segmento](./segment-jobs.md).

## Ricerca di segmenti

La ricerca dei segmenti viene utilizzata per cercare i campi contenuti nelle varie origini dati e per restituirli in tempo quasi reale. Per iniziare a lavorare con la ricerca dei segmenti, vedi [guida all’endpoint di ricerca](segment-search.md)

## Passaggi successivi

Per iniziare a utilizzare [!DNL Segmentation Service] API, consulta le diverse guide degli endpoint per i passaggi dettagliati su come effettuare chiamate ai vari endpoint del servizio. Per ulteriori informazioni sull’utilizzo dei segmenti con la [!DNL Platform] Interfaccia utente, vedi [Guida utente alla segmentazione](../ui/overview.md).
