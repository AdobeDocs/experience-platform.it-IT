---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;API;api;
title: Guida all’API del servizio di segmentazione
topic-legacy: guide
description: L’API del servizio di segmentazione consente agli sviluppatori di gestire in modo programmatico le operazioni di segmentazione in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Guida all’API del servizio di segmentazione

[!DNL Adobe Experience Platform Segmentation Service] ti consente di generare segmenti e generare tipi di pubblico in  [!DNL Adobe Experience Platform] dai tuoi  [!DNL Real-time Customer Profile] dati.

L’ API [!DNL Segmentation Service] fornisce più endpoint che consentono di gestire in modo programmatico le operazioni di segmentazione in [!DNL Experience Platform]. Questo documento di panoramica fornisce presentazioni di alto livello per ciascuno di questi endpoint e fornisce collegamenti alle relative guide degli endpoint associate per ulteriori dettagli. Prima di leggere le singole guide degli endpoint, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, fai riferimento al [riferimento API del servizio di segmentazione](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Esportare i processi

I processi di esportazione sono processi asincroni utilizzati per mantenere i membri dei segmenti di pubblico nei set di dati. È possibile utilizzare l&#39;endpoint `/export/jobs` per recuperare tutti i processi di esportazione, creare un nuovo processo di esportazione, recuperare i dettagli di un processo di esportazione specifico o annullare un processo di esportazione specifico.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la [guida all&#39;endpoint dei processi di esportazione](./export-jobs.md).

## Anteprime e stime

Le anteprime forniscono un elenco impaginato di profili qualificati per una definizione di segmento, che consente di confrontare i risultati rispetto alle aspettative. Puoi utilizzare l’endpoint `/preview` per creare un nuovo processo di anteprima o cercare i risultati di un processo di anteprima specifico.

Le stime forniscono informazioni statistiche per le definizioni dei segmenti, come la dimensione del pubblico prevista, l’intervallo di affidabilità e la deviazione standard dell’errore. Puoi utilizzare l’endpoint `/estimate` per visualizzare una stima della definizione di un segmento.

Per ulteriori informazioni sull&#39;utilizzo di questi endpoint, leggere la [guida alle anteprime e alle stime degli endpoint](./previews-and-estimates.md).

## Pianificazioni

Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente i processi di segmentazione batch una volta al giorno. È possibile utilizzare l&#39;endpoint `/config/schedules` per recuperare un elenco di pianificazioni, creare una nuova pianificazione, recuperare i dettagli di una pianificazione specifica, aggiornare una pianificazione specifica o eliminare una pianificazione specifica.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la [guida agli endpoint programmati](./schedules.md).

## Definizioni dei segmenti

Le definizioni dei segmenti definiscono quali profili faranno parte dei segmenti di pubblico. Puoi utilizzare l’endpoint `/segment/definitions` per gestire le definizioni dei segmenti.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consulta la [guida alle definizioni dei segmenti endpoint](./segment-definitions.md).

## Processi dei segmenti

Il processo dei processi di segmento ha stabilito in precedenza le definizioni dei segmenti per generare un segmento di pubblico. Puoi utilizzare l’endpoint `/segment/jobs` per gestire i processi dei segmenti.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consulta la [guida all&#39;endpoint dei processi di segmento](./segment-jobs.md).

## Ricerca di segmenti

La ricerca dei segmenti viene utilizzata per cercare i campi contenuti nelle varie origini dati e per restituirli in tempo quasi reale. Per iniziare a lavorare con la ricerca dei segmenti, consulta la [guida agli endpoint di ricerca](segment-search.md)

## Passaggi successivi

Per iniziare a utilizzare l’ API [!DNL Segmentation Service] , consulta le diverse guide dell’endpoint per i passaggi dettagliati su come effettuare chiamate ai vari endpoint del servizio. Per ulteriori informazioni sull’utilizzo dei segmenti nell’interfaccia utente di [!DNL Platform], consulta la [Guida utente alla segmentazione](../ui/overview.md).
