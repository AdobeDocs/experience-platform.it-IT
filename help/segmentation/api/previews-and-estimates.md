---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida agli endpoint delle anteprime e delle stime
topic: developer guide
translation-type: tm+mt
source-git-commit: 41a5d816f9dc6e7c26141ff5e9173b1b5631d75e
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 2%

---


# Guida agli endpoint delle anteprime e delle stime

Mentre sviluppate la definizione del segmento, potete utilizzare gli strumenti di stima e anteprima all’interno [!DNL Adobe Experience Platform] per visualizzare le informazioni a livello di riepilogo per garantire che l’audience attesa sia isolata. **Le anteprime** forniscono elenchi impaginati di profili idonei per una definizione di segmento, consentendo di confrontare i risultati con quanto previsto. **Le stime** forniscono informazioni statistiche sulla definizione di un segmento, come la dimensione dell&#39;audience prevista, l&#39;intervallo di confidenza e la deviazione standard dell&#39;errore.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39; [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controllate la guida [](./getting-started.md) introduttiva per informazioni importanti che dovete conoscere per effettuare correttamente le chiamate all&#39;API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Modalità di generazione delle stime

Il modo in cui viene attivato il campionamento dei dati dipende dal metodo di assimilazione.

Per l’assimilazione batch, lo store del profilo viene analizzato automaticamente ogni quindici minuti per verificare se un nuovo batch è stato correttamente assimilato dall’ultima esecuzione del processo di campionamento. In tal caso, lo store del profilo viene successivamente analizzato per verificare se il numero di record è stato modificato almeno del 5%. Se tali condizioni sono soddisfatte, viene attivato un nuovo processo di campionamento.

Per l&#39;assimilazione in streaming, lo store del profilo viene automaticamente analizzato ogni ora per verificare se il numero di record è cambiato almeno del 5%. Se questa condizione viene soddisfatta, viene attivato un nuovo processo di campionamento.

La dimensione del campione della scansione dipende dal numero complessivo di entità nell&#39;archivio profili. Queste dimensioni di campione sono rappresentate nella seguente tabella:

| Entità nell&#39;archivio profili | Dimensione del campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

>[!NOTE] Le stime impiegano generalmente dai 10 ai 15 secondi per essere eseguite, a partire da una stima approssimativa e affinando man mano che vengono letti più record.

## Create a new preview {#create-preview}

Potete creare una nuova anteprima effettuando una richiesta POST all’ `/preview` endpoint.

>[!NOTE] Quando viene creato un processo di anteprima, viene creato automaticamente un processo di stima. Questi due processi condividono lo stesso ID.

**Formato API**

```http
POST /preview
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile"
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `predicateExpression` | Espressione PQL per eseguire una query sui dati. |
| `predicateType` | Il tipo di predicato per l&#39;espressione della query in `predicateExpression`. Attualmente, l&#39;unico valore accettato per questa proprietà è `pql/text`. |
| `predicateModel` | Nome dello schema Experience Data Model (XDM) su cui si basano i dati del profilo. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) con i dettagli della nuova anteprima creata.

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `state` | Stato corrente del processo di anteprima. Quando viene creato inizialmente, lo stato sarà &quot;NEW&quot;. Successivamente, sarà in stato &quot;RUNNING&quot; fino al completamento dell&#39;elaborazione, al punto in cui diventa &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `previewId` | L’ID del processo di anteprima, da utilizzare a scopo di ricerca quando si visualizza una stima o un’anteprima, come indicato nella sezione successiva. |

## Recuperare i risultati di un&#39;anteprima specifica {#get-preview}

Potete recuperare informazioni dettagliate su una specifica anteprima effettuando una richiesta GET all&#39; `/preview` endpoint e fornendo l&#39;ID anteprima nel percorso della richiesta.

**Formato API**

```http
GET /preview/{PREVIEW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{PREVIEW_ID}` | Il `previewId` valore dell’anteprima da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sull&#39;anteprima specificata.

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        },
        "state": "RESULT_READY",
        "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
        }
    }],
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `results` | Un elenco di ID entità, con le relative identità. I collegamenti forniti possono essere utilizzati per cercare le entità specificate, utilizzando l&#39;API [di accesso](../../profile/api/entities.md)profilo. |

## Recuperare i risultati di un processo di stima specifico {#get-estimate}

Dopo aver creato un processo di anteprima, potete usarlo `previewId` nel percorso di una richiesta GET all&#39; `/estimate` endpoint per visualizzare informazioni statistiche sulla definizione del segmento, tra cui la dimensione prevista del pubblico, l&#39;intervallo di confidenza e la deviazione standard dell&#39;errore.

**Formato API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{PREVIEW_ID}` | Un processo di stima viene attivato solo quando viene creato un processo di anteprima e i due processi condividono lo stesso valore ID a scopo di ricerca. In modo specifico, si tratta del `previewId` valore restituito al momento della creazione del processo di anteprima. |

**Richiesta**

La richiesta seguente recupera i risultati di un processo di stima specifico.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del processo stimato.

```json
{
    "estimatedSize": 0,
    "numRowsToRead": 1,
    "state": "RESULT_READY",
    "profilesReadSoFar": 1,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 0,
    "totalRows": 1,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `state` | Stato corrente del processo di anteprima. Sarà &quot;IN ESECUZIONE&quot; fino al completamento dell&#39;elaborazione, al punto in cui diventa &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `_links.preview` | Quando lo stato corrente del processo di anteprima è &quot;RESULT_READY&quot;, questo attributo fornisce un URL per visualizzare la stima. |

## Passaggi successivi

Dopo aver letto questa guida è ora possibile comprendere meglio come utilizzare le anteprime e le stime. Per ulteriori informazioni sugli altri endpoint API di Segmentation Service, consulta la panoramica [della guida per gli sviluppatori di](./overview.md)Segmentation Service.