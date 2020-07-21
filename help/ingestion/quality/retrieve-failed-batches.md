---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Recupero batch non riusciti
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 2%

---


# Recupero di batch con errore tramite l&#39;API

 Adobe Experience Platform offre due metodi per caricare e acquisire i dati. Potete utilizzare l’assimilazione batch, che consente di inserire i dati utilizzando vari tipi di file (come i CSV), oppure l’assimilazione in streaming, per inserire i dati [!DNL Platform] utilizzando gli endpoint in streaming in tempo reale.

Questa esercitazione descrive i passaggi per recuperare informazioni su un batch con errore utilizzando [!DNL Data Ingestion] le API.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
- [!DNL Data Ingestion](../home.md): I metodi con cui i dati possono essere inviati [!DNL Experience Platform].

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti al gruppo [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: `application/json`

### Esempio di batch non riuscito

Questa esercitazione utilizzerà dati di esempio con una marca temporale con formattazione non corretta che imposta il valore del mese su **00**, come illustrato di seguito:

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

Il payload sopra non verrà convalidato correttamente rispetto allo schema XDM a causa di marca temporale non valida.

## Recupero del batch non riuscito

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

Con la risposta di cui sopra, potete vedere quali blocchi del batch sono riusciti e non riusciti. Da questa risposta, potete vedere che il file `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contiene il batch con errore.

## Download del batch non riuscito

Una volta che si è saputo quale file del batch non è riuscito, è possibile scaricare il file con errore e vedere qual è il messaggio di errore.

**Formato API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch che contiene il file con errore. |
| `{FAILED_FILE}` | Nome del file con formattazione non riuscita. |

**Richiesta**

La richiesta seguente consente di scaricare il file che ha avuto errori di assimilazione.

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

Poiché la data-ora del precedente batch assimilato non era valida, verrà visualizzato il seguente errore di convalida.

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

Dopo aver letto questa esercitazione, hai imparato a recuperare gli errori dai batch con errore. Per ulteriori informazioni sull&#39;assimilazione batch, leggere la guida [per gli sviluppatori di assimilazione](../batch-ingestion/overview.md)batch. Per ulteriori informazioni sull&#39;assimilazione in streaming, consulta l&#39;esercitazione sulla [creazione di una connessione in streaming](../tutorials/create-streaming-connection.md).

## Appendice

Questa sezione contiene informazioni su altri tipi di errori di assimilazione che possono verificarsi.

### Formato XDM non corretto

Come l&#39;errore di marca temporale nel flusso precedente, questi errori sono dovuti a XDM formattati in modo non corretto. Questi messaggi di errore variano a seconda della natura del problema. Di conseguenza, non è possibile visualizzare alcun esempio di errore specifico.

### ID organizzazione IMS mancante o non valido

Questo errore viene mostrato se l&#39;ID organizzazione IMS mancante nel payload non è valido.

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

Questo errore viene visualizzato se `schemaRef` manca il `xdmMeta` modulo.

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

### Nome origine mancante

Questo errore viene mostrato se `source` nell’intestazione manca il valore `name`.

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

Questo errore viene mostrato se non è `xdmEntity` presente.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
