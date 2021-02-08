---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Segmentation Service;anteprime;stime;anteprime e stime;stime e anteprime;api;API;'
solution: Experience Platform
title: Anteprime e stime degli endpoint API
topic: developer guide
description: Man mano che la definizione del segmento viene sviluppata, potete utilizzare gli strumenti di stima e anteprima in Adobe Experience Platform per visualizzare le informazioni a livello di riepilogo per garantire che stiate isolando il pubblico previsto.
translation-type: tm+mt
source-git-commit: eba6de210dcbc12b829b09ba6e7083d342517ba2
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 2%

---


# Anteprime e endpoint stime

Nello sviluppo di una definizione di segmento, potete utilizzare gli strumenti di stima e anteprima in Adobe Experience Platform per visualizzare le informazioni a livello di riepilogo, in modo da garantire che l&#39;audience prevista sia isolata.

* **Le** anteprime forniscono elenchi impaginati di profili di qualifica per una definizione di segmento, consentendo di confrontare i risultati rispetto alle aspettative.

* **Le** stime forniscono informazioni statistiche su una definizione di segmento, come la dimensione dell&#39;audience proiettata, l&#39;intervallo di confidenza e la deviazione standard dell&#39;errore.

>[!NOTE]
>
>Per accedere a metriche simili correlate ai dati del profilo cliente in tempo reale, ad esempio il numero totale di frammenti di profilo e profili uniti all&#39;interno di spazi dei nomi specifici o dell&#39;archivio dei dati del profilo nel suo insieme, fare riferimento alla guida dell&#39;endpoint [profile preview (preview sample status) (guida di anteprima dello stato)](../../profile/api/preview-sample-status.md), parte della guida per gli sviluppatori dell&#39;API del profilo.

## Introduzione

Gli endpoint utilizzati in questa guida fanno parte dell&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all&#39;API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Modalità di generazione delle stime

Quando l’inserimento di record nell’archivio profili aumenta o diminuisce il conteggio totale dei profili di oltre il 5%, viene attivato un processo di campionamento per aggiornare il conteggio. Il modo in cui viene attivato il campionamento dei dati dipende dal metodo di assimilazione:

* **Caricamento batch:** Per l&#39;assimilazione batch, entro 15 minuti dal corretto inserimento di un batch nell&#39;archivio profili, se viene raggiunta la soglia di incremento o riduzione del 5%, viene eseguito un processo per aggiornare il conteggio.
* **Caricamento streaming:** Per i flussi di lavoro con dati in streaming, viene effettuato un controllo ogni ora per determinare se è stata raggiunta la soglia di aumento o riduzione del 5%. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio.

La dimensione del campione della scansione dipende dal numero complessivo di entità nell&#39;archivio profili. Queste dimensioni di campione sono rappresentate nella seguente tabella:

| Entità nell&#39;archivio profili | Dimensione del campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

>[!NOTE]
>
>Le stime impiegano generalmente dai 10 ai 15 secondi per essere eseguite, a partire da una stima approssimativa e affinando man mano che vengono letti più record.

## Creare una nuova anteprima {#create-preview}

Potete creare una nuova anteprima effettuando una richiesta di POST all&#39;endpoint `/preview`.

>[!NOTE]
>
>Quando viene creato un processo di anteprima, viene creato automaticamente un processo di stima. Questi due processi condividono lo stesso ID.

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
| `predicateModel` | Nome della classe dello schema [!DNL Experience Data Model] (XDM) su cui si basano i dati del profilo. |

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

Potete recuperare informazioni dettagliate su una specifica anteprima effettuando una richiesta di GET all&#39;endpoint `/preview` e fornendo l&#39;ID di anteprima nel percorso della richiesta.

**Formato API**

```http
GET /preview/{PREVIEW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{PREVIEW_ID}` | Il valore `previewId` dell&#39;anteprima che si desidera recuperare. |

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
| `results` | Un elenco di ID entità, con le relative identità. I collegamenti forniti possono essere utilizzati per cercare le entità specificate, utilizzando l&#39;endpoint API di accesso profilo [](../../profile/api/entities.md). |

## Recuperare i risultati di un processo di stima specifico {#get-estimate}

Dopo aver creato un processo di anteprima, potete utilizzare il relativo percorso `previewId` nel percorso di una richiesta di GET all&#39;endpoint `/estimate` per visualizzare informazioni statistiche sulla definizione del segmento, incluse le dimensioni del pubblico proiettate, l&#39;intervallo di confidenza e la deviazione standard dell&#39;errore.

**Formato API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{PREVIEW_ID}` | Un processo di stima viene attivato solo quando viene creato un processo di anteprima e i due processi condividono lo stesso valore ID a scopo di ricerca. Nello specifico, si tratta del valore `previewId` restituito al momento della creazione del processo di anteprima. |

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
| `estimatedNamespaceDistribution` | Un array di oggetti che mostra il numero di profili all&#39;interno del segmento suddivisi per namespace di identità. Il numero totale di profili per namespace (sommando insieme i valori mostrati per ogni namespace) potrebbe essere superiore alla metrica del conteggio dei profili, perché un profilo potrebbe essere associato a più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più spazi dei nomi. |
| `state` | Stato corrente del processo di anteprima. Lo stato sarà &quot;ESECUZIONE&quot; finché l&#39;elaborazione non viene completata, al punto che diventa &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `_links.preview` | Quando il valore `state` è &quot;RESULT_READY&quot;, questo campo fornisce un URL per visualizzare la stima. |

## Passaggi successivi

Dopo aver letto questa guida è necessario avere una migliore comprensione di come lavorare con le anteprime e le stime utilizzando l&#39;API di segmentazione. Per informazioni su come accedere alle metriche correlate ai dati del profilo cliente in tempo reale, ad esempio il numero totale di frammenti di profilo e di profili uniti all&#39;interno di spazi dei nomi specifici o dell&#39;archivio dati del profilo nel suo insieme, visita la [guida dell&#39;endpoint Anteprima profilo (`/previewsamplestatus`)](../../profile/api/preview-sample-status.md).