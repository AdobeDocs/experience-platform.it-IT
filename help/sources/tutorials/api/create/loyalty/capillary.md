---
title: Connettere Capillary ad Experience Platform utilizzando l’API del servizio Flusso
description: Scopri come collegare Capillary ad Experience Platform utilizzando le API.
hide: true
hidefromtoc: true
badge: Beta
exl-id: 763792d0-d5dc-40ac-b86a-6a0d26463b71
source-git-commit: b3b1542f7e297f4ca872a155ac3801266bc1e6a6
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 2%

---

# Connetti [!DNL Capillary Streaming Events] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

>[!AVAILABILITY]
>
>L&#39;origine [!DNL Capillary Streaming Events] è in versione beta. Leggi i [termini e condizioni](../../../../home.md#terms-and-conditions) nella panoramica delle origini per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta.

Leggi questa guida per scoprire come utilizzare [!DNL Capillary Streaming Events] e l&#39;[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) per inviare dati dal tuo account [!DNL Capillary] a Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Capillary Streaming Events] panoramica](../../../../connectors/loyalty/capillary.md).

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, leggi la guida [guida introduttiva alle API di Experience Platform](../../../../../landing/api-guide.md).

>[!BEGINSHADEBOX]

## Elenco di controllo del processo sviluppatore

1. Crea o scegli lo schema di destinazione **Experience Data Model (XDM)** utilizzando il registro degli schemi. Usa questo schema XDM per **creare un set di dati** in Catalog Service.
2. Crea una **connessione di base** per archiviare le credenziali di [!DNL Capillary].
3. Crea una **connessione di origine** da associare a `baseConnectionId`.
4. Crea una **connessione di destinazione** per assicurarti che i tuoi dati arrivino nel data lake.
5. Utilizza Preparazione dati per creare mappature che mappano i campi di origine [!DNL Capillary] ai campi XDM corretti.
6. Crea un flusso di dati utilizzando `sourceConnectionId`, `targetConnectionId` e `mappingID`
7. Esegui il test con singoli eventi di profilo/transazione di esempio per verificare il flusso di dati.

>[!ENDSHADEBOX]

## Creare una connessione di base {#base-connection}

