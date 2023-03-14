---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;servizio di segmentazione;API;api;
title: Guida API del servizio di segmentazione
description: L’API del servizio di segmentazione consente agli sviluppatori di gestire in modo programmatico le operazioni di segmentazione in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---

# Guida API del servizio di segmentazione

[!DNL Adobe Experience Platform Segmentation Service] consente di creare segmenti e generare tipi di pubblico in [!DNL Adobe Experience Platform] dal tuo [!DNL Real-Time Customer Profile] dati.

Il [!DNL Segmentation Service] API fornisce più endpoint che consentono di gestire in modo programmatico le operazioni di segmentazione in [!DNL Experience Platform]. Questo documento fornisce introduzioni di alto livello su ciascuno di questi endpoint e collegamenti alle relative guide degli endpoint associate per ulteriori dettagli. Prima di leggere le guide dei singoli endpoint, consulta [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, leggi le chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, fare riferimento al [Riferimento API del servizio di segmentazione](https://www.adobe.io/experience-platform-apis/references/segmentation/).

<!-- ## Audiences

Audiences are a collection of people who share similar behaviors and/or characteristics. These can be generated either by using Platform or from external sources. You can use the `/audiences` endpoint to retrieve all audiences, create a new audience, retrieve details of a specific audience, update a specific audience, or delete a specific audience.

For more information on using this endpoint, please read the [audiences endpoint guide](./audiences.md). -->

## Processi di esportazione

I processi di esportazione sono processi asincroni utilizzati per rendere persistenti i membri del segmento di pubblico nei set di dati. È possibile utilizzare `/export/jobs` endpoint per recuperare tutti i processi di esportazione, creare un nuovo processo di esportazione, recuperare i dettagli di un processo di esportazione specifico o annullare un processo di esportazione specifico.

Per ulteriori informazioni sull’utilizzo di questo endpoint, consulta la sezione [guida dell’endpoint &quot;export jobs&quot;](./export-jobs.md).

## Anteprime e stime

Le anteprime forniscono un elenco impaginato di profili idonei per la definizione di un segmento, consentendo di confrontare i risultati rispetto a quelli previsti. È possibile utilizzare `/preview` endpoint per creare un nuovo processo di anteprima o cercare i risultati di un processo di anteprima specifico.

Le stime forniscono informazioni statistiche per le definizioni dei segmenti, ad esempio la dimensione del pubblico prevista, l’intervallo di affidabilità e la deviazione standard di errore. È possibile utilizzare `/estimate` per visualizzare una stima della definizione di un segmento.

Per ulteriori informazioni sull’utilizzo di questi endpoint, consulta la sezione [guida alle anteprime e alle stime degli endpoint](./previews-and-estimates.md).

## Schedules

Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente processi di segmentazione batch una volta al giorno. È possibile utilizzare `/config/schedules` endpoint per recuperare un elenco di pianificazioni, creare una nuova pianificazione, recuperare i dettagli di una pianificazione specifica, aggiornare una pianificazione specifica o eliminarla.

Per ulteriori informazioni sull’utilizzo di questo endpoint, consulta la sezione [guida dell’endpoint &quot;schedule&quot;](./schedules.md).

## Definizioni dei segmenti

Le definizioni dei segmenti definiscono quali profili faranno parte di quali segmenti di pubblico. È possibile utilizzare `/segment/definitions` endpoint per gestire le definizioni dei segmenti.

Per ulteriori informazioni sull’utilizzo di questo endpoint, consulta la sezione [guida dell’endpoint &quot;segment definitions&quot;](./segment-definitions.md).

## Processi segmento

I processi di segmentazione elaborano le definizioni dei segmenti stabilite in precedenza per generare un segmento di pubblico. È possibile utilizzare `/segment/jobs` endpoint per gestire i processi di segmentazione.

Per ulteriori informazioni sull’utilizzo di questo endpoint, consulta la sezione [guida dell’endpoint &quot;segment jobs&quot;](./segment-jobs.md).

## Ricerca di segmenti

La ricerca dei segmenti viene utilizzata per cercare i campi contenuti in diverse origini dati e restituirli quasi in tempo reale. Per iniziare a lavorare con la ricerca dei segmenti, vedi [guida dell’endpoint &quot;search&quot;](segment-search.md)

## Passaggi successivi

Per iniziare a utilizzare [!DNL Segmentation Service] API, controlla le diverse guide degli endpoint per i passaggi dettagliati su come effettuare chiamate ai vari endpoint del servizio. Per ulteriori informazioni sull’utilizzo dei segmenti con [!DNL Platform] UI, consulta la [Guida utente alla segmentazione](../ui/overview.md).
