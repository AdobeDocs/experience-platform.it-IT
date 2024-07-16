---
title: Guida API del servizio di segmentazione
description: L’API del servizio di segmentazione consente agli sviluppatori di gestire in modo programmatico le operazioni di segmentazione in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 3%

---

# Guida API del servizio di segmentazione

Adobe Experience Platform [!DNL Segmentation Service] consente di creare tipi di pubblico tramite definizioni di segmenti o altre origini in Adobe Experience Platform dai dati di [!DNL Real-Time Customer Profile].

L&#39;API [!DNL Segmentation Service] fornisce più endpoint che consentono di gestire programmaticamente le operazioni di segmentazione in [!DNL Experience Platform]. Questo documento fornisce introduzioni di alto livello su ciascuno di questi endpoint e collegamenti alle relative guide degli endpoint associate per ulteriori dettagli. Prima di leggere le guide dei singoli endpoint, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, consulta il riferimento API del servizio di segmentazione [](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Tipi di pubblico

I tipi di pubblico sono una raccolta di persone che condividono comportamenti e/o caratteristiche simili. Questi possono essere generati utilizzando Platform o da sorgenti esterne. È possibile utilizzare l&#39;endpoint `/audiences` per recuperare tutti i tipi di pubblico, creare un nuovo pubblico, recuperare i dettagli di un pubblico specifico, aggiornare un pubblico specifico o eliminare un pubblico specifico.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la [guida dell&#39;endpoint dei tipi di pubblico](./audiences.md).

## Processi di esportazione

I processi di esportazione sono processi asincroni utilizzati per rendere persistenti i membri del segmento di pubblico nei set di dati. È possibile utilizzare l&#39;endpoint `/export/jobs` per recuperare tutti i processi di esportazione, creare un nuovo processo di esportazione, recuperare i dettagli di un processo di esportazione specifico o annullare un processo di esportazione specifico.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la [guida dell&#39;endpoint dei processi di esportazione](./export-jobs.md).

## Anteprime e stime

Le anteprime forniscono un elenco impaginato di profili idonei per la definizione di un segmento, consentendo di confrontare i risultati rispetto a quelli previsti. È possibile utilizzare l&#39;endpoint `/preview` per creare un nuovo processo di anteprima o cercare i risultati di un processo di anteprima specifico.

Le stime forniscono informazioni statistiche per le definizioni dei segmenti, ad esempio la dimensione del pubblico prevista, l’intervallo di affidabilità e la deviazione standard di errore. È possibile utilizzare l&#39;endpoint `/estimate` per visualizzare una stima della definizione di un segmento.

Per ulteriori informazioni sull&#39;utilizzo di questi endpoint, leggere la [guida delle anteprime e delle stime degli endpoint](./previews-and-estimates.md).

## Pianificazioni

Le pianificazioni sono uno strumento che può essere utilizzato per eseguire automaticamente processi di segmentazione batch una volta al giorno. È possibile utilizzare l&#39;endpoint `/config/schedules` per recuperare un elenco di pianificazioni, creare una nuova pianificazione, recuperare i dettagli di una pianificazione specifica, aggiornare una pianificazione specifica o eliminare una pianificazione specifica.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la [guida degli endpoint di pianificazione](./schedules.md).

## Definizioni dei segmenti

Le definizioni dei segmenti definiscono quali profili faranno parte di quale pubblico. È possibile utilizzare l&#39;endpoint `/segment/definitions` per gestire le definizioni dei segmenti.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la [guida dell&#39;endpoint per le definizioni dei segmenti](./segment-definitions.md).

## Segmenta processi

I processi di segmentazione elaborano definizioni di segmenti stabilite in precedenza per generare un pubblico. È possibile utilizzare l&#39;endpoint `/segment/jobs` per gestire i processi dei segmenti.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, leggere la guida dell&#39;endpoint [segment jobs](./segment-jobs.md).

## Ricerca di segmenti

La ricerca dei segmenti viene utilizzata per cercare i campi contenuti in diverse origini dati e restituirli quasi in tempo reale. Per iniziare a utilizzare la ricerca dei segmenti, consulta la [guida dell&#39;endpoint di ricerca](segment-search.md)

## Passaggi successivi

Per iniziare a utilizzare l&#39;API [!DNL Segmentation Service], consulta le diverse guide degli endpoint per i passaggi dettagliati su come effettuare chiamate ai vari endpoint del servizio. Per ulteriori informazioni sull&#39;utilizzo dei segmenti tramite l&#39;interfaccia utente [!DNL Platform], consulta la [Guida utente per la segmentazione](../ui/overview.md).
