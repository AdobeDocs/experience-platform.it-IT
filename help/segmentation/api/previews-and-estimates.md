---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;anteprime;stime;anteprime e stime;stime e anteprime;api;API;
solution: Experience Platform
title: Anteprime e stime degli endpoint API
topic-legacy: developer guide
description: Man mano che vengono sviluppate le definizioni dei segmenti, puoi utilizzare gli strumenti di stima e anteprima all’interno di Adobe Experience Platform per visualizzare le informazioni a livello di riepilogo per assicurarti di isolare il pubblico previsto.
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 2%

---

# Anteprime e stime degli endpoint

Quando si sviluppa una definizione di segmento, è possibile utilizzare gli strumenti di stima e anteprima all’interno di Adobe Experience Platform per visualizzare informazioni a livello di riepilogo per assicurarsi di isolare il pubblico previsto.

* **Anteprime** fornisce elenchi impaginati di profili qualificati per una definizione di segmento, che consentono di confrontare i risultati rispetto alle aspettative.

* **Stime** fornisce informazioni statistiche su una definizione di segmento, ad esempio la dimensione del pubblico, l’intervallo di affidabilità e la deviazione standard dell’errore proiettati.

>[!NOTE]
>
>Per accedere a metriche simili correlate ai dati del Profilo cliente in tempo reale, ad esempio il numero totale di frammenti di profilo e profili uniti in spazi dei nomi specifici o nell’archivio dati del profilo nel suo complesso, consulta [guida all’anteprima del profilo (stato dell’esempio di anteprima) dell’endpoint](../../profile/api/preview-sample-status.md), parte della guida per gli sviluppatori dell’API di profilo.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Generazione delle stime

Quando l’acquisizione dei record nell’archivio profili aumenta o diminuisce il conteggio totale dei profili di oltre il 5%, viene attivato un processo di campionamento per aggiornare il conteggio. Il modo in cui viene attivato il campionamento dei dati dipende dal metodo di acquisizione:

* **Acquisizione batch:** Per l’acquisizione batch, entro 15 minuti dal corretto inserimento di un batch nell’archivio profili, se viene soddisfatta la soglia di aumento o diminuzione del 5%, viene eseguito un processo per aggiornare il conteggio.
* **Acquisizione in streaming:** Per i flussi di lavoro con dati in streaming, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o diminuzione del 5% è stata soddisfatta. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio.

La dimensione del campione della scansione dipende dal numero complessivo di entità nell’archivio dei profili. Le dimensioni dei campioni sono rappresentate nella tabella seguente:

| Entità nell’archivio profili | Dimensione del campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

>[!NOTE]
>
>Le stime richiedono generalmente dai 10 ai 15 secondi per essere eseguite, a partire da una stima approssimativa e affinando man mano che vengono letti più record.

## Creare una nuova anteprima {#create-preview}

Puoi creare una nuova anteprima effettuando una richiesta di POST al `/preview` punto finale.

>[!NOTE]
>
>Un processo di stima viene creato automaticamente quando viene creato un processo di anteprima. Questi due processi condivideranno lo stesso ID.

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
| `predicateExpression` | Espressione PQL per eseguire una query dei dati. |
| `predicateType` | Il tipo di predicato per l&#39;espressione di query in `predicateExpression`. Attualmente, l&#39;unico valore accettato per questa proprietà è `pql/text`. |
| `predicateModel` | Nome della [!DNL Experience Data Model] (XDM) classe schema su cui si basano i dati del profilo. |
| `graphType` | Il tipo di grafico da cui si desidera ottenere il cluster. I valori supportati sono `none` (non esegue alcuna unione di identità) e `pdg` (esegue le unione delle identità in base al grafico di identità privata). |

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
| `state` | Lo stato corrente del processo di anteprima. Quando viene creato inizialmente, lo stato sarà &quot;NEW&quot;. Successivamente, sarà in stato &quot;RUNNING&quot; fino al completamento dell&#39;elaborazione, al punto in cui diventa &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `previewId` | ID del processo di anteprima, da utilizzare a scopo di ricerca quando si visualizza una stima o un’anteprima, come descritto nella sezione successiva. |

## Recupera i risultati di un’anteprima specifica {#get-preview}

Puoi recuperare informazioni dettagliate su un&#39;anteprima specifica effettuando una richiesta di GET al `/preview` e fornisce l&#39;ID di anteprima nel percorso della richiesta.

**Formato API**

```http
GET /preview/{PREVIEW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{PREVIEW_ID}` | La `previewId` valore dell&#39;anteprima da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `results` | Elenco degli ID entità e delle relative identità. I collegamenti forniti possono essere utilizzati per cercare le entità specificate, utilizzando [endpoint API di accesso profilo](../../profile/api/entities.md). |

## Recupera i risultati di un processo di stima specifico {#get-estimate}

Dopo aver creato un processo di anteprima, puoi utilizzare la relativa `previewId` nel percorso di una richiesta di GET al `/estimate` per visualizzare informazioni statistiche sulla definizione del segmento, tra cui dimensioni del pubblico proiettate, intervallo di affidabilità e deviazione standard di errore.

**Formato API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{PREVIEW_ID}` | Un processo di stima viene attivato solo quando viene creato un processo di anteprima e i due lavori condividono lo stesso valore ID a scopo di ricerca. In particolare, questa è la `previewId` restituito quando è stato creato il processo di anteprima. |

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

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli del processo di stima.

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
| `estimatedNamespaceDistribution` | Matrice di oggetti che mostra il numero di profili all’interno del segmento suddivisi per namespace di identità. Il numero totale di profili per namespace (aggiunta insieme dei valori mostrati per ogni namespace) può essere maggiore della metrica di conteggio dei profili, perché un profilo può essere associato a più namespace. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più namespace. |
| `state` | Lo stato corrente del processo di anteprima. Lo stato sarà &quot;IN ESECUZIONE&quot; fino al completamento dell&#39;elaborazione, al punto in cui diventa &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `_links.preview` | Quando il `state` è &quot;RESULT_READY&quot;, questo campo fornisce un URL per visualizzare la stima. |

## Passaggi successivi

Dopo aver letto questa guida dovresti avere una migliore comprensione di come lavorare con le anteprime e le stime utilizzando l’API di segmentazione. Per informazioni su come accedere alle metriche correlate ai dati del Profilo cliente in tempo reale, ad esempio il numero totale di frammenti di profilo e profili uniti in spazi dei nomi specifici o nell’archivio dati del profilo nel suo complesso, visita il [anteprima profilo (`/previewsamplestatus`a) guida endpoint](../../profile/api/preview-sample-status.md).
