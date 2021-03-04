---
keywords: Experience Platform;home;argomenti popolari;recuperare batch non riusciti;batch non riusciti;acquisizione batch;acquisizione batch;batch non riusciti;ottenere batch non riusciti;ottenere batch non riusciti;scaricare batch non riusciti;scaricare batch non riusciti; scaricare batch non riusciti;
solution: Experience Platform
title: Recupero dei batch con errore tramite API di accesso ai dati
topic: tutorial
type: Tutorial
description: Questa esercitazione descrive i passaggi per recuperare informazioni su un batch con errore utilizzando le API di acquisizione dati.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 2%

---


# Recupero dei batch non riusciti utilizzando l’API di accesso ai dati

Adobe Experience Platform fornisce due metodi per caricare e acquisire i dati. È possibile utilizzare l’acquisizione batch, che consente di inserire i dati utilizzando vari tipi di file (come CSV), o l’acquisizione in streaming, che consente di inserire i dati in [!DNL Platform] utilizzando gli endpoint di streaming in tempo reale.

Questa esercitazione descrive i passaggi per il recupero di informazioni su un batch non riuscito utilizzando le API [!DNL Data Ingestion] .

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
- [[!DNL Data Ingestion]](../home.md): I metodi con cui i dati possono essere inviati a  [!DNL Experience Platform].

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- nome x-sandbox: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: `application/json`

### Batch di esempio non riuscito

Questa esercitazione utilizzerà dati di esempio con una marca temporale in formato non corretto che imposta il valore del mese su **00**, come mostrato di seguito:

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

Il payload di cui sopra non verrà convalidato correttamente rispetto allo schema XDM a causa di una marca temporale non valida.

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
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}
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

Con la risposta di cui sopra, puoi vedere quali blocchi del batch sono riusciti e non riusciti. Da questa risposta, puoi vedere che il file `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contiene il batch non riuscito.

## Scarica il batch non riuscito

Una volta che si è saputo quale file nel batch non è riuscito, è possibile scaricare il file non riuscito e vedere qual è il messaggio di errore.

**Formato API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch che contiene il file non riuscito. |
| `{FAILED_FILE}` | Nome del file con formattazione non riuscita. |

**Richiesta**

La seguente richiesta ti consente di scaricare il file che aveva errori di acquisizione.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Poiché il batch precedentemente acquisito aveva una data-ora non valida, verrà visualizzato il seguente errore di convalida.

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

Dopo aver letto questa esercitazione, hai imparato a recuperare gli errori dai batch con errori. Per ulteriori informazioni sull&#39;acquisizione batch, consulta la [guida per sviluppatori per l&#39;acquisizione batch](../batch-ingestion/overview.md). Per ulteriori informazioni sull&#39;acquisizione in streaming, consulta l&#39; [esercitazione sulla creazione di una connessione in streaming](../tutorials/create-streaming-connection.md).

## Appendice

Questa sezione contiene informazioni su altri tipi di errori di acquisizione che possono verificarsi.

### XDM formattato in modo errato

Come l&#39;errore di marca temporale nel flusso dell&#39;esempio precedente, questi errori sono dovuti a XDM formattati in modo errato. Questi messaggi di errore variano a seconda della natura del problema. Di conseguenza, non è possibile visualizzare alcun esempio di errore specifico.

### ID organizzazione IMS mancante o non valido

Questo errore viene mostrato se l&#39;ID organizzazione IMS mancante dal payload non è valido.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has an absent or wrong ims org in the header"
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
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Nome sorgente mancante

Questo errore viene mostrato se nell’intestazione manca `source` .`name`

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

Questo errore viene mostrato se non è presente `xdmEntity`.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
