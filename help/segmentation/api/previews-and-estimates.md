---
solution: Experience Platform
title: Endpoint API per anteprime e stime
description: Man mano che vengono sviluppate le definizioni dei segmenti, puoi utilizzare gli strumenti di stima e anteprima disponibili in Adobe Experience Platform per visualizzare informazioni di riepilogo utili a isolare il pubblico previsto.
role: Developer
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 2%

---

# Anteprime ed endpoint di stima

Quando sviluppi una definizione di segmento, puoi utilizzare gli strumenti di stima e anteprima in Adobe Experience Platform per visualizzare informazioni di riepilogo per accertarti di isolare il pubblico previsto.

* **Anteprime** fornisce elenchi impaginati di profili idonei per la definizione di un segmento, che consentono di confrontare i risultati con quelli previsti.

* **Stime** fornisci informazioni statistiche sulla definizione di un segmento, ad esempio le dimensioni del pubblico previste, l’intervallo di affidabilità e la deviazione standard dell’errore.

>[!NOTE]
>
>Per accedere a metriche simili relative ai dati del Profilo cliente in tempo reale, ad esempio il numero totale di frammenti di profilo e profili uniti all’interno di spazi dei nomi specifici o dell’archivio dati profilo nel suo complesso, consulta la [guida dell’endpoint &quot;profile preview&quot; (anteprima stato del campione)](../../profile/api/preview-sample-status.md), parte della guida per gli sviluppatori API per profili.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controlla [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all’API, incluse le intestazioni richieste e la lettura di esempi di chiamate API.

## Come vengono generate le stime

Quando l’acquisizione dei record nell’archivio profili aumenta o diminuisce il conteggio totale dei profili di oltre il 5%, viene attivato un processo di campionamento per aggiornare il conteggio. Il modo in cui viene attivato il campionamento dei dati dipende dal metodo di acquisizione:

* **Acquisizione in batch:** Per l’acquisizione batch, entro 15 minuti dalla corretta acquisizione di un batch nell’archivio profili, se viene raggiunta la soglia di aumento o di riduzione del 5%, viene eseguito un processo per aggiornare il conteggio.
* **Acquisizione in streaming:** Per i flussi di lavoro di dati in streaming, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o riduzione del 5% è stata raggiunta. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio.

La dimensione del campione della scansione dipende dal numero complessivo di entità nell’archivio profili. Queste dimensioni di esempio sono rappresentate nella tabella seguente:

| Entità nell’archivio profili | Dimensione campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

>[!NOTE]
>
>L’esecuzione delle stime richiede generalmente dai 10 ai 15 secondi, a partire da una stima approssimativa e con la lettura di più record.

## Crea una nuova anteprima {#create-preview}

Per creare una nuova anteprima, devi effettuare una richiesta POST al `/preview` endpoint.

>[!NOTE]
>
>Quando si crea un processo di anteprima, viene creato automaticamente un processo di stima. Questi due processi condivideranno lo stesso ID.

**Formato API**

```http
POST /preview
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `predicateExpression` | L’espressione PQL in base alla quale eseguire la query dei dati. |
| `predicateType` | Tipo di predicato per l’espressione di query in `predicateExpression`. Attualmente, l’unico valore accettato per questa proprietà è `pql/text`. |
| `predicateModel` | Il nome del [!DNL Experience Data Model] (XDM) classe di schema su cui si basano i dati del profilo. |
| `graphType` | Tipo di grafico da cui ottenere il cluster. I valori supportati sono `none` (non esegue alcuna unione di identità) e `pdg` (esegue l’unione delle identità in base al grafico delle identità private). |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) con i dettagli della nuova anteprima creata.

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
| `state` | Stato corrente del processo di anteprima. Al momento della creazione, lo stato sarà &quot;NUOVO&quot;. Successivamente, sarà nello stato &quot;RUNNING&quot; (IN ESECUZIONE) fino al completamento dell’elaborazione, che diventa &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `previewId` | ID del processo di anteprima, da utilizzare a scopo di ricerca quando si visualizza una stima o un’anteprima, come descritto nella sezione successiva. |

## Recuperare i risultati di un’anteprima specifica {#get-preview}

Per recuperare informazioni dettagliate su un’anteprima specifica, effettua una richiesta GET al `/preview` e fornendo l’ID di anteprima nel percorso della richiesta.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sull’anteprima specificata.

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
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `results` | Un elenco di ID entità, insieme alle relative identità. I collegamenti forniti possono essere utilizzati per cercare le entità specificate utilizzando [endpoint API di accesso al profilo](../../profile/api/entities.md). |

## Recuperare i risultati di un processo di stima specifico {#get-estimate}

Dopo aver creato un processo di anteprima, puoi utilizzarne `previewId` nel percorso di una richiesta GET al `/estimate` endpoint per visualizzare informazioni statistiche sulla definizione del segmento, tra cui la dimensione del pubblico prevista, l’intervallo di affidabilità e la deviazione standard dell’errore.

**Formato API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{PREVIEW_ID}` | Un processo di stima viene attivato solo quando viene creato un processo di anteprima e i due processi condividono lo stesso valore ID a scopo di ricerca. In particolare, questo è il `previewId` valore restituito al momento della creazione del processo di anteprima. |

**Richiesta**

La richiesta seguente recupera i risultati di un processo di stima specifico.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del processo di stima.

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | Array di oggetti che mostrano il numero di profili all’interno del segmento suddivisi per spazio dei nomi dell’identità. Il numero totale di profili per spazio dei nomi (sommando i valori mostrati per ciascuno spazio dei nomi) può essere maggiore della metrica del conteggio dei profili, perché un profilo può essere associato a più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente verranno associati più spazi dei nomi. |
| `state` | Stato corrente del processo di anteprima. Lo stato sarà &quot;RUNNING&quot; (IN ESECUZIONE) fino al completamento dell’elaborazione, che diventa &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `_links.preview` | Quando `state` è &quot;RESULT_READY&quot;, questo campo fornisce un URL per visualizzare la stima. |

## Passaggi successivi

Dopo aver letto questa guida sarai in grado di comprendere meglio come utilizzare le anteprime e le stime utilizzando l’API di segmentazione. Per informazioni su come accedere alle metriche relative ai dati Profilo cliente in tempo reale, ad esempio il numero totale di frammenti di profilo e profili uniti all’interno di spazi dei nomi specifici o all’archivio dati profilo nel suo complesso, visita il [anteprima profilo (`/previewsamplestatus`) guida dell&#39;endpoint](../../profile/api/preview-sample-status.md).
