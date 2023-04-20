---
title: Creare una connessione sorgente di streaming e un flusso di dati per la visualizzazione di dati in modo casuale utilizzando l’API del servizio di flusso
description: Scopri come creare una connessione sorgente in streaming e un flusso di dati per Shopify data utilizzando l’API del servizio di flusso.
badge: "Beta"
hidefromtoc: y
hide: y
source-git-commit: 279d8e307c8ca5a799a47c6f903b9a082d9cf034
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 2%

---

# Creare una connessione sorgente di streaming e un flusso di dati per [!DNL Shopify] dati utilizzando l’API del servizio di flusso

>[!NOTE]
>
>La [!DNL Shopify] la sorgente in streaming è in versione beta. Per piacere, leggi le [panoramica di origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

L’esercitazione seguente fornisce passaggi su come creare una connessione sorgente di streaming e un flusso di dati per lo streaming di dati da [[!DNL Shopify]](https://www.shopify.com/) a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione {#getting-started}

Questa guida richiede una buona comprensione dei seguenti componenti dell’Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente l’acquisizione di dati da varie sorgenti e allo stesso tempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Flusso [!DNL Shopify] Dati a Platform tramite l’API del servizio di flusso

Di seguito sono descritti i passaggi da eseguire per creare una connessione sorgente e un flusso di dati per lo streaming del [!DNL Shopify] a Platform.

### Creazione di una connessione sorgente {#source-connection}

Creare una connessione sorgente effettuando una richiesta di POST al [!DNL Flow Service] API, fornendo allo stesso tempo l’ID della specifica di connessione dell’origine, dettagli quali nome e descrizione e il formato dei dati.

**Formato API**

```https
POST /sourceConnections
```

**Richiesta**

La richiesta seguente crea una connessione di origine per *GIOVANE*:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Shopify Streaming Source Connection",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Shopify Streaming Source Connection",
      "connectionSpec": {
          "id": "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione sorgente. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sulla connessione sorgente. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente alla tua origine. |
| `data.format` | Il formato del [!DNL Shopify] dati da acquisire. Attualmente, l’unico formato di dati supportato è `json`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### Creare uno schema XDM di destinazione {#target-schema}

Affinché i dati di origine possano essere utilizzati in Platform, è necessario creare uno schema di destinazione per strutturare i dati di origine in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione effettuando una richiesta POST al [API del Registro di sistema dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l’esercitazione su [creazione di uno schema tramite API](../../../../../xdm/api/schemas.md).

### Creare un set di dati di destinazione {#target-dataset}

È possibile creare un set di dati di destinazione eseguendo una richiesta di POST al [API del servizio catalogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornendo l’ID dello schema di destinazione all’interno del payload.

Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l’esercitazione su [creazione di un set di dati tramite API](../../../../../catalog/api/create-dataset.md).

### Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui devono essere memorizzati i dati acquisiti. Per creare una connessione di destinazione, è necessario fornire l’ID di specifica di connessione fissa corrispondente al data lake. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sono ora disponibili gli identificatori univoci, uno schema di destinazione, un set di dati di destinazione e l’ID delle specifiche di connessione al data lake. Utilizzando questi identificatori, puoi creare una connessione di destinazione utilizzando [!DNL Flow Service] API per specificare il set di dati che conterrà i dati di origine in entrata.

**Formato API**

```https
POST /targetConnections
```

**Richiesta**

La seguente richiesta crea una connessione di destinazione per [!DNL Shopify]:


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Shopify Streaming Target Connection",
      "description": "Shopify Streaming Target Connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "{TARGET_XDM_SCHEMA}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{TARGET_DATASET}"
      }
  }'
```


| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome della connessione di destinazione. Assicurati che il nome della connessione di destinazione sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione di destinazione. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sulla connessione di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente al data lake. Questo ID fisso è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Il formato del [!DNL Shopify] i dati che desideri inserire in Platform. |
| `params.dataSetId` | ID del set di dati di destinazione recuperato in un passaggio precedente. |


**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Questo ID è necessario nei passaggi successivi.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Creare una mappatura {#mapping}

Affinché i dati di origine possano essere acquisiti in un set di dati di destinazione, devono prima essere mappati sullo schema di destinazione a cui aderisce il set di dati di destinazione. A tal fine, esegui una richiesta POST a [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) con mappature dati definite all’interno del payload della richiesta.

**Formato API**

```http
POST /conversion/mappingSets
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "{TARGET_XDM_SCHEMA}",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `xdmSchema` | ID del [schema XDM di destinazione](#target-schema) generato in un passaggio precedente. |
| `mappings.destinationXdmPath` | Percorso XDM di destinazione in cui viene eseguito il mapping dell&#39;attributo di origine. |
| `mappings.sourceAttribute` | L&#39;attributo di origine che deve essere mappato su un percorso XDM di destinazione. |
| `mappings.identity` | Un valore booleano che indica se il set di mappatura verrà contrassegnato per [!DNL Identity Service]. |

**Risposta**

Una risposta corretta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Questo valore è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Creare un flusso {#flow}

Ultimo passo verso l&#39;inserimento dei dati [!DNL Shopify] su Platform viene creato un flusso di dati. A questo punto sono stati preparati i seguenti valori richiesti:

* [ID connessione di origine](#source-connection)
* [ID connessione di destinazione](#target-connection)
* [ID mappatura](#mapping)

Un flusso di dati è responsabile della pianificazione e della raccolta dei dati da un’origine. È possibile creare un flusso di dati eseguendo una richiesta di POST fornendo al contempo i valori precedentemente menzionati all’interno del payload.

**Formato API**

```http
POST /flows
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Shopify Streaming Dataflow",
      "description": "Shopify Streaming Dataflow",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
          "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome del flusso di dati. Assicurati che il nome del flusso di dati sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sul flusso di dati. |
| `description` | Un valore facoltativo che può essere incluso per fornire ulteriori informazioni sul flusso di dati. |
| `flowSpec.id` | ID delle specifiche di flusso necessario per creare un flusso di dati. Questo ID fisso è: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | Versione corrispondente dell’ID della specifica di flusso. Questo valore predefinito è `1.0`. |
| `sourceConnectionIds` | La [ID connessione di origine](#source-connection) generato in un passaggio precedente. |
| `targetConnectionIds` | La [ID connessione di destinazione](#target-connection) generato in un passaggio precedente. |
| `transformations` | Questa proprietà contiene le varie trasformazioni necessarie per essere applicate ai dati. Questa proprietà è necessaria per portare dati non conformi a XDM su Platform. |
| `transformations.name` | Nome assegnato alla trasformazione. |
| `transformations.params.mappingId` | La [ID mappatura](#mapping) generato in un passaggio precedente. |
| `transformations.params.mappingVersion` | Versione corrispondente dell&#39;ID di mappatura. Questo valore predefinito è `0`. |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato. Puoi utilizzare questo ID per monitorare, aggiornare o eliminare il flusso di dati.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### Ottieni l&#39;URL dell&#39;endpoint di streaming

Con il flusso di dati creato, ora puoi recuperare l’URL dell’endpoint di streaming. Utilizzerai questo URL dell’endpoint per abbonare la tua sorgente a un webhook, consentendo alla tua sorgente di comunicare con l’Experience Platform.

Per recuperare l’URL dell’endpoint di streaming, effettua una richiesta GET al `/flows` e fornisci l&#39;ID del flusso di dati.

**Formato API**

```http
GET /flows/{FLOW_ID}
```

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce informazioni sul flusso di dati, incluso l’URL dell’endpoint, contrassegnato come `inletUrl`.

```json
{
   "header":{
      "xactionId":"1658464615769:0062:161",
      "source":{
         "name":"shopify"
      },
      "sandboxId":"d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName":"prod",
      "originalTimestamp":1658464615770,
      "msgId":"1658464615769:0062:161",
      "msgVersion":"1.0",
      "traceContext":{
         "traceId":"ff3e7544618471eee6b934a4c5929d4e",
         "spanId":"74a759c5cc5f5a06",
         "isSampled":1.0
      },
      "_dcsMeta":{
         "inletId":"9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
         "authenticatedRequest":false,
         "debug":true
      }
   },
   "body":{
      "id":4135234371722,
      "admin_graphql_api_id":"gid://shopify/Order/4135234371722",
      "app_id":1354745,
      "browser_ip":null,
      "buyer_accepts_marketing":false,
      "cancel_reason":null,
      "cancelled_at":null,
      "cart_token":null,
      "checkout_id":21706716217482,
      "checkout_token":"b143503216124d50141fe0832fa3f4b0",
      "client_details":{
         "accept_language":null,
         "browser_height":null,
         "browser_ip":null,
         "browser_width":null,
         "session_hash":null,
         "user_agent":null
      },
      "closed_at":null,
      "confirmed":true,
      "contact_email":null,
      "created_at":"2022-07-22T00:36:48-04:00",
      "currency":"INR",
      "current_subtotal_price":"40000.00",
      "current_subtotal_price_set":{
         "shop_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         }
      },
      "current_total_discounts":"0.00",
      "current_total_discounts_set":{
         "shop_money":{
            "amount":"0.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"0.00",
            "currency_code":"INR"
         }
      },
      "current_total_duties_set":null,
      "current_total_price":"47200.00",
      "current_total_price_set":{
         "shop_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         }
      },
      "current_total_tax":"7200.00",
      "current_total_tax_set":{
         "shop_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         }
      },
      "customer_locale":null,
      "device_id":null,
      "discount_codes":[
          
      ],
      "email":"",
      "estimated_taxes":false,
      "financial_status":"paid",
      "fulfillment_status":null,
      "gateway":"manual",
      "landing_site":null,
      "landing_site_ref":null,
      "location_id":39129743498,
      "name":"#1005",
      "note":null,
      "note_attributes":[
          
      ],
      "number":5,
      "order_number":1005,
      "order_status_url":"https://connnectors-test.myshopify.com/31913214090/orders/ffd48198c78ef460177e44e22b19e6ab/authenticate?key=79a40d7da4b23d6a0beb2ba774f6ac83",
      "original_total_duties_set":null,
      "payment_gateway_names":[
         "manual"
      ],
      "phone":null,
      "presentment_currency":"INR",
      "processed_at":"2022-07-22T00:36:48-04:00",
      "processing_method":"manual",
      "reference":null,
      "referring_site":null,
      "source_identifier":null,
      "source_name":"shopify_draft_order",
      "source_url":null,
      "subtotal_price":"40000.00",
      "subtotal_price_set":{
         "shop_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         }
      },
      "tags":"",
      "tax_lines":[
         {
            "price":"7200.00",
            "rate":0.18,
            "title":"IGST",
            "price_set":{
               "shop_money":{
                  "amount":"7200.00",
                  "currency_code":"INR"
               },
               "presentment_money":{
                  "amount":"7200.00",
                  "currency_code":"INR"
               }
            },
            "channel_liable":false
         }
      ],
      "taxes_included":false,
      "test":false,
      "token":"ffd48198c78ef460177e44e22b19e6ab",
      "total_discounts":"0.00",
      "total_discounts_set":{
         "shop_money":{
            "amount":"0.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"0.00",
            "currency_code":"INR"
         }
      },
      "total_line_items_price":"40000.00",
      "total_line_items_price_set":{
         "shop_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         }
      },
      "total_outstanding":"0.00",
      "total_price":"47200.00",
      "total_price_set":{
         "shop_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         }
      },
      "total_price_usd":"589.95",
      "total_shipping_price_set":{
         "shop_money":{
            "amount":"0.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"0.00",
            "currency_code":"INR"
         }
      },
      "total_tax":"7200.00",
      "total_tax_set":{
         "shop_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         }
      },
      "total_tip_received":"0.00",
      "total_weight":800,
      "updated_at":"2022-07-22T00:36:49-04:00",
      "user_id":44968935562,
      "discount_applications":[
          
      ],
      "fulfillments":[
          
      ],
      "line_items":[
         {
            "id":10630730743946,
            "admin_graphql_api_id":"gid://shopify/LineItem/10630730743946",
            "fulfillable_quantity":1,
            "fulfillment_service":"manual",
            "fulfillment_status":null,
            "gift_card":false,
            "grams":800,
            "name":"Mobile Phones",
            "origin_location":{
               "id":3141069111434,
               "country_code":"IN",
               "province_code":"UP",
               "name":"Noida",
               "address1":"Noida",
               "address2":"",
               "city":"Noida",
               "zip":"201301"
            },
            "price":"40000.00",
            "price_set":{
               "shop_money":{
                  "amount":"40000.00",
                  "currency_code":"INR"
               },
               "presentment_money":{
                  "amount":"40000.00",
                  "currency_code":"INR"
               }
            },
            "product_exists":true,
            "product_id":4525859963018,
            "properties":[
                
            ],
            "quantity":1,
            "requires_shipping":true,
            "sku":"",
            "taxable":true,
            "title":"Mobile Phones",
            "total_discount":"0.00",
            "total_discount_set":{
               "shop_money":{
                  "amount":"0.00",
                  "currency_code":"INR"
               },
               "presentment_money":{
                  "amount":"0.00",
                  "currency_code":"INR"
               }
            },
            "variant_id":32045196640394,
            "variant_inventory_management":"shopify",
            "variant_title":"",
            "vendor":"Connnectors Test",
            "tax_lines":[
               {
                  "channel_liable":false,
                  "price":"7200.00",
                  "price_set":{
                     "shop_money":{
                        "amount":"7200.00",
                        "currency_code":"INR"
                     },
                     "presentment_money":{
                        "amount":"7200.00",
                        "currency_code":"INR"
                     }
                  },
                  "rate":0.18,
                  "title":"IGST"
               }
            ],
            "duties":[
                
            ],
            "discount_allocations":[
                
            ]
         }
      ],
      "payment_terms":null,
      "refunds":[
          
      ],
      "shipping_lines":[
          
      ]
   }
}
```

## Appendice

La sezione seguente fornisce informazioni sui passaggi da eseguire per monitorare, aggiornare ed eliminare il flusso di dati.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sulle esecuzioni del flusso, lo stato di completamento e gli errori. Per esempi completi sulle API, consulta la guida su [monitoraggio dei flussi di dati sorgente tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Aggiornare il flusso di dati

Aggiorna i dettagli del flusso di dati, ad esempio il nome e la descrizione, nonché la pianificazione di esecuzione e i set di mappature associati, effettuando una richiesta PATCH al `/flows` punto finale [!DNL Flow Service] , fornendo al tempo stesso l’ID del flusso di dati. Quando effettui una richiesta di PATCH, devi fornire l’univoco del flusso di dati `etag` in `If-Match` intestazione. Per esempi completi sulle API, consulta la guida su [aggiornamento dei flussi di dati di origini tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Aggiorna il tuo account

Aggiorna il nome, la descrizione e le credenziali dell&#39;account di origine effettuando una richiesta PATCH al [!DNL Flow Service] API fornendo l&#39;ID di connessione di base come parametro di query. Quando effettui una richiesta di PATCH, devi fornire l’account sorgente univoco `etag` in `If-Match` intestazione. Per esempi completi sulle API, consulta la guida su [aggiornamento dell’account sorgente tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Elimina il flusso di dati

Elimina il flusso di dati eseguendo una richiesta DELETE al [!DNL Flow Service] API fornendo l’ID del flusso di dati che desideri eliminare come parte del parametro di query. Per esempi completi sulle API, consulta la guida su [eliminazione dei flussi di dati tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Elimina l&#39;account

Elimina il tuo account eseguendo una richiesta DELETE al [!DNL Flow Service] API fornendo l’ID di connessione di base dell’account da eliminare. Per esempi completi sulle API, consulta la guida su [eliminazione dell’account sorgente tramite API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).