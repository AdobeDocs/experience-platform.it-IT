---
title: Shopify Streaming Source
description: Scopri come creare una connessione di origine e un flusso di dati per acquisire i dati in streaming dall’istanza di Shopify a Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>L&#39;origine [!DNL Shopify Streaming] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Adobe Experience Platform fornisce supporto per l’acquisizione di dati da applicazioni di streaming. Il supporto per i provider di streaming include [!DNL Shopify].

## Prerequisiti {#prerequisites}

La sezione seguente illustra i passaggi prerequisiti da completare prima di utilizzare l&#39;origine [!DNL Shopify Streaming].

Per connettersi alle API [!DNL Shopify] è necessario disporre di un account partner [!DNL Shopify] valido. Se non disponi già di un account partner, registrati utilizzando il dashboard [[!DNL Shopify] partner](https://www.shopify.com/partners).

### Creare l’applicazione

Con un account partner [!DNL Shopify] valido, ora puoi procedere e creare la tua app utilizzando il dashboard dei partner. Per i passaggi completi su come creare l&#39;app in [!DNL Shopify], consulta la [[!DNL Shopify] guida introduttiva](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Una volta creata l&#39;app, recupera l&#39;**ID client** e il **segreto client** dalla scheda **credenziali client** del dashboard [!DNL Shopify] partner. L’ID client e il segreto client verranno utilizzati nei passaggi successivi per recuperare il codice di autorizzazione e il token di accesso.

### Recuperare il codice di autorizzazione

Quindi, recupera il codice di autorizzazione immettendo l&#39;URL `myshopify.com` del tuo dominio nel browser, insieme alle stringhe di query che definiscono la chiave API, gli ambiti e l&#39;URI di reindirizzamento.

Il formato di questo URL è il seguente:

**Formato API**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parametro | Descrizione |
| --- | --- |
| `shop` | URL del sottodominio `myshopify.com`. |
| `api_key` | ID client [!DNL Shopify]. Puoi recuperare l&#39;ID client dalla scheda **credenziali client** del dashboard dei partner [!DNL Shopify]. |
| `scopes` | Tipo di accesso che si desidera definire. Ad esempio, è possibile impostare gli ambiti come `scope=write_orders,read_customers` per consentire le autorizzazioni di modifica degli ordini e di lettura dei clienti. |
| `redirect_uri` | URL dello script che genererà il token di accesso. |

**Richiesta**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’URL di reindirizzamento, incluso il codice di autorizzazione necessario per generare il token di accesso.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Recuperare il token di accesso

Ora che disponi del tuo ID client, del segreto client e del codice di autorizzazione, puoi recuperare il token di accesso. Per recuperare il token di accesso, effettuare una richiesta POST all&#39;URL `myshopify.com` del dominio aggiungendo questo URL con l&#39;endpoint API [!DNL Shopify's]: `/admin/oauth/access_token`.

**Formato API**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Richiesta**

La richiesta seguente genera un token di accesso per l&#39;istanza [!DNL Shopify].

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/oauth/access_token' \
  -H 'developer-token: {DEVELOPER_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: _master_udr=xxx; request_method=POST'
  -d '{
    "client_id": "l6fiviermmzpram5i1spfub99shms3j9",
    "client_secret": "dajn3caxz9s7ti624ncyv_m4f60jnwi3ii3y3k",
    "code": "k6j2palgrbljja228ou8c20fmn7w41gz"
}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce il token di accesso e gli ambiti delle autorizzazioni.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Crea un webhook per lo streaming dei dati [!DNL Shopify] {#webhook}

I webhook consentono alle applicazioni di rimanere sincronizzate con i dati di [!DNL Shopify] o di eseguire un&#39;azione dopo che un particolare evento si è verificato in un negozio. Per lo streaming dei dati [!DNL Shopify] su Experience Platform, è possibile utilizzare i webhook per definire l&#39;endpoint http e gli argomenti per la sottoscrizione.

**Richiesta**

La richiesta seguente crea un webhook per i dati di [!DNL Shopify Streaming].

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| Parametro | Descrizione |
| --- | --- | 
| `webhook.address` | L’endpoint http in cui vengono inviati i messaggi in streaming. |
| `webhook.topic` | L’argomento dell’abbonamento al webhook. Per ulteriori informazioni, leggere la [[!DNL Shopify] guida agli argomenti dell&#39;evento webhook](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | Il formato dei dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce informazioni sul webhook, inclusi `id`, l&#39;indirizzo e altre informazioni sui metadati corrispondenti.

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "created_at": "2022-07-20T07:15:23-04:00",
    "updated_at": "2022-07-20T07:15:23-04:00",
    "format": "json",
    "fields": [],
    "metafield_namespaces": [],
    "api_version": "2021-10",
    "private_metafield_namespaces": []
  }
}
```

### Limitazioni {#limitations}

Di seguito è riportato un elenco delle limitazioni note che possono verificarsi quando si utilizzano i webhook con l&#39;origine [!DNL Shopify Streaming].

* Non è garantito che puoi organizzare l’ordine di consegna di diversi argomenti per la stessa risorsa. È ad esempio possibile che un webhook `products/update` venga recapitato prima di un webhook `products/create`.
* Puoi impostare il webhook in modo che distribuisca gli eventi del webhook a un endpoint almeno una volta. Ciò significa che un endpoint può ricevere lo stesso evento più di una volta. È possibile cercare eventi webhook duplicati confrontando l&#39;intestazione `X-Shopify-Webhook-Id` con eventi precedenti.
* [!DNL Shopify] considera le risposte allo stato HTTP 2xx come notifiche riuscite. Qualsiasi altra risposta al codice di stato è considerata un errore. [!DNL Shopify] fornisce un meccanismo di esecuzione di un nuovo tentativo per le notifiche del webhook non riuscite. Se non viene ricevuta **alcuna risposta dopo aver atteso cinque secondi**, [!DNL Shopify] ritenta la connessione **19 volte** nel corso delle **48 ore** successive. Se non sono ancora presenti risposte entro la fine del periodo di esecuzione dei nuovi tentativi, [!DNL Shopify] elimina il webhook.

## Passaggi successivi

I seguenti tutorial forniscono i passaggi per collegare l&#39;origine [!DNL Shopify Streaming] ad Experience Platform utilizzando l&#39;API e l&#39;interfaccia utente:

* [Creare una connessione e un flusso di dati di origine di Shopify Streaming utilizzando l’API del servizio Flusso](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Creare una connessione e un flusso di dati Shopify Streaming nell’interfaccia utente](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
