---
keywords: Experience Platform;home;argomenti popolari;recuperare batch non riusciti;batch non riusciti;inserimento batch;inserimento batch;batch non riusciti;Recuperare batch non riusciti;Recuperare batch non riusciti;Scaricare batch non riusciti;scaricare batch non riusciti;
solution: Experience Platform
title: Recupero dei batch non riusciti tramite l’API di accesso ai dati
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per recuperare informazioni su un batch non riuscito utilizzando le API di acquisizione dati.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# Recupero di batch non riusciti tramite l’API di accesso ai dati

Adobe Experience Platform fornisce due metodi per caricare e acquisire i dati. Puoi utilizzare l’acquisizione in batch, che consente di inserire i dati utilizzando vari tipi di file (ad esempio CSV), oppure l’acquisizione in streaming, che consente di inserire i dati in [!DNL Platform] utilizzo di endpoint di streaming in tempo reale.

Questa esercitazione descrive i passaggi per recuperare informazioni su un batch non riuscito utilizzando [!DNL Data Ingestion] API.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
- [[!DNL Data Ingestion]](../home.md): metodi tramite i quali i dati possono essere inviati a [!DNL Experience Platform].

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti al [!DNL Schema Registry], sono isolate in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- `Content-Type: application/json`

### Batch campione non riuscito

Questa esercitazione utilizzerà dati di esempio con una marca temporale formattata in modo errato che imposta il valore del mese su **00**, come illustrato di seguito:

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

Il payload riportato sopra non verrà convalidato correttamente in base allo schema XDM a causa della marca temporale non valida.

## Recupera il batch non riuscito

**Formato API**

```http
GET /batches/{BATCH_ID}/failed
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch che stai cercando. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

Con la risposta precedente, puoi vedere quali blocchi del batch hanno avuto esito positivo o negativo. Da questa risposta, puoi vedere che il file `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contiene il batch non riuscito.

## Scarica il batch non riuscito

Una volta individuato il file non riuscito nel batch, è possibile scaricare il file non riuscito e visualizzare il messaggio di errore.

**Formato API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch che contiene il file non riuscito. |
| `{FAILED_FILE}` | Nome del file con la formattazione non riuscita. |

**Richiesta**

La seguente richiesta ti consente di scaricare il file che presentava errori di acquisizione.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Poiché il batch acquisito precedente aveva una data/ora non valida, verrà visualizzato il seguente errore di convalida.

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## Passaggi successivi

Dopo aver letto questa esercitazione, hai imparato a recuperare gli errori dai batch non riusciti. Per ulteriori informazioni sull’acquisizione batch, consulta [guida per gli sviluppatori sull’acquisizione batch](../batch-ingestion/overview.md). Per ulteriori informazioni sull’acquisizione in streaming, consulta [tutorial sulla creazione di una connessione in streaming](../tutorials/create-streaming-connection.md).

## Appendice

Questa sezione contiene informazioni su altri tipi di errori di acquisizione che possono verificarsi.

### XDM formattato in modo errato

Come l’errore di marca temporale nel flusso di esempio precedente, questi errori sono dovuti a XDM formattato in modo errato. Questi messaggi di errore variano a seconda della natura del problema. Di conseguenza, non è possibile visualizzare alcun esempio di errore specifico.

### ID organizzazione mancante o non valido

Questo errore viene visualizzato se l’ID organizzazione risulta mancante nel payload non è valido.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### Schema XDM mancante

Questo errore viene visualizzato se `schemaRef` per `xdmMeta` è mancante.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Nome sorgente mancante

Questo errore viene visualizzato se `source` nell’intestazione manca il relativo `name`.

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### Entità XDM mancante

Questo errore viene visualizzato se non è `xdmEntity` presente.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
