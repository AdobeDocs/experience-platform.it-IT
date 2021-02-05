---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Segmentation Service;API;api;'
title: Guida API del servizio di segmentazione
topic: guide
description: L’API del servizio di segmentazione consente agli sviluppatori di gestire le operazioni di segmentazione in Adobe Experience Platform a livello di programmazione. Seguite questa guida per apprendere come eseguire operazioni chiave tramite l'API.
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# Guida API del servizio di segmentazione

[!DNL Adobe Experience Platform Segmentation Service] consente di creare segmenti e generare audience  [!DNL Adobe Experience Platform] dai  [!DNL Real-time Customer Profile] dati.

L&#39;API [!DNL Segmentation Service] fornisce più endpoint che consentono di gestire in modo programmatico le operazioni di segmentazione in [!DNL Experience Platform]. Questo documento di panoramica fornisce presentazioni di alto livello a ciascuno di questi endpoint e collegamenti alle relative guide degli endpoint associate per ulteriori dettagli. Prima di leggere le singole guide degli endpoint, consultare la [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, per leggere chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, fare riferimento al [riferimento API del servizio di segmentazione](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Esportare i processi

I processi di esportazione sono processi asincroni utilizzati per mantenere i membri del segmento di pubblico nei set di dati. Potete utilizzare l&#39;endpoint `/export/jobs` per recuperare tutti i processi di esportazione, creare un nuovo processo di esportazione, recuperare i dettagli di un processo di esportazione specifico o annullare un processo di esportazione specifico.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la guida [all&#39;endpoint dei processi di esportazione](./export-jobs.md).

## Anteprime e stime

Le anteprime forniscono un elenco impaginato di profili di qualifica per una definizione di segmento, che consente di confrontare i risultati rispetto alle aspettative. Potete utilizzare l&#39;endpoint `/preview` per creare un nuovo processo di anteprima o per cercare i risultati di uno specifico processo di anteprima.

Le stime forniscono informazioni statistiche per le definizioni dei segmenti, come la dimensione dell&#39;audience proiettata, l&#39;intervallo di confidenza e la deviazione standard dell&#39;errore. Puoi utilizzare l&#39;endpoint `/estimate` per visualizzare una stima della definizione di un segmento.

Per ulteriori informazioni sull&#39;utilizzo di questi endpoint, leggere la guida [anteprime e stime degli endpoint](./previews-and-estimates.md).

## Pianificazioni

Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente i processi di segmentazione batch una volta al giorno. È possibile utilizzare l&#39;endpoint `/config/schedules` per recuperare un elenco di pianificazioni, creare una nuova pianificazione, recuperare i dettagli di una pianificazione specifica, aggiornare una pianificazione specifica o eliminare una pianificazione specifica.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la [guida dell&#39;endpoint di pianificazione](./schedules.md).

## Definizioni dei segmenti

Le definizioni dei segmenti definiscono quali profili faranno parte dei segmenti di pubblico. Puoi utilizzare l&#39;endpoint `/segment/definitions` per gestire le definizioni dei segmenti.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la guida [alle definizioni dei segmenti endpoint](./segment-definitions.md).

## Processi segmento

I processi di segmento hanno definito precedentemente le definizioni dei segmenti per generare un segmento di pubblico. Puoi utilizzare l&#39;endpoint `/segment/jobs` per gestire i processi dei segmenti.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la guida [all&#39;endpoint dei processi del segmento](./segment-jobs.md).

## Ricerca di segmenti

La ricerca dei segmenti viene utilizzata per cercare i campi contenuti in varie origini dati e restituirli in tempo quasi reale. Per iniziare a lavorare con la ricerca dei segmenti, vedi la [guida all&#39;endpoint di ricerca](segment-search.md)

## Passaggi successivi

Per iniziare a utilizzare l&#39;API [!DNL Segmentation Service], controlla le diverse guide dell&#39;endpoint per i passaggi dettagliati su come effettuare chiamate ai vari endpoint del servizio. Per ulteriori informazioni sull&#39;utilizzo dei segmenti nell&#39;interfaccia [!DNL Platform], vedere la [Guida utente alla segmentazione](../ui/overview.md).