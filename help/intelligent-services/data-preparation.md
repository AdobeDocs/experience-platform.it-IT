---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Preparare i dati per l'utilizzo in Intelligent Services
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 9a2e6f7db441b804f17ec91d06d359439c3d5da5
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---


# Preparare i dati per l&#39;utilizzo in Intelligent Services

Per consentire ai servizi intelligenti di scoprire informazioni ricavate dai dati degli eventi di marketing, i dati devono essere arricchiti e mantenuti in modo semantico in una struttura standard. I servizi intelligenti sfruttano gli schemi XDM (Experience Data Model) per ottenere questo risultato. Nello specifico, tutti i set di dati utilizzati in Intelligent Services devono essere conformi allo schema XDM **Consumer ExperienceEvent (CEE)** .

Questo documento fornisce linee guida generali sulla mappatura dei dati degli eventi di marketing da più canali a questo schema, delineando le informazioni sui campi importanti all&#39;interno dello schema per consentire di determinare in modo efficace come mappare i dati alla relativa struttura.

## Riepilogo flusso di lavoro

Il processo di preparazione varia a seconda che i dati siano memorizzati in Adobe Experience Platform o esternamente. In questa sezione vengono riepilogati i passi necessari da intraprendere, in base a uno dei due scenari.

### Preparazione dati esterni

Se i dati sono memorizzati al di fuori di [!DNL Experience Platform], attenetevi alla procedura seguente:

