---
description: Questa pagina elenca e descrive i passaggi per configurare una destinazione di streaming con Destination SDK.
title: Utilizzare Destination SDK per configurare una destinazione di streaming
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 52be44ece950ee57a66a13ab7962907b2b7c0fb1
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---

# Utilizzare Destination SDK per configurare una destinazione di streaming

## Panoramica {#overview}

Questa pagina descrive come utilizzare le informazioni in [Opzioni di configurazione nell’SDK delle destinazioni](../functionality/configuration-options.md) e in altri documenti di riferimento API e funzionalità Destination SDK per configurare un [destinazione di streaming](../../destination-types.md#streaming-destinations). I passaggi sono disposti in ordine sequenziale di seguito.

## Prerequisiti {#prerequisites}

Prima di procedere con i passaggi illustrati di seguito, leggere la [Destination SDK introduzione](../getting-started.md) per informazioni su come ottenere le credenziali di autenticazione Adobe I/O necessarie e altri prerequisiti per lavorare con le API Destination SDK. Ciò presuppone che tu abbia completato i prerequisiti di partnership e autorizzazione e che sia pronto per iniziare a sviluppare la tua destinazione.

## Passaggi per utilizzare le opzioni di configurazione in Destination SDK per impostare la destinazione {#steps}

![Passaggi illustrati per l’utilizzo degli endpoint Destination SDK](../assets/guides/destination-sdk-steps.png)

## Passaggio 1: creare una configurazione di server e modelli {#create-server-template-configuration}

Inizia per [creazione di una configurazione di server e modelli](../authoring-api/destination-server/create-destination-server.md) utilizzando `/destinations-server` endpoint.

Di seguito è riportato un esempio di configurazione. Tieni presente che il modello di trasformazione dei messaggi in `requestBody.value` il parametro è trattato nel passaggio 3, [Creare un modello di trasformazione](#create-transformation-template).

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json {line-numbers="true" highlight="14"}
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

## Passaggio 2: creare la configurazione di destinazione {#create-destination-configuration}

Di seguito è riportata una configurazione di esempio per un modello di destinazione, creata utilizzando `/destinations` Endpoint API Consulta [creare una configurazione di destinazione](../authoring-api/destination-configuration/create-destination-configuration.md) per ulteriori informazioni.

Per connettere il server e la configurazione del modello nel passaggio 1 a questa configurazione di destinazione, aggiungi l’ID istanza del server e della configurazione del modello come `destinationServerId` qui.

>[!IMPORTANT]
>
>Per creare una destinazione in tempo reale (streaming) configurata correttamente, *deve* aggiungi almeno un’identità di destinazione in `identityNamespaces`, come illustrato di seguito. Se non è configurata alcuna identità di destinazione, gli utenti non potranno procedere oltre il [Passaggio di mappatura](../../ui/activate-segment-streaming-destinations.md#mapping) del workflow di attivazione.

```shell
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="74"}
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
   "audienceMetadataConfig":{
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

## Passaggio 3: creare un modello di trasformazione dei messaggi. Utilizza il linguaggio dei modelli per specificare il formato di output del messaggio {#create-transformation-template}

In base ai payload supportati dalla destinazione, è necessario creare un modello che trasformi il formato dei dati esportati dal formato XDM Adobe in un formato supportato dalla destinazione. Consulta esempi di modelli nella sezione [Utilizzo di un linguaggio per modelli per le trasformazioni di identità, attributi e appartenenza a un pubblico](../functionality/destination-server/message-format.md#using-templating) e utilizza [strumento per la creazione di modelli](../testing-api/streaming-destinations/create-template.md) fornite dall’Adobe.

Dopo aver creato un modello di trasformazione dei messaggi che funziona per te, aggiungilo al server e alla configurazione del modello creati nel passaggio 1.

```json {line-numbers="true" highlight="13-14"}
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
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"users\": [\n        {% for profile in input.profiles %}\n            {{profile|raw}}{% if not loop.last %},{% endif %}\n        {% endfor %}\n    ]\n}"
      },
      "contentType":"application/json"
   }
}
```

## Passaggio 4: creare la configurazione dei metadati del pubblico {#create-audience-metadata-configuration}

Per alcune destinazioni, Destination SDK richiede la configurazione di una configurazione di metadati di pubblico per creare, aggiornare o eliminare in modo programmatico i tipi di pubblico nella destinazione. Fai riferimento a [Gestione dei metadati del pubblico](../functionality/audience-metadata-management.md) per informazioni su quando è necessario impostare questa configurazione e su come eseguire questa operazione.

Se utilizzi una configurazione di metadati di pubblico, devi collegarla alla configurazione di destinazione creata nel passaggio 2. Aggiungi l&#39;ID istanza della configurazione dei metadati del pubblico alla configurazione di destinazione come `audienceTemplateId`.

```json {line-numbers="true" highlight="53"}
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
   "audienceMetadataConfig":{
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


## Passaggio 5: configurare l’autenticazione {#set-up-authentication}

A seconda che tu specifichi `"authenticationRule": "CUSTOMER_AUTHENTICATION"` o `"authenticationRule": "PLATFORM_AUTHENTICATION"` nella configurazione di destinazione precedente, puoi impostare l&#39;autenticazione per la destinazione utilizzando `/destination` o `/credentials` endpoint.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION` è la più comune delle due regole di autenticazione ed è quella da utilizzare se richiedi agli utenti di fornire una forma di autenticazione alla destinazione prima di poter impostare una connessione ed esportare dati.

Se hai selezionato `"authenticationRule": "CUSTOMER_AUTHENTICATION"` nella configurazione di destinazione e la destinazione supporta il metodo di autenticazione OAuth 2, leggi [Autenticazione OAuth 2](../functionality/destination-configuration/oauth2-authorization.md).

Se hai selezionato `"authenticationRule": "PLATFORM_AUTHENTICATION"`, è necessario creare un [configurazione delle credenziali](../credentials-api/create-credential-configuration.md).

## Passaggio 6: verifica della destinazione {#test-destination}

Dopo aver impostato la destinazione utilizzando gli endpoint di configurazione nei passaggi precedenti, puoi utilizzare [strumento di test di destinazione](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) per testare l’integrazione tra Adobe Experience Platform e la tua destinazione.

Come parte del processo di test della destinazione, devi utilizzare l’interfaccia utente di Experienci Platform per creare i segmenti, che attiverai nella destinazione. Per istruzioni su come creare un pubblico in Experienci Platform, consulta le due risorse seguenti:

* [Creare una pagina di documentazione del pubblico](/help/segmentation/ui/overview.md#create-segment)
* [Procedura dettagliata per la creazione di un video sul pubblico](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)

## Passaggio 7: pubblicare la destinazione {#publish-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Dopo aver configurato e testato la destinazione, utilizza [API di pubblicazione della destinazione](../publishing-api/create-publishing-request.md) per inviare la configurazione all&#39;Adobe per la revisione.

## Passaggio 8: documentare la destinazione {#document-destination}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Se si è un fornitore di software indipendente (ISV) o un integratore di sistemi (SI) che crea un [integrazione di produzione](../overview.md#productized-custom-integrations), utilizza [processo di documentazione self-service](../docs-framework/documentation-instructions.md) per creare una pagina di documentazione del prodotto per la destinazione in [catalogo delle destinazioni di Experience Platform](/help/destinations/catalog/overview.md).

## Passaggio 9: inviare la destinazione per la revisione di Adobe {#submit-for-review}

>[!NOTE]
>
>Questo passaggio non è necessario se stai creando una destinazione privata per il tuo utilizzo e non stai cercando di pubblicarla nel catalogo delle destinazioni affinché altri clienti la possano utilizzare.

Infine, prima che la destinazione possa essere pubblicata nel catalogo di Experienci Platform e visibile a tutti i clienti di Experienci Platform, devi inviare ufficialmente la destinazione per la revisione di Adobi. Informazioni complete su come [invia per la revisione una destinazione prodotta creata con Destination SDK](../guides/submit-destination.md).
