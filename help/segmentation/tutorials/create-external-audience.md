---
title: Creare e attivare un pubblico esterno
type: Tutorial
description: Scopri come creare un pubblico esterno in Adobe Experience Platform utilizzando le API di Experience Platform.
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 3%

---


# Creare e attivare un pubblico esterno tramite l’API

Questo tutorial illustra i passaggi necessari per creare un pubblico esterno utilizzando le API di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei vari servizi Experience Platform coinvolti nella creazione di un pubblico esterno. Prima di iniziare questo tutorial, leggi la documentazione dei seguenti servizi:

- [Origini](../../sources/home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): consente di creare tipi di pubblico dai dati esterni.
- [Destinazioni](../../destinations/home.md): le destinazioni sono integrazioni predefinite con applicazioni di uso comune che consentono l&#39;attivazione diretta dei dati da Experience Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e altro ancora.

### Intestazioni richieste

Questo tutorial richiede anche di aver completato l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate alle API [!DNL Experience Platform]. Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Le richieste alle API [!DNL Experience Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste POST, PUT e PATCH richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

## Preparare il pubblico esterno {#prepare}

Prima di poter creare un pubblico esterno all’interno di Experience Platform, devi preparare un file che contenga i dati del pubblico.

In questo esempio, devi utilizzare un file CSV. Verifica che il file CSV contenga **almeno** una colonna con un valore di identità come ECID, ID e-mail o ID CRM. Inoltre, assicurati che contenga tutti gli attributi di arricchimento necessari per la segmentazione e l’attivazione.

È inoltre necessario assicurarsi che il file sia conforme ai requisiti dello schema di Experience Platform. Per ulteriori informazioni sulla creazione di uno schema, leggere l&#39;[esercitazione sulla creazione di uno schema tramite API](/help/xdm/tutorials/create-schema-api.md) o l&#39;[esercitazione sulla creazione di uno schema tramite l&#39;interfaccia utente](/help/xdm/tutorials/create-schema-ui.md).

Dopo aver confermato che il file CSV contiene tutte le informazioni necessarie e che è conforme allo schema, devi caricare il file CSV nel provider di archiviazione cloud in modo da poter utilizzare le origini per acquisire i dati in Experience Platform. Per ulteriori informazioni sull&#39;utilizzo di un&#39;origine di archiviazione cloud, leggere l&#39;[esercitazione sull&#39;esplorazione delle opzioni di archiviazione cloud tramite l&#39;API](/help/sources/tutorials/api/explore/cloud-storage.md) o la [panoramica delle origini](/help/sources/home.md#cloud-storage).

## Creare un pubblico esterno {#create}

Dopo aver preparato il file CSV, ora puoi avviare il processo di creazione del pubblico esterno.

Per creare un pubblico esterno, devi eseguire una richiesta POST all&#39;endpoint `/external-audience/`.

Quando effettui questa richiesta, devi specificare le seguenti informazioni:

- Nome del pubblico
- Una descrizione per il pubblico
- Campi corrispondenti tra il file CSV e lo schema
- Informazioni sulla specifica di origine
   - Questo include il percorso del file CSV da acquisire
      - Il percorso del file **non può** contenere spazi. Ad esempio, se il percorso è `activation/sample-source/Example CSV File.csv`, impostare il percorso su `activation/sample-source/ExampleCSVFile.csv`.

Per informazioni più dettagliate su come utilizzare questo endpoint, consulta la [guida dell&#39;endpoint tipi di pubblico esterni](/help/segmentation/api/external-audiences.md#create-audience).

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

+++

Dopo aver effettuato questa richiesta, assicurati di prendere nota di `operationId` che ricevi dalla risposta in modo da poter recuperare l&#39;ID del pubblico.

## Recupera ID pubblico {#retrieve-audience-id}

Dopo aver creato il pubblico esterno, devi ottenere l’ID del pubblico in modo da poterlo inserire in Experience Platform.

Per recuperare l&#39;ID del pubblico, devi eseguire una richiesta GET all&#39;endpoint `/external-audiences/operations` e fornire l&#39;ID dell&#39;operazione precedentemente ricevuta dalla risposta di creazione del pubblico esterno.

Per informazioni più dettagliate su come utilizzare questo endpoint, consulta la [guida dell&#39;endpoint per pubblico esterno](/help/segmentation/api/external-audiences.md#retrieve-status).

+++ Richiesta

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/{OPERATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

Dopo aver effettuato questa richiesta, accertati di prendere nota di `audienceId` che ricevi dalla risposta in modo da poter attivare il processo di acquisizione per il pubblico.

## Avvia l’acquisizione del pubblico {#start-ingestion}

Poiché hai `audienceId`, ora puoi attivare l&#39;acquisizione del pubblico esterno in Experience Platform.

Per avviare l’acquisizione di un pubblico, effettua una richiesta POST all’endpoint seguente e specifica l’ID del pubblico. Inoltre, è necessario specificare l&#39;ora di inizio per determinare quali file verranno elaborati.

Per informazioni più dettagliate su come utilizzare questo endpoint, consulta la [guida dell&#39;endpoint per tipi di pubblico esterni](/help/segmentation/api/external-audiences.md#start-audience-ingestion)

+++ Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

+++

Dopo aver effettuato questa richiesta, assicurati di prendere nota di `runId` che ricevi dalla risposta in modo da poter monitorare lo stato di acquisizione.

## Monitorare lo stato di acquisizione {#monitor-ingestion}

Dopo aver attivato l’acquisizione del pubblico, ora puoi monitorare i progressi dell’acquisizione per confermarne il successo e convalidare la disponibilità del pubblico per l’attivazione a valle.

Per recuperare lo stato di un’acquisizione di pubblico, effettua una richiesta GET al seguente endpoint e allo stesso tempo fornisce sia l’ID del pubblico che gli ID di esecuzione.

Per informazioni più dettagliate su come utilizzare questo endpoint, consulta la [guida dell&#39;endpoint per pubblico esterno](/help/segmentation/api/external-audiences.md#retrieve-ingestion-status).

+++ Richiesta

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs/{RUN_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

## Passaggi successivi {#next-steps}

>[!IMPORTANT]
>
>Per utilizzare il pubblico generato esternamente, **devi** attendere il completamento del processo di segmentazione giornaliero.

Una volta confermato che il pubblico esterno è stato acquisito correttamente, puoi visualizzarlo in Audience Portal e utilizzarlo in servizi a valle come le destinazioni.

Per ulteriori informazioni su Audience Portal, consulta la [Guida dell&#39;interfaccia utente di Audience Portal](/help/segmentation/ui/audience-portal.md). Per ulteriori informazioni sulle destinazioni, leggere la [panoramica sulle destinazioni](/help/destinations/home.md).

