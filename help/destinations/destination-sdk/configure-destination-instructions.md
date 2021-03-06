---
description: Questa pagina elenca e descrive i passaggi per configurare una destinazione di streaming utilizzando Destination SDK.
title: Utilizza Destination SDK per configurare una destinazione di streaming
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: abc9b9857e4a93a334440e855ca0ae562c695df1
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Utilizza Destination SDK per configurare una destinazione di streaming

## Panoramica {#overview}

Questa pagina descrive come utilizzare le informazioni in [Opzioni di configurazione nell’SDK delle destinazioni](./configuration-options.md) e in altri documenti di riferimento sulle funzionalità di Destination SDK e API per configurare un [destinazione streaming](/help/destinations/destination-types.md#streaming-destinations). I passaggi sono disposti in ordine sequenziale di seguito.

## Prerequisiti {#prerequisites}

Prima di passare ai passaggi illustrati di seguito, leggere il [Guida introduttiva alla Destination SDK](./getting-started.md) per informazioni su come ottenere le credenziali di autenticazione necessarie per l’Adobe I/O e altri prerequisiti per l’utilizzo con le API Destination SDK.

## Passaggi per utilizzare le opzioni di configurazione in Destination SDK per impostare la destinazione {#steps}

![Passaggi illustrativi dell’utilizzo degli endpoint Destination SDK](./assets/destination-sdk-steps.png)

## Passaggio 1: Creare una configurazione server e modello {#create-server-template-configuration}

Inizia creando un server e una configurazione di modelli utilizzando `/destinations-server` endpoint (lettura [Riferimento API](destination-server-api.md)). Per ulteriori informazioni sulla configurazione del server e del modello, consulta [Specifiche del server e del modello](server-and-template-configuration.md) nella sezione riferimento.

Di seguito è riportato un esempio di configurazione. Tieni presente che il modello di trasformazione del messaggio nel `requestBody.value` il parametro è affrontato al punto 3, [Creare un modello di trasformazione](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
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

Di seguito è riportato un esempio di configurazione per un modello di destinazione, creato utilizzando `/destinations` Endpoint API. Per ulteriori informazioni su questa configurazione, consulta [Configurazione della destinazione](./destination-configuration.md).

Per collegare la configurazione del server e del modello nel passaggio 1 a questa configurazione di destinazione, aggiungi l’ID istanza del server e la configurazione del modello come `destinationServerId` qui.

>[!IMPORTANT]
>
>Per creare una destinazione configurata correttamente, *deve* aggiungi almeno un&#39;identità di destinazione in `identityNamespaces`, come illustrato di seguito. Se non è configurata alcuna identità di destinazione, gli utenti non potranno passare oltre il [Passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di attivazione.

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
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

## Passaggio 3: Crea modello di trasformazione del messaggio: utilizza il linguaggio di template per specificare il formato di output del messaggio {#create-transformation-template}

In base ai payload supportati dalla destinazione, è necessario creare un modello che trasformi il formato dei dati esportati dal formato Adobe XDM in un formato supportato dalla destinazione. Consulta esempi di modelli nella sezione . [Utilizzo di un linguaggio di template per le trasformazioni di identità, attributi e appartenenza ai segmenti](./message-format.md#using-templating) e utilizza [strumento di creazione dei modelli](./create-template.md) fornito dall&#39;Adobe.

Dopo aver creato un modello di trasformazione del messaggio che funziona per te, aggiungilo al server e alla configurazione del modello che hai creato al passaggio 1.

## Passaggio 4: Creare la configurazione dei metadati del pubblico {#create-audience-metadata-configuration}

Per alcune destinazioni, Destination SDK richiede di configurare una configurazione di metadati del pubblico per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella destinazione. Fai riferimento a [Gestione dei metadati del pubblico](./audience-metadata-management.md) per informazioni su quando è necessario configurare questa configurazione e su come eseguirla.

Se utilizzi una configurazione di metadati del pubblico, devi connetterla alla configurazione di destinazione creata nel passaggio 2. Aggiungi l&#39;ID istanza della configurazione dei metadati del pubblico alla configurazione di destinazione come `audienceTemplateId`.

## Passaggio 5: Configurare l’autenticazione {#set-up-authentication}

A seconda se si specifica `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` nella configurazione di destinazione di cui sopra, puoi impostare l’autenticazione per la tua destinazione utilizzando `/destination` o `/credentials` punto finale.

* **Caso più comune**: Se hai selezionato `"authenticationRule": "CUSTOMER_AUTHENTICATION"` nella configurazione di destinazione e la destinazione supporta il metodo di autenticazione OAuth 2, leggere [Autenticazione OAuth 2](./oauth2-authentication.md).
* Se hai selezionato `"authenticationRule": "PLATFORM_AUTHENTICATION"`, fare riferimento alla [Configurazione dell’autenticazione](./authentication-configuration.md#when-to-use).

## Passaggio 6: Verificare la destinazione {#test-destination}

Dopo aver impostato la destinazione utilizzando gli endpoint di configurazione nei passaggi precedenti, puoi utilizzare la [strumento di prova della destinazione](./test-destination.md) per testare l’integrazione tra Adobe Experience Platform e la destinazione.

Per testare la destinazione devi usare l’interfaccia utente di Experience Platform per creare i segmenti da attivare nella destinazione. Per istruzioni su come creare segmenti in Experience Platform, consulta le due risorse seguenti:

* [Creare una pagina di documentazione sui segmenti](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Procedura dettagliata sulla creazione di un segmento](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Passaggio 7: Pubblicare la destinazione {#publish-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se crei una destinazione privata per tuo uso e non desideri pubblicarla nel catalogo delle destinazioni affinché altri clienti possano utilizzarla.

Dopo aver configurato e testato la destinazione, utilizza il [API di pubblicazione della destinazione](./destination-publish-api.md) per inviare la configurazione ad Adobe per la revisione.

## Passaggio 8: Documentare la destinazione {#document-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se crei una destinazione privata per tuo uso e non desideri pubblicarla nel catalogo delle destinazioni affinché altri clienti possano utilizzarla.

Se sei un fornitore di software indipendente (ISV) o un integratore di sistema (SI) che crea un [integrazione di prodotti](./overview.md#productized-custom-integrations), utilizza [processo di documentazione self-service](./docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto per la destinazione in [Catalogo delle destinazioni di Experience Platform](/help/destinations/catalog/overview.md).
