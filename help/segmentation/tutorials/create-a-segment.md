---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creazione di un segmento
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 2%

---


# Creazione di un segmento

Questo documento fornisce un&#39;esercitazione per lo sviluppo, il test, la visualizzazione in anteprima e il salvataggio di una definizione di segmento mediante l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)Segmentazione.

Per informazioni su come creare segmenti utilizzando l’interfaccia utente, consulta la guida [di](../ui/overview.md)Segment Builder (Generatore di segmenti).

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei vari servizi di Adobe Experience Platform  coinvolti nella creazione di segmenti di pubblico. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [servizio](../home.md)di segmentazione Adobe Experience Platform: Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
- [Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API Platform.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Sviluppo di una definizione di segmento

Il primo passo nella segmentazione consiste nel definire un segmento, rappresentato in un costrutto chiamato definizione **di** segmento. Una definizione di segmento è un oggetto che racchiude una query scritta in Profile Query Language (PQL). Questo oggetto è anche denominato predicato **PQL**. I predicati PQL definiscono le regole per il segmento in base alle condizioni relative a qualsiasi record o dati delle serie temporali forniti al profilo cliente in tempo reale. Per ulteriori informazioni sulla scrittura di query PQL, consultate la guida [](../pql/overview.md) PQL.

Puoi creare una nuova definizione del segmento effettuando una richiesta POST all’ `/segment/definitions` endpoint nell’API Profilo cliente in tempo reale. L&#39;esempio seguente illustra come formattare una richiesta di definizione, incluse le informazioni necessarie per definire correttamente un segmento.

Le definizioni dei segmenti possono essere valutate in due modi: segmentazione batch e segmentazione in streaming. La segmentazione in batch valuta i segmenti in base a una pianificazione preimpostata o quando la valutazione viene attivata manualmente, mentre la segmentazione in streaming valuta i segmenti non appena i dati vengono acquisiti in Platform. Questa esercitazione utilizzerà la segmentazione **batch**. Per ulteriori informazioni sulla segmentazione in streaming, consultate la [panoramica sulla segmentazione](../api/streaming-segmentation.md)in streaming.

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

La richiesta seguente crea una nuova definizione di segmento per uno schema denominato &quot;MyProfile&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "My Sample Cart Abandons Segment Definition",
        "schema": {
            "name": "MyProfile",
        },
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "xEvent.metrics.commerce.abandons.value > 0",
        },
        "mergePolicyId": "mpid1",
        "description": "This Segment represents those users who have abandoned a cart"
    }'