Una connessione di base conserva le credenziali e i dettagli di connessione. Per creare una connessione di base per [!DNL Capillary], effettuare una richiesta POST all&#39;endpoint `/connections` dell&#39;API [!DNL Flow Service] e fornire le credenziali [!DNL Capillary] nel corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Capillary]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary base connection",
    "description": "Base connection to authenticate the [!DNL Capillary] source.",
    "connectionSpec": {
      "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
      "version": "1.0"
    },
    "auth": {
      "specName": "OAuth generic-rest-connector",
      "params": {
        "clientId": "{CLIENT_ID}",
        "clientSecret": "{CLIENT_SECRET}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    }
  }'
```

**Risposta**

```
A successful response returns the newly created base connection, including its unique connection identifier (id). This ID is required to explore your source's file structure and contents in the next step.

{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Creare una connessione sorgente

Per creare una connessione di origine, eseguire una richiesta POST all&#39;endpoint `/sourceConnections` fornendo l&#39;ID connessione di base.

**Formato API**

```http
POST /flowservice/sourceConnections
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Capillary Streaming",
      "description": "Capillary Streaming",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
          "version": "1.0"
      }
    }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con informazioni dettagliate sulla connessione di origine appena creata, incluso il relativo identificatore univoco (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

### Configurazioni schema

>[!BEGINTABS]

>[!TAB Acquisizione profilo]

I profili contengono attributi di identità e fedeltà. Visualizzare il payload seguente per un esempio basato sullo schema del profilo [!DNL Capillary]. Puoi configurare e mappare questo schema su un singolo profilo XDM.

**Richiesta**

```json
{
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john.doe@capillarytech.com",
        "primary": true
      }
    ]
  },
  "loyalty": {
    "tier": "gold",
    "points": 1250,
    "lifetimePoints": 122,
    "expiredPoints": 12,
    "pointsRedeemed": 500,
    "program": "loyalty program name",
    "status": "active"
  }
}
```

**Risposta**

```json
{
  "id": "8c19f1c3-4b91-47cd-8cb5-b152a93f7349",
  "status": "success",
  "message": "Profile record ingested successfully"
}
```

>[!TAB Acquisizione transazione]

Le transazioni acquisiscono le attività commerciali. Visualizza il seguente payload per un esempio basato sullo schema di eventi [!DNL Capillary]. Puoi configurare e mappare questo schema a un Experience Event XDM.

**Richiesta**

```json
{
  "_id": "T0001",
  "timestamp": "2025-07-14T12:00:00-06:00",
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john@capillarytech.com",
        "primary": true
      }
    ]
  },
  "commerce": {
    "commerceScope": {
      "storeCode": "HSR"
    },
    "order": {
      "priceTotal": 90
    }
  },
  "productLineItems": [
    {
      "SKU": "sku_01",
      "quantity": 1,
      "priceTotal": 100,
      "name": "Kitkat",
      "discountAmount": 10
    }
  ]
}
```

**Risposta**

```json
{
  "id": "T0001",
  "status": "success",
  "message": "Transaction event ingested successfully"
}
```

>[!ENDTABS]

<!--### Supported Events

The [!DNL Capillary] source supports the following events:

* `pointsIssued`
* `tierDowngraded`
* `tierUpgraded`
* `pointsExpiryChange`
* `pointsExpired`
* `transactionUpdated`
* `customerAdded`
* `tierDowngradeReminder`
* `promotionEarned`
* `pointsExpiryReminder`
* `pointsRedeemed`
* `transactionAdded`
* `tierRenewed`
* `customerUpdated`-->

### Migrazione dei dati storici

Puoi inserire in Experience Platform i dati storici relativi a fidelizzazione e transazioni. È sufficiente esportare i dati come file CSV strutturati da [!DNL Capillary], trasferirli in modo sicuro utilizzando [!DNL SFTP] e acquisirli nei set di dati di Experience Platform. Dopo la migrazione iniziale, i dati rimarranno aggiornati in tempo reale tramite il connettore basato su eventi.

### Creare uno schema XDM di destinazione {#target-schema}

Uno schema Experience Data Model (XDM) fornisce un modo standardizzato per organizzare e descrivere i dati sull’esperienza del cliente in Experience Platform. Per acquisire i dati di origine in Experience Platform, devi innanzitutto creare uno schema XDM di destinazione che definisca la struttura e i tipi di dati da acquisire. Questo schema funge da blueprint per il set di dati di Experience Platform in cui risiederanno i dati acquisiti.

È possibile creare uno schema XDM di destinazione eseguendo una richiesta POST all&#39;API [Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Per i passaggi dettagliati su come creare uno schema XDM di destinazione, leggi le seguenti guide:

* [Crea uno schema utilizzando l&#39;API](../../../../../xdm/api/schemas.md).
* [Creare uno schema utilizzando l&#39;interfaccia utente](../../../../../xdm/tutorials/create-schema-ui.md).

Una volta creato, lo schema XDM di destinazione `$id` sarà necessario in seguito per il set di dati di destinazione e la mappatura.

## Creare un set di dati di destinazione {#target-dataset}

Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere strutturato come una tabella con colonne (schema) e righe (campi). I dati acquisiti correttamente in Experience Platform vengono memorizzati nel data lake come set di dati. Durante questo passaggio, puoi creare un nuovo set di dati o utilizzarne uno esistente.

È possibile creare un set di dati di destinazione effettuando una richiesta POST all&#39;API [Catalog Service](https://developer.adobe.com/experience-platform-apis/references/catalog/), fornendo al tempo stesso l&#39;ID dello schema di destinazione all&#39;interno del payload. Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta la guida su [creazione di un set di dati utilizzando l&#39;API](../../../../../catalog/api/create-dataset.md).


## Creare una connessione di destinazione {#target}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui arrivano i dati acquisiti. Per creare una connessione di destinazione, devi fornire l’ID di specifica della connessione fissa associato al data lake. ID della specifica di connessione: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**Formato API**

```http
POST /targetConnections
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Capillary Target Connection",
      "description": "Capillary Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

### Creare una mappatura {#mapping}

Quindi, mappa i dati di origine con lo schema di destinazione a cui aderisce il set di dati di destinazione. Per creare una mappatura, effettuare una richiesta POST all&#39;endpoint `mappingSets` dell&#39;[[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/). Includi l’ID dello schema XDM di destinazione e i dettagli dei set di mappatura che desideri creare.

Mappa i campi Capillary ai campi dello schema XDM corrispondenti come segue:

| Schema di origine | Schema di destinazione |
|------------------------------|-------------------------------|
| `identityMap.email.id` | `xdm:identityMap.email[0].id` |
| `loyalty.points` | `xdm:loyalty.points` |
| `loyalty.tier` | `xdm:loyalty.tier` |
| `commerce.order.priceTotal` | `xdm:commerce.order.priceTotal` |
| `productLineItems.SKU` | `xdm:productListItems.SKU` |

>[!TIP]
>
>È possibile scaricare [Eventi e mappature profilo](../../../../images/tutorials/create/capillary/mappings.zip) per [!DNL Capillary] e [importare i file in Preparazione dati](../../../../../data-prep/ui/mapping.md#import-mapping) quando si è pronti per mappare i dati.

### Creare un flusso di dati {#flow}

Dopo aver creato la connessione di origine, la mappatura e la connessione di destinazione, puoi configurare un flusso di dati per spostare i dati da [!DNL Capillary] ad Experience Platform.

I flussi di dati tipici includono:

* **Flusso di dati profilo**: acquisisce i dati del profilo [!DNL Capillary] in un set di dati profilo individuale XDM.
* **Flusso di dati di transazione**: acquisisce i dati di transazione [!DNL Capillary] in un set di dati ExperienceEvent XDM.

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary dataflow",
    "description": "Capillary → Experience Platform dataflow",
    "flowSpec": {
      "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "version": "1.0"
    },
    "sourceConnectionIds": "{SOURCE_CONNECTION_ID}",
    "targetConnectionIds": "{TARGET_CONNECTION_ID}",
    "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "{MAPPING_ID}",
          "mappingVersion": "0"
        }
      }
    ],
    "scheduleParams": {
      "startTime": "1625040887",
      "frequency": "minute",
      "interval": 15
    }
  }'
```

>[!NOTE]
>
>`startTime` è in secondi dell&#39;epoca UNIX.

**Risposta**

In caso di esito positivo, la risposta restituisce il flusso di dati con l’ID del flusso di dati corrispondente.

```json
{
  "id": "92f11b8c-0a9f-45a9-8239-60b4e8430a88",
  "status": "enabled",
  "message": "Dataflow created successfully"
}
```

## Gestione degli errori

Il connettore include una solida gestione degli errori per i seguenti scenari:

* **Errori di autenticazione**: aggiorna automaticamente le credenziali di Adobe quando l&#39;autenticazione non riesce.
* **Errori limite di frequenza**: implementa nuovi tentativi con backoff esponenziale quando vengono raggiunti i limiti di velocità API.
* **Errori di rete**: registri e nuovi tentativi non riusciti nelle richieste di rete.
* **Errori di convalida dei dati**: registra payload non validi per la revisione e la risoluzione manuali.

Tutti gli errori vengono registrati con dettagli quali il tipo di errore, la marca temporale, il payload della richiesta e la risposta API di Adobe per facilitare la risoluzione dei problemi e il debug.

## Verifica la connessione

Segui i passaggi seguenti per scoprire i passaggi da seguire per verificare la connessione:

* Effettua una richiesta GET a `/connections/{BASE_CONNECTION_ID}` e fornisci l&#39;ID connessione di base per verificare che esista la tua connessione di base. Durante questo passaggio è inoltre possibile verificare che lo stato della connessione di base sia impostato su `active`.
* Effettua una richiesta GET a `/flowservice/sourceConnections/{SOURCE_CONNECTION_ID}` e fornisci l&#39;ID della connessione di origine per verificare la connessione di origine.
* Utilizza l’URL dell’endpoint di streaming per inviare un payload di profilo di esempio (utilizza il codice JSON per l’acquisizione del profilo).
* Passa al set di dati nell’interfaccia utente di Experience Platform ed esegui una query sul set di dati per confermare i record.
* Utilizza i registri della preparazione dati per verificare la presenza di errori.
* Se devi aprire un ticket di supporto, assicurati di disporre dei seguenti elementi:
   * Richiedi payload
   * Corpo della risposta
   * Request-id
   * timestamp
   * ID risorsa.

## Appendice

Consulta la seguente documentazione per guide su operazioni aggiuntive

* [Monitorare i flussi di dati](../../../../../dataflows/ui/monitor-sources.md)
* [Aggiorna flussi di dati](../../../ui/update-dataflows.md)
* [Elimina flussi di dati](../../../ui/delete.md)
* [Aggiorna account di origine](../../../ui/update.md)
