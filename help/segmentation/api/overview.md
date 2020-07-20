---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: ' Guida per lo sviluppatore del servizio Segmentazione di Adobe Experience Platform'
topic: guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---


#  Guida per lo sviluppo API del servizio di segmentazione del Adobe Experience Platform

[!DNL Adobe Experience Platform Segmentation Service] consente di creare segmenti e generare audience [!DNL Adobe Experience Platform] dai [!DNL Real-time Customer Profile] dati.

L&#39; [!DNL Segmentation Service] API fornisce più endpoint che consentono di gestire in modo programmatico le operazioni di segmentazione in [!DNL Experience Platform]. Questo documento di panoramica fornisce presentazioni di alto livello a ciascuno di questi endpoint e collegamenti alle relative guide degli endpoint associate per ulteriori dettagli. Prima di leggere le singole guide degli endpoint, fate riferimento alla guida [](./getting-started.md) introduttiva per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint e le operazioni CRUD disponibili, fare riferimento al riferimento [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)Segmentation Service.

## Esportare i processi

I processi di esportazione sono processi asincroni utilizzati per mantenere i membri del segmento di pubblico nei set di dati. Potete utilizzare l&#39; `/export/jobs` endpoint per recuperare tutti i processi di esportazione, creare un nuovo processo di esportazione, recuperare i dettagli di un processo di esportazione specifico o annullare un processo di esportazione specifico.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consultate la guida [all&#39;endpoint dei processi di](./export-jobs.md)esportazione.

## Anteprime e stime

Le anteprime forniscono un elenco impaginato di profili di qualifica per una definizione di segmento, che consente di confrontare i risultati rispetto alle aspettative. Potete usare l’ `/preview` endpoint per creare un nuovo processo di anteprima o per cercare i risultati di uno specifico processo di anteprima.

Le stime forniscono informazioni statistiche per le definizioni dei segmenti, come la dimensione dell&#39;audience proiettata, l&#39;intervallo di confidenza e la deviazione standard dell&#39;errore. Puoi utilizzare l&#39; `/estimate` endpoint per visualizzare una stima della definizione di un segmento.

Per ulteriori informazioni sull&#39;utilizzo di questi endpoint, consultate la guida [alle](./previews-and-estimates.md)anteprime e agli endpoint delle stime.

## Pianificazioni

Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente i processi di segmentazione batch una volta al giorno. Potete utilizzare l&#39; `/config/schedules` endpoint per recuperare un elenco di pianificazioni, creare una nuova pianificazione, recuperare i dettagli di una pianificazione specifica, aggiornare una pianificazione specifica o eliminare una pianificazione specifica.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consultate la guida [all&#39;endpoint di](./schedules.md)pianificazione.

## Definizioni dei segmenti

Le definizioni dei segmenti definiscono quali profili faranno parte dei segmenti di pubblico. Puoi utilizzare l&#39; `/segment/definitions` endpoint per gestire le definizioni dei segmenti.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consulta la guida [alle definizioni dei](./segment-definitions.md)segmenti.

## Processi segmento

I processi di segmento hanno definito precedentemente le definizioni dei segmenti per generare un segmento di pubblico. Potete utilizzare l&#39; `/segment/jobs` endpoint per gestire i processi dei segmenti.

Per ulteriori informazioni sull’utilizzo di questo endpoint, consultate la guida [all’endpoint dei processi di](./segment-jobs.md)segmento.

## Ricerca di segmenti

La ricerca dei segmenti viene utilizzata per cercare i campi contenuti in varie origini dati e restituirli in tempo quasi reale. Per iniziare a lavorare con la ricerca dei segmenti, consulta la guida all’endpoint di [ricerca](segment-search.md)

## Passaggi successivi

Per iniziare a utilizzare l&#39; [!DNL Segmentation Service] API, consulta le diverse guide degli endpoint per i passaggi dettagliati su come effettuare chiamate ai vari endpoint del servizio. Per ulteriori informazioni sull’utilizzo dei segmenti nell’ [!DNL Platform] interfaccia utente, consulta la guida [utente alla](../ui/overview.md)segmentazione.