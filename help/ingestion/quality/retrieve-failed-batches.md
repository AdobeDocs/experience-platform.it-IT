---
keywords: Experience Platform;home;argomenti popolari;recuperare batch non riusciti;batch non riusciti;inserimento batch;inserimento batch;batch non riusciti;Recuperare batch non riusciti;Recuperare batch non riusciti;Scaricare batch non riusciti;scaricare batch non riusciti;
solution: Experience Platform
title: Recupero dei batch non riusciti tramite l’API di accesso ai dati
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per recuperare informazioni su un batch non riuscito utilizzando le API di acquisizione dati.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 14%

---

# Recupero di batch non riusciti tramite l’API di accesso ai dati

Adobe Experience Platform fornisce due metodi per caricare e acquisire i dati. È possibile utilizzare l&#39;acquisizione in batch, che consente di inserire i dati utilizzando vari tipi di file (ad esempio CSV), oppure l&#39;acquisizione in streaming, che consente di inserire i dati in [!DNL Platform] utilizzando endpoint di streaming in tempo reale.

Questo tutorial descrive i passaggi necessari per recuperare informazioni su un batch non riuscito utilizzando le API [!DNL Data Ingestion].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
- [[!DNL Data Ingestion]](../home.md): i metodi tramite i quali i dati possono essere inviati a [!DNL Experience Platform].

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- `Content-Type: application/json`

### Batch campione non riuscito

Questa esercitazione utilizzerà dati di esempio con un timestamp formattato in modo errato che imposta il valore del mese su **00**, come illustrato di seguito:

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

Con la risposta precedente, puoi vedere quali blocchi del batch hanno avuto esito positivo o negativo. Da questa risposta è possibile vedere che il file `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contiene il batch non riuscito.

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

Dopo aver letto questa esercitazione, hai imparato a recuperare gli errori dai batch non riusciti. Per ulteriori informazioni sull&#39;acquisizione batch, leggere la [guida per gli sviluppatori sull&#39;acquisizione batch](../batch-ingestion/overview.md). Per ulteriori informazioni sull&#39;acquisizione in streaming, leggere l&#39;[esercitazione sulla creazione di una connessione in streaming](../tutorials/create-streaming-connection.md).

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

Questo errore viene visualizzato se manca `schemaRef` per `xdmMeta`.

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

Questo errore viene visualizzato se `source` nell&#39;intestazione manca il relativo `name`.

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

Questo errore viene visualizzato se non è presente `xdmEntity`.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