1. Contattare Adobe Consulting Services per richiedere le credenziali di accesso per un contenitore di archiviazione BLOB di Azure dedicato.
1. Utilizzando le credenziali di accesso, caricate i dati nel contenitore BLOB.
1. Consulta Adobe Consulting Services per mappare i tuoi dati sullo schema [](#cee-schema) Consumer ExperienceEvent e trasferirli in Servizi intelligenti.

### [!DNL Experience Platform] preparazione dei dati

Se i dati sono già memorizzati in [!DNL Platform], segui i passaggi indicati di seguito:

1. Esaminare la struttura dello schema [](#cee-schema) Consumer ExperienceEvent e determinare se i dati possono essere mappati ai relativi campi.
1. Contatta i servizi di consulenza Adobe per facilitare la mappatura dei dati sullo schema e l&#39;assimilazione nei servizi intelligenti, oppure [segui i passaggi descritti in questa guida](#mapping) se vuoi mappare i dati da solo.

## Informazioni sullo schema CEE {#cee-schema}

Lo schema Consumer ExperienceEvent descrive il comportamento di un individuo in quanto si riferisce a eventi di marketing digitale (Web o mobile) nonché alle attività commerciali online o offline. L&#39;utilizzo di questo schema è richiesto per i servizi intelligenti a causa dei relativi campi (colonne) semanticamente ben definiti, evitando nomi sconosciuti che altrimenti renderebbero i dati meno chiari.

I servizi intelligenti utilizzano diversi campi chiave all&#39;interno di questo schema per generare informazioni dai dati degli eventi di marketing, che possono essere trovati a livello principale e espansi per mostrare i relativi sottocampi richiesti.

![](./images/data-preparation/schema-expansion.gif)

Come tutti gli schemi XDM, il mixin CEE è estensibile. In altre parole, è possibile aggiungere altri campi al mixin CEE, e se necessario è possibile includere diverse varianti in più schemi.

Un esempio completo del mixin può essere trovato nel repository [XDM](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)pubblico e dovrebbe essere utilizzato come riferimento per i campi chiave descritti nella sezione seguente.

## Campi chiave

Le sezioni seguenti evidenziano i campi chiave all&#39;interno del mixin CEE che dovrebbero essere utilizzati per consentire ai servizi intelligenti di generare informazioni utili, tra cui descrizioni e collegamenti alla documentazione di riferimento per ulteriori esempi.

>[!IMPORTANT] Il `xdm:channel` campo (illustrato nella prima sezione di seguito) è **richiesto** per consentire l&#39;utilizzo dei dati da parte dell&#39;AI di attribuzione, mentre l&#39;AI cliente non dispone di campi obbligatori. Tutti gli altri campi chiave sono fortemente consigliati, ma non obbligatori.

### xdm:channel

Questo campo rappresenta il canale di marketing correlato a ExperienceEvent. Il campo include informazioni sul tipo di canale, il tipo di supporto e il tipo di posizione. **Questo campo _deve_essere fornito per consentire l&#39;utilizzo dei dati** da parte di AI di attribuzione.

![](./images/data-preparation/channel.png)

**Esempio di schema**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:channel`, consultate la specifica dello schema [del canale](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) esperienza. Per alcuni esempi di mappature, vedere la [tabella seguente](#example-channels).

#### Esempio di mappature dei canali {#example-channels}

Nella tabella seguente sono riportati alcuni esempi di canali di marketing mappati allo `xdm:channel` schema:

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Ricerca pagata | https:/<span>/ns.adobe.com/xdm/channel-types/search | pagato | click |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | guadagnato | click |
| Visualizzazione | https:/<span>/ns.adobe.com/xdm/channel-types/display | pagato | click |
| E-mail | https:/<span>/ns.adobe.com/xdm/channel-types/email | pagato | click |
| Referente interno | https:/<span>/ns.adobe.com/xdm/channel-types/direct | di proprietà | click |
| VisualizzazioneTramite | https:/<span>/ns.adobe.com/xdm/channel-types/display | pagato | impressioni |
| Reindirizzamento del codice QR | https:/<span>/ns.adobe.com/xdm/channel-types/direct | di proprietà | click |
| Dispositivi mobili | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | di proprietà | click |

### xdm:productListItems

Questo campo è un array di elementi che rappresentano i prodotti selezionati da un cliente, inclusi SKU di prodotto, nome, prezzo e quantità.

![](./images/data-preparation/productListItems.png)

**Esempio di schema**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:productListItems`, fare riferimento alla specifica dello schema [dei dettagli](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) commerciali.

### xdm:commerce

Questo campo contiene informazioni commerciali specifiche sull’ExperienceEvent, compreso il numero dell’ordine di acquisto e le informazioni di pagamento.

![](./images/data-preparation/commerce.png)

**Esempio di schema**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:commerce`, fare riferimento alla specifica dello schema [dei dettagli](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) commerciali.

### xdm:web

Questo campo rappresenta i dettagli Web relativi a ExperienceEvent, ad esempio l’interazione, i dettagli della pagina e il referente.

![](./images/data-preparation/web.png)

**Esempio di schema**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:productListItems`, consulta la specifica dello schema [dei dettagli Web](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) ExperienceEvent.

### xdm:marketing

Questo campo contiene informazioni relative alle attività di marketing attive con il punto di contatto.

![](./images/data-preparation/marketing.png)

**Esempio di schema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Per informazioni complete su ciascuno dei campi secondari richiesti per `xdm:productListItems`, consulta le specifiche sechma [di](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) marketing.

## Mappatura e assimilazione dei dati (#mapping)

Una volta determinato se i dati degli eventi di marketing possono essere mappati sullo schema CEE, il passaggio successivo consiste nel determinare quali dati includere nei servizi intelligenti. Tutti i dati storici utilizzati in Intelligent Services devono rientrare nel periodo minimo di quattro mesi di dati, più il numero di giorni previsti come periodo di lookback.

Dopo aver deciso l&#39;intervallo di dati da inviare, contatta i servizi di consulenza Adobe per facilitare la mappatura dei dati sullo schema e l&#39;assimilazione nel servizio.

Se disponete di un’ [!DNL Adobe Experience Platform] iscrizione e desiderate mappare e assimilare i dati voi stessi, seguite i passaggi descritti nella sezione seguente.

### Utilizzo di Adobe Experience Platform

>[!NOTE] I passaggi seguenti richiedono un’iscrizione a Experience Platform. Se non disponete dell&#39;accesso alla piattaforma, passate alla sezione dei passaggi [](#next-steps) successivi.

In questa sezione viene illustrato il flusso di lavoro per la mappatura e l’assimilazione dei dati in Experience Platform per l’utilizzo in Intelligent Services, compresi i collegamenti alle esercitazioni per passaggi dettagliati.

#### Creare uno schema e un dataset CEE

Quando si è pronti per iniziare a preparare i dati per l&#39;assimilazione, il primo passo consiste nel creare un nuovo schema XDM che utilizzi il mixin CEE. Le seguenti esercitazioni forniscono informazioni dettagliate sul processo di creazione di un nuovo schema nell&#39;interfaccia utente o nell&#39;API:

* [Creare uno schema nell&#39;interfaccia utente](../xdm/tutorials/create-schema-ui.md)
* [Creare uno schema nell&#39;API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] Le esercitazioni riportate sopra seguono un flusso di lavoro generico per la creazione di uno schema. Quando si sceglie una classe per lo schema, è necessario utilizzare la classe **ExperienceEvent** XDM. Una volta scelta questa classe, è possibile aggiungere il mixin CEE allo schema.

Dopo aver aggiunto il mixin CEE allo schema, è possibile aggiungere altri mixin come richiesto per campi aggiuntivi all&#39;interno dei dati.

Dopo aver creato e salvato lo schema, è possibile creare un nuovo dataset basato su tale schema. Le seguenti esercitazioni forniscono informazioni dettagliate sul processo di creazione di un nuovo set di dati nell&#39;interfaccia utente o nell&#39;API:

* [Creare un set di dati nell’interfaccia](../catalog/datasets/user-guide.md#create) (seguire il flusso di lavoro per utilizzare uno schema esistente)
* [Creare un set di dati nell&#39;API](../catalog/datasets/create.md)

#### Aggiunta di un tag dello spazio dei nomi dell&#39;identità primaria al dataset

Se trasferisci dati da [!DNL Adobe Audience Manager], [!DNL Adobe Analytics]o da un&#39;altra origine esterna, devi aggiungere un `primaryIdentityNameSpace` tag al dataset. Questo può essere fatto eseguendo una richiesta PATCH all’API del servizio catalogo.

Se state acquisendo dati da un file CSV locale, potete passare alla sezione successiva sulla [mappatura e l’assimilazione dei dati](#ingest).

Prima di seguire la chiamata API di esempio riportata di seguito, consultate la sezione [](../catalog/api/getting-started.md) introduttiva nella guida per gli sviluppatori di Catalog per informazioni importanti sulle intestazioni richieste.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | ID del set di dati creato in precedenza. |

**Richiesta**

A seconda dell’origine da cui vengono acquisiti i dati, nel payload della richiesta dovete fornire valori `primaryIdentityNamespace` e `sourceConnectorId` tag appropriati.

La seguente richiesta aggiunge i valori tag appropriati per Audience Manager:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["mcid"],
          "sourceConnectorId": ["audiencemanager"],
        }
      }'
```

La seguente richiesta aggiunge i valori tag appropriati per Analytics:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["aaid"],
          "sourceConnectorId": ["analytics"],
        }
      }'
```

>[!NOTE] Per ulteriori informazioni sull&#39;utilizzo degli spazi dei nomi di identità in Piattaforma, consultate la panoramica [dello spazio dei nomi](../identity-service/namespaces.md)di identità.

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

#### Mappa e acquisizione dei dati {#ingest}

Dopo aver creato uno schema CEE e un set di dati, è possibile iniziare a mappare le tabelle di dati sullo schema e a assimilare i dati in Platform. Per informazioni su come eseguire questa operazione nell’interfaccia utente, consultate l’esercitazione sulla [mappatura di un file CSV su uno schema](../ingestion/tutorials/map-a-csv-file.md) XDM. Una volta compilato il set di dati, lo stesso set di dati può essere utilizzato per acquisire file di dati aggiuntivi.

Se i dati sono memorizzati in un&#39;applicazione di terze parti supportata, puoi anche scegliere di creare un connettore [](../sources/home.md) sorgente per trasferire in tempo reale i dati degli eventi di marketing in Piattaforma.

## Passaggi successivi {#next-steps}

Questo documento fornisce indicazioni generali sulla preparazione dei dati per l&#39;utilizzo in Intelligent Services. Se avete bisogno di consulenza aggiuntiva in base al caso d&#39;uso, contattate l&#39;Assistenza Consultiva Adobe.

Dopo aver compilato con successo un dataset con i dati sull&#39;esperienza cliente, puoi utilizzare i servizi intelligenti per generare informazioni approfondite. Per iniziare, consulta i seguenti documenti:

* [Panoramica di AI per attribuzione](./attribution-ai/overview.md)
* [Panoramica dell&#39;AI del cliente](./customer-ai/overview.md)