```

| Proprietà | Descrizione |
| --------- | ------------ | 
| `name` | **Obbligatorio.** Un nome univoco con cui fare riferimento al segmento. |
| `schema` | **Obbligatorio.** Schema associato alle entità nel segmento. È costituito da un campo `id` o `name` . |
| `expression` | **Obbligatorio.** Entità che contiene informazioni sui campi relativi alla definizione del segmento. |
| `expression.type` | Specifica il tipo di espressione. Attualmente, è supportato solo &quot;PQL&quot;. |
| `expression.format` | Indica la struttura dell&#39;espressione in valore. Attualmente è supportato il seguente formato: <ul><li>`pql/text`: Una rappresentazione testuale di una definizione di segmento, in base alla grammatica PQL pubblicata.  Ad esempio, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Un&#39;espressione conforme al tipo indicato in `expression.format`. |
| `mergePolicyId` | Identificatore del criterio di unione da utilizzare per i dati esportati. Per ulteriori informazioni, consultare il documento [di configurazione del criterio di](../../profile/api/merge-policies.md)unione. |
| `description` | Una descrizione leggibile dell&#39;espressione. |

**Risposta**

Una risposta corretta restituisce i dettagli della definizione del segmento appena creata, inclusa la definizione di sola lettura generata dal sistema, `id` che verrà utilizzata più avanti in questa esercitazione.

```json
{
    "id": "1234",
    "name": "My Sample Cart Abandons Segment Definition",
    "description": "This Segment represents those users who have abandoned a cart",
    "type": "PQL",
    "format": "pql/text",
    "expression": "xEvent.metrics.commerce.abandons.value > 0",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/core/ups/segment/definitions/1234"
        }
    }
}
```

## Stima e anteprima di un&#39;audience {#estimate-and-preview-an-audience}

Mentre sviluppate la definizione del segmento, potete utilizzare gli strumenti di stima e anteprima nel profilo cliente in tempo reale per visualizzare le informazioni a livello di riepilogo per garantire che stiate isolando il pubblico previsto. Le stime forniscono informazioni statistiche sulla definizione di un segmento, come la dimensione dell&#39;audience e l&#39;intervallo di confidenza proiettati. Le anteprime forniscono elenchi impaginati di profili di qualifica per una definizione di segmento, consentendo di confrontare i risultati con quanto previsto.

Stimando e visualizzando in anteprima il pubblico, potete sottoporre a test e ottimizzare i predicati PQL fino a ottenere un risultato desiderato, da cui poi utilizzarli in una definizione aggiornata del segmento.

Sono necessari due passaggi per visualizzare l’anteprima o ottenere una stima del segmento:

1. [Creare un processo di anteprima](#create-a-preview-job)
2. [Visualizzare la stima o l’anteprima](#view-an-estimate-or-preview) utilizzando l’ID del processo di anteprima

### Modalità di generazione delle stime

Gli esempi di dati vengono utilizzati per valutare i segmenti e stimare il numero di profili di qualifica. I nuovi dati vengono caricati in memoria ogni mattina (tra le 12AM-2AM PT, che è 7-9AM UTC), e tutte le query di segmentazione sono stimate utilizzando i dati di esempio di quel giorno. Di conseguenza, eventuali nuovi campi aggiunti o dati aggiuntivi raccolti saranno riportati nelle stime il giorno successivo.

La dimensione del campione dipende dal numero complessivo di entità nell&#39;archivio profili. Queste dimensioni di campione sono rappresentate nella seguente tabella:

| Entità nell&#39;archivio profili | Dimensione del campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

Le stime generalmente vengono eseguite su un periodo di 10-15 secondi, a partire da una stima approssimativa e con un perfezionamento man mano che vengono letti più record.

### Creare un processo di anteprima

Potete creare un nuovo processo di anteprima effettuando una richiesta POST all’ `/preview` endpoint.

**Formato API**

```http
POST /preview
```

**Richiesta**

La richiesta seguente crea un nuovo processo di anteprima. Il corpo della richiesta contiene le informazioni sulla query relative al segmento.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "simple",
        "mergeStrategy": "simple"
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `predicateExpression` | Espressione PQL per eseguire una query sui dati. |
| `predicateModel` | Nome dello schema XDM su cui si basano i dati del profilo. |

**Risposta**

Una risposta corretta restituisce i dettagli del processo di anteprima appena creato, incluso l’ID e lo stato di elaborazione corrente.

```json
{
   "state": "RUNNING",
   "previewQueryId": "4a45e853-ac91-4bb7-a426-150937b6af5c",
   "previewQueryStatus": "RUNNING",
   "previewId": "MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg",
   "previewExecutionId": 42
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `state` | Stato corrente del processo di anteprima. Sarà in stato &quot;RUNNING&quot; fino al completamento dell&#39;elaborazione, al punto in cui diventa &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `previewId` | L’ID del processo di anteprima, da utilizzare a scopo di ricerca quando si visualizza una stima o un’anteprima, come indicato nella sezione seguente. |

### Visualizzare una stima o un&#39;anteprima

I processi di stima e anteprima vengono eseguiti in modo asincrono, in quanto le diverse query possono richiedere diversi tempi di completamento. Una volta avviata la query, potete utilizzare le chiamate API per recuperare (GET) lo stato corrente della stima o dell&#39;anteprima mentre progredisce.

Utilizzando l’API Profilo cliente in tempo reale, potete cercare lo stato corrente di un processo di anteprima in base al relativo ID. Se lo stato è &quot;RESULT_READY&quot;, è possibile visualizzare i risultati. A seconda se si desidera visualizzare una stima o un&#39;anteprima, ciascuna ha un proprio endpoint nell&#39;API. Di seguito sono riportati alcuni esempi per entrambi.

### Visualizzare una stima

**Formato API**

```http
GET /estimate/{PREVIEW_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{PREVIEW_ID}` | ID del processo di anteprima che si desidera visualizzare. |

**Richiesta**

La richiesta seguente recupera una stima, utilizzando la stima `previewId` creata nel passaggio precedente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della stima.

```json
{
    "estimatedSize": 45,
    "state": "RESULT_READY",
    "profilesReadSoFar": 83834,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 46,
    "totalRows": 82473,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview?previewQueryId=f88bc056-ee48-40d5-9ddb-8865d7d6a0e0"
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `state` | Stato corrente del processo di anteprima. Sarà &quot;IN ESECUZIONE&quot; fino al completamento dell&#39;elaborazione, al punto in cui diventa &quot;RESULT_READY&quot; o &quot;FAILED&quot;. |
| `_links.preview` | Quando lo stato corrente del processo di anteprima è &quot;RESULT_READY&quot;, questo attributo fornisce un URL per visualizzare la stima. |

### Visualizzare un’anteprima

**Formato API**

```http
GET /preview/{PREVIEW_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{PREVIEW_ID}` | ID del processo di anteprima che si desidera visualizzare. |

**Richiesta**

La richiesta seguente recupera un&#39;anteprima, utilizzando la procedura `previewId` creata nel passaggio precedente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli dell’anteprima.

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
      }
   ],
   "page": {
      "offset": 0,
      "size": 3
   }
}
```

## Passaggi successivi

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi creare un processo di segmento per creare un pubblico utilizzando l’API Profilo cliente in tempo reale. Per informazioni dettagliate su come [valutare e accedere ai risultati](./evaluate-a-segment.md) del segmento, consulta l’esercitazione.