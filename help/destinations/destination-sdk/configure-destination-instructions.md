---
description: Questa pagina descrive come utilizzare le informazioni di riferimento nelle opzioni di configurazione dell’SDK per le destinazioni per configurare la destinazione utilizzando l’SDK di destinazione.
seo-description: This page describes how to use the reference information in Configuration options for the Destinations SDK to configure your destination using Destination SDK.
seo-title: How to use Destination SDK to configure your destination
title: Come utilizzare l'SDK di destinazione per configurare la destinazione
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# Come utilizzare l&#39;SDK di destinazione per configurare la destinazione

## Panoramica {#overview}

Questa pagina descrive come utilizzare le informazioni di riferimento in [Opzioni di configurazione nell&#39;SDK delle destinazioni](./configuration-options.md) per configurare la destinazione. I passaggi sono disposti in ordine sequenziale di seguito.

## Prerequisiti {#prerequisites}

Prima di passare ai passaggi descritti di seguito, leggi la pagina [Guida introduttiva all’SDK di destinazione](./getting-started.md) per informazioni su come ottenere le credenziali di autenticazione necessarie per l’Adobe I/O e altri prerequisiti per lavorare con le API SDK di destinazione.

## Passaggi per utilizzare le opzioni di configurazione nell’SDK di destinazione per impostare la destinazione {#steps}

![Passaggi illustrativi dell’utilizzo degli endpoint SDK di destinazione](./assets/destination-sdk-steps.png)

## Passaggio 1: Creare una configurazione server e modello {#create-server-template-configuration}

Inizia creando una configurazione del server e del modello utilizzando l&#39;endpoint `/destinations-server` (leggi [Riferimento API](./destination-server-api.md)). Per ulteriori informazioni sulla configurazione del server e del modello, consulta [Specifiche del server e del modello](./configuration-options.md#server-and-template) nella sezione di riferimento.

Di seguito è riportato un esempio di configurazione. Nota che il modello di trasformazione del messaggio nel parametro `requestBody.value` è indirizzato nel passaggio 3, [Crea modello di trasformazione](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{endpoint.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## Passaggio 2: Creare la configurazione di destinazione {#create-destination-configuration}

Di seguito è riportato un esempio di configurazione per un modello di destinazione, creato utilizzando l’endpoint API `/destinations`. Per ulteriori informazioni su questo modello, consulta [Configurazione di destinazione](./destination-configuration.md).

```json
POST platform.adobe.io/data/core/activation/authoring/destinations
 
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":360,
         "maxNumEventsInBatch":100
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed"
}
```

## Passaggio 3: Crea modello di trasformazione del messaggio: utilizza il linguaggio di template per specificare il formato di output del messaggio {#create-transformation-template}

In base ai payload supportati dalla destinazione, è necessario creare un modello che trasformi il formato dei dati esportati dal formato Adobe XDM in un formato supportato dalla destinazione. Consulta gli esempi di modelli nella sezione [Uso di un linguaggio di template per le trasformazioni di identità, attributi e appartenenza al segmento](./message-format.md#using-templating) e utilizza lo [strumento di creazione dei modelli](./create-template.md) fornito dall&#39;Adobe.

## Passaggio 4: Creare la configurazione dei metadati del pubblico {#create-audience-metadata-configuration}

Per alcune destinazioni, l&#39;SDK di destinazione richiede di configurare un modello di metadati per i tipi di pubblico per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella destinazione. Fai riferimento a [Gestione dei metadati del pubblico](./audience-metadata-management.md) per informazioni su quando devi configurare questa configurazione e come farlo.

## Passaggio 5: Creare la configurazione delle credenziali / Configurare l&#39;autenticazione {#set-up-authentication}

A seconda che sia stato specificato `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` nella configurazione di destinazione di cui sopra, è possibile impostare l’autenticazione per la destinazione utilizzando l’endpoint `/destination` o `/credentials`.

* **Caso** più comune: Se hai selezionato  `"authenticationRule": "CUSTOMER_AUTHENTICATION"` e la destinazione supporta il metodo di autenticazione OAuth 2, leggi l’autenticazione [ ](./oauth2-authentication.md)OAuth 2 .
* Se hai selezionato `"authenticationRule": "PLATFORM_AUTHENTICATION"`, fai riferimento a [Configurazione delle credenziali](./credentials-configuration.md) nella documentazione di riferimento.

## Passaggio 6: Verificare la destinazione {#test-destination}

Dopo aver impostato la destinazione utilizzando i modelli dei passaggi precedenti, puoi utilizzare lo [strumento di test della destinazione](./create-template.md) per testare l&#39;integrazione tra Adobe Experience Platform e la destinazione.

Per testare la destinazione devi usare l’interfaccia utente di Experience Platform per creare i segmenti da attivare nella destinazione. Per istruzioni su come creare segmenti in Experience Platform, consulta le due risorse seguenti:

* [Creare una pagina di documentazione sui segmenti](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Procedura dettagliata sulla creazione di un segmento](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)


## Passaggio 7: Pubblicare la destinazione {#publish-destination}

Dopo aver configurato e verificato la destinazione. utilizza l’ [API di pubblicazione di destinazione](./destination-publish-api.md) per inviare la configurazione ad Adobe per la revisione.

## Passaggio 8: Documentare la destinazione {#document-destination}

Se sei un fornitore indipendente di software (ISV) o un integratore di sistema (SI) che crea un&#39;integrazione di prodotto [a1/>, utilizza il [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto per la tua destinazione nel [catalogo delle destinazioni di Experience League](/help/destinations/catalog/overview.md).](./overview.md#productized-custom-integrations)