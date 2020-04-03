---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori di Segmentation Service
topic: developer guide
translation-type: tm+mt
source-git-commit: 38762fa57188ed018c4347c07765f3d09daef2e6

---


# Guida per gli sviluppatori di Segmentation Service

La segmentazione consente di creare segmenti e generare audience in Adobe Experience Platform a partire dai dati del profilo cliente in tempo reale.

## Introduzione

Questa guida richiede una buona conoscenza dei vari servizi Adobe Experience Platform coinvolti nell&#39;utilizzo della segmentazione.

- [Segmentazione](../home.md): Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
- [Sistema](../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
- [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per utilizzare correttamente la segmentazione tramite l&#39;API.

### Lettura di chiamate API di esempio

La documentazione API del servizio di segmentazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Intestazioni necessarie

La documentazione API richiede inoltre di aver completato l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate agli endpoint piattaforma. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste nelle chiamate API di Experience Platform, come illustrato di seguito:

- Autorizzazione: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>**Nota:** Per ulteriori informazioni sull’utilizzo delle sandbox in Experience Platform, consulta la documentazione [sulla panoramica delle](../../sandboxes/home.md)sandbox.

<!-- ## Estimates

Estimates provides statistical information for a segment definition, such as projected audience size and confidence interval. You can use the `/estimate` endpoint to view an estimate of a segment definition. 

For more information on using this endpoint, please read the [estimates developer guide](./estimates.md). 

## Export jobs

Export jobs are asynchronous processes that are used to persist audience segment members to datasets. You can use the `/export/jobs` endpoint to retrieve all export jobs, create a new export job, retrieve details of a specific export job, or cancel a specific export job.

For more information on using this endpoint, please read the [export jobs developer guide](./export-jobs.md).

## Previews

Previews provide a paginated list of qualifying profiles for a segment definition, allowing you to compare the results against what you expect. You can use the `/preview` endpoint to create a new preview job, look up results of a specific preview job, or delete a specific preview job.

For more information on using this endpoint, please read the [previews developer guide](./previews.md).

## PQL conversions

Profile Query Language (PQL) conversions allows you to convert your formatting between `pql/text` and `pql/json`. You can do this by using the `/segment/conversion` endpoint.

For more information on using this endpoint, please read the [PQL conversions developer guide](./pql-conversions.md).

## Schedules

Schedules are a tool that can be used to automatically run export jobs once a day. You can use the `/config/schedules` endpoint to retrieve a list of schedules, create a new schedule, retrieve details of a specific schedule, update a specific schedule, or delete a specific schedule. 

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md).

## Segment definitions

Segment definitions define which profiles will be part of which audience segments. You can use the `/segment/definitions` endpoint to retrieve a list of segment definitions, create a new segment definition, retrieve details of a specific segment definition, delete a specific segment definition, or overwrite details of a specific segment definition.

For more information on using this endpoint, please read the [segment definitions developer guide](./segment-definitions.md). -->

## Processi segmento

I processi di segmento hanno definito precedentemente le definizioni dei segmenti per generare un segmento di pubblico. Potete utilizzare l&#39; `/segment/jobs` endpoint per recuperare un elenco di processi di segmento, creare un nuovo processo di segmento, recuperare i dettagli di un processo di segmento specifico o eliminare un processo di segmento specifico.

Per ulteriori informazioni sull&#39;utilizzo di questo endpoint, consultate la guida [per gli sviluppatori di processi di](./segment-jobs.md)segmento.

## Passaggi successivi

Per iniziare a effettuare chiamate tramite l’API di segmentazione, seleziona una delle guide secondarie per apprendere come utilizzare endpoint specifici correlati alla segmentazione. Per ulteriori informazioni sull’utilizzo dei segmenti tramite l’interfaccia utente della piattaforma, consulta la guida [utente alla](../ui/overview.md)segmentazione.