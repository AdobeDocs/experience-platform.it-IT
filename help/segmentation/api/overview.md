---
title: Guida API del servizio di segmentazione
description: L’API del servizio di segmentazione consente agli sviluppatori di gestire in modo programmatico le operazioni di segmentazione in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 2%

---

# Guida API del servizio di segmentazione

Adobe Experience Platform [!DNL Segmentation Service] consente di creare tipi di pubblico tramite definizioni di segmenti o altre origini in Adobe Experience Platform dal [!DNL Real-Time Customer Profile] dati.

Il [!DNL Segmentation Service] API fornisce più endpoint che consentono di gestire in modo programmatico le operazioni di segmentazione in [!DNL Experience Platform]. Questo documento fornisce introduzioni di alto livello su ciascuno di questi endpoint e collegamenti alle relative guide degli endpoint associate per ulteriori dettagli. Prima di leggere le guide dei singoli endpoint, consulta [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, leggi le chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, fare riferimento al [Riferimento API del servizio di segmentazione](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Tipi di pubblico

I tipi di pubblico sono una raccolta di persone che condividono comportamenti e/o caratteristiche simili. Questi possono essere generati utilizzando Platform o da sorgenti esterne. È possibile utilizzare `/audiences` endpoint per recuperare tutti i tipi di pubblico, creare un nuovo pubblico, recuperare i dettagli di un pubblico specifico, aggiornare un pubblico specifico o eliminarlo.

Per ulteriori informazioni sull’utilizzo di questo endpoint, consulta la sezione [guida dell’endpoint &quot;audiences&quot;](./audiences.md).

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

Le definizioni dei segmenti definiscono quali profili faranno parte di quale pubblico. È possibile utilizzare `/segment/definitions` endpoint per gestire le definizioni dei segmenti.

Per ulteriori informazioni sull’utilizzo di questo endpoint, consulta la sezione [guida dell’endpoint &quot;segment definitions&quot;](./segment-definitions.md).

## Processi segmento

I processi di segmentazione elaborano definizioni di segmenti stabilite in precedenza per generare un pubblico. È possibile utilizzare `/segment/jobs` endpoint per gestire i processi di segmentazione.

Per ulteriori informazioni sull’utilizzo di questo endpoint, consulta la sezione [guida dell’endpoint &quot;segment jobs&quot;](./segment-jobs.md).

## Ricerca di segmenti

La ricerca dei segmenti viene utilizzata per cercare i campi contenuti in diverse origini dati e restituirli quasi in tempo reale. Per iniziare a lavorare con la ricerca dei segmenti, vedi [guida dell’endpoint &quot;search&quot;](segment-search.md)

## Passaggi successivi

Per iniziare a utilizzare [!DNL Segmentation Service] API, controlla le diverse guide degli endpoint per i passaggi dettagliati su come effettuare chiamate ai vari endpoint del servizio. Per ulteriori informazioni sull’utilizzo dei segmenti con [!DNL Platform] UI, consulta la [Guida utente alla segmentazione](../ui/overview.md).
