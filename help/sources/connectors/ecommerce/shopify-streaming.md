---
title: Sorgente in streaming ridotta
description: Scopri come creare una connessione sorgente e un flusso di dati per acquisire i dati in streaming dalla tua istanza Shopify su Adobe Experience Platform
badge: Beta
exl-id: 4c83c08d-c744-4167-9e3b-ed9a995943f4
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>La [!DNL Shopify Streaming] la sorgente è in versione beta. Per piacere, leggi le [panoramica di origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Adobe Experience Platform supporta l’acquisizione di dati da applicazioni di streaming. Il supporto per i provider di streaming include [!DNL Shopify].

## Prerequisiti {#prerequisites}

La sezione seguente illustra i passaggi preliminari da completare prima di utilizzare [!DNL Shopify Streaming] sorgente.

È necessario disporre di un [!DNL Shopify] account partner per connettersi al [!DNL Shopify] API. Se non disponi già di un account partner, registrati utilizzando [[!DNL Shopify] dashboard dei partner](https://www.shopify.com/partners).

### Creare l&#39;applicazione

Con un valore valido [!DNL Shopify] account partner, ora puoi procedere e creare l’app utilizzando il dashboard partner. Per passaggi completi su come creare l’app in [!DNL Shopify], leggi [[!DNL Shopify] guida introduttiva](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Una volta creata l’app, recupera la **ID client** e **segreto client** dal **credenziali client** della scheda [!DNL Shopify] dashboard partner. L’ID client e il segreto client verranno utilizzati nei passaggi successivi per recuperare il codice di autorizzazione e il token di accesso.

### Recupera il codice di autorizzazione

Quindi, recupera il codice di autorizzazione inserendo il dominio `myshopify.com` URL nel browser, insieme a stringhe di query che definiscono la chiave API, gli ambiti e l’URI di reindirizzamento.

Il formato di questo URL è il seguente:

**Formato API**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parametro | Descrizione |
| --- | --- |
| `shop` | Il sottodominio `myshopify.com` URL. |
| `api_key` | Le [!DNL Shopify] ID client. Puoi recuperare l’ID client da **credenziali client** della scheda [!DNL Shopify] dashboard partner. |
| `scopes` | Tipo di accesso da definire. Ad esempio, puoi impostare gli ambiti come `scope=write_orders,read_customers` per consentire le autorizzazioni per modificare gli ordini e leggere i clienti. |
| `redirect_uri` | URL per lo script che genererà il token di accesso. |

**Richiesta**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Risposta**

Una risposta corretta restituisce l’URL di reindirizzamento, incluso il codice di autorizzazione necessario per generare il token di accesso.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Recupera il token di accesso

Ora che disponi del tuo ID client, del segreto client e del codice di autorizzazione, puoi recuperare il token di accesso. Per recuperare il token di accesso, effettua una richiesta POST al dominio `myshopify.com` URL durante l’aggiunta di questo URL con [!DNL Shopify's] Endpoint API: `/admin/oauth/access_token`.

**Formato API**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Richiesta**

La seguente richiesta genera un token di accesso per il tuo [!DNL Shopify] istanza.

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

Una risposta corretta restituisce il token di accesso e gli ambiti delle autorizzazioni.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Crea un webhook per lo streaming [!DNL Shopify] dati {#webhook}

I webhook consentono alle applicazioni di rimanere sincronizzati con i [!DNL Shopify] o eseguire un&#39;azione dopo che un particolare evento si verifica in un negozio. Per lo streaming [!DNL Shopify] ad Experience Platform, i webhook possono essere utilizzati per definire l’endpoint http e gli argomenti per la sottoscrizione.

**Richiesta**

La seguente richiesta crea un webhook per il tuo [!DNL Shopify Streaming] dati.

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
| `webhook.topic` | L&#39;argomento del tuo abbonamento a webhook. Per ulteriori informazioni, consulta la sezione [[!DNL Shopify] guida agli argomenti dell&#39;evento webhook](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | Il formato dei dati. |

**Risposta**

Una risposta corretta restituisce informazioni sul webhook, incluso il corrispondente `id`, indirizzo e altre informazioni di metadati.

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

### Limitazioni  {#limitations}

Di seguito è riportato un elenco delle limitazioni note che si possono incontrare quando si utilizzano i webhook con [!DNL Shopify Streaming] sorgente.

* Non è garantito che sia possibile organizzare l’ordine di consegna di diversi argomenti per la stessa risorsa. Ad esempio, è possibile che un `products/update` il webhook viene consegnato prima di un `products/create` gancio.
* Puoi impostare il tuo webhook per consegnare eventi webhook a un endpoint almeno una volta. Ciò significa che un endpoint potrebbe ricevere lo stesso evento più di una volta. Puoi cercare eventi webhook duplicati confrontando `X-Shopify-Webhook-Id` intestazione degli eventi precedenti.
* [!DNL Shopify] considera le risposte allo stato di HTTP 2xx come notifiche di successo. Qualsiasi altra risposta del codice di stato viene considerata un errore. [!DNL Shopify] fornisce un meccanismo di esecuzione di un nuovo tentativo per le notifiche webhook non riuscite. Se esiste **nessuna risposta dopo cinque secondi di attesa**, [!DNL Shopify] prova nuovamente la connessione **19 volte** nel corso del successivo **48 ore**. Se non vi sono ancora risposte entro la fine del periodo di esecuzione dei nuovi tentativi, allora [!DNL Shopify] elimina il webhook.

## Passaggi successivi

Le seguenti esercitazioni forniscono passaggi su come collegare i [!DNL Shopify Streaming] da sorgente ad Experience Platform utilizzando l’API e l’interfaccia utente:

* [Creare una connessione sorgente e un flusso di dati Shopify Streaming utilizzando l’API del servizio di flusso](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Creare una connessione sorgente e un flusso di dati Shopify Streaming nell&#39;interfaccia utente](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
