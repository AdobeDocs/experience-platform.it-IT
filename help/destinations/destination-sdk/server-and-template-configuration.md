---
description: Le specifiche del server e del modello possono essere configurate in Adobe Experience Platform Destination SDK tramite l'endpoint comune `/authoring/destination-servers`.
title: Opzioni di configurazione per le specifiche del server e del modello nell’SDK di destinazione
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 9%

---

# Opzioni di configurazione per le specifiche del server e del modello

## Panoramica {#overview}

Le specifiche del server e del modello possono essere configurate in Adobe Experience Platform Destination SDK tramite l&#39;endpoint comune `/authoring/destination-servers`. Leggi [Operazioni endpoint API delle destinazioni](./destination-server-api.md) per un elenco completo delle operazioni che puoi eseguire sull&#39;endpoint.

## Esempio di configurazione {#example-configuration}

```json
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
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## Specifiche del server {#server-specs}

![Configurazione del server evidenziata](./assets/server-configuration.png)

I clienti potranno attivare i dati da Adobe Experience Platform alla tua destinazione tramite esportazioni HTTP. La configurazione del server contiene informazioni sul server che riceve i messaggi (il server sul tuo lato).

Questo processo distribuisce i dati utente sotto forma di serie di messaggi HTTP alla piattaforma di destinazione. I parametri seguenti formano il modello delle specifiche del server HTTP.

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | *Obbligatorio.* Rappresenta un nome descrittivo del server, visibile solo ad Adobe. Questo nome non è visibile ai partner o clienti. Esempio `Moviestar destination server`. |
| `destinationServerType` | Stringa | *Obbligatorio.* `URL_BASED` al momento è l’unica opzione disponibile. |
| `templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Utilizza `PEBBLE_V1` se l&#39;Adobe deve trasformare l&#39;URL nel campo `value` sottostante. Utilizza questa opzione se disponi di un endpoint come: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Utilizza `NONE` se non è necessaria alcuna trasformazione sul lato Adobe, ad esempio se disponi di un endpoint come: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Stringa | *Obbligatorio.* Inserisci l’indirizzo dell’endpoint API a cui Experience Platform deve connettersi. |

{style=&quot;table-layout:auto&quot;}

<!--

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |
|`httpMethod` | String | The method that Adobe will use in calls to your server. Options are `GET`, `PUT`, `POST`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD`. |
|`contentType` | String | Defines how to structure the content sent to your servers. Supported options are JSON and XML. |

-->

## Specifiche dei modelli {#template-specs}

![Configurazione del modello evidenziata](./assets/template-configuration.png)

La specifica del modello ti consente di configurare la modalità di formattazione del messaggio esportato verso la destinazione. Adobe utilizza un linguaggio di template simile a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) per trasformare i campi dallo schema XDM in un formato supportato dalla destinazione. Per ulteriori informazioni sulla trasformazione, visita i collegamenti seguenti:

* [Formato del messaggio](./message-format.md)
* [Utilizzo di un linguaggio di template per le trasformazioni di identità, attributi e appartenenza ai segmenti ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe offre uno [strumento per sviluppatori](./create-template.md) che consente di creare e testare un modello di trasformazione dei messaggi.

| Parametro | Tipo | Descrizione |
|---|---|---|
| `httpMethod` | Stringa | *Obbligatorio.* Il metodo che Adobe utilizzerà nelle chiamate al server. Le opzioni sono `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `value` | Stringa | *Obbligatorio.* Questa stringa è la versione con sequenza di caratteri che trasforma i dati dei clienti Platform nel formato previsto dal servizio. <br> Per informazioni su come scrivere il modello, consulta la sezione  [Utilizzo del modello](./message-format.md#using-templating). <br> Per ulteriori informazioni sull’escape dei caratteri, consulta la sezione sette dello standard  [RFC JSON](https://tools.ietf.org/html/rfc8259#section-7). <br> Per un esempio di trasformazione semplice, consulta  [Profile ](./message-format.md#attributes) Attributestransformation (Attribuzione profilo). |
| `contentType` | Stringa | *Obbligatorio.* Il tipo di contenuto accettato dal server. Questo valore è molto probabilmente `application/json`. |

{style=&quot;table-layout:auto&quot;}

<!--

|`requestBody` | String | The request body contains the data exported from Real-time CDP, activated to your destination. <br> We need to know which data format macros your destination should support. See [Outbound Template Macros](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-template-macros.html) and [Outbound Macro Examples](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-macro-examples.html) for examples from Adobe's DMP, Audience Manager. <br> See also, [Message format](#message-format) for further information.  |
|`queryParameters` | String | Request parameters defined as macros. See above.|



<br>&nbsp;

#### Example

A valid HTTP specs template could look like below:

```

{
  "name": "ACME company HTTP template",
  "type": "HTTP", 
  "httpTemplate": {
    "httpMethod": "POST",
    "requestBody": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "queryParameters": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "contentType": "JSON"
  }
}

```

// commenting out this part as these types of destination specs are not supported in phase one

### File specifications

File-based destinations deliver file exports containing segment qualifications and profile attributes to your preferred storage location. If you want to set up a batch file-based destination, the template we'll use will be as below:

## Server specs

The server configuration contains information about the server receiving the messages (the server on your side). 
Adobe Real-time CDP currently supports three types of server configurations:
* URL
* File-based SFTP
* File-based S3

For URL destinations, you would provide us your server's information, for File-based SFTP and File-based S3 you would provide information as to the storage locations where files should be delivered.
Provide us the necessary information about your server or storage locations, as shown in the sections below.


**urlBasedDestination**

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |


// commenting out this part as these types of destination specs are not supported in phase one

**SFTP Destinations**

For FTP destinations, we need the protocol details below:

Parameter | Type | 
---------|----------|
 hostname | String | 
 port | integer | 
 rootDirectory | String | 
 moveToWhenCompleted | integer | 
 tmpFileRename | integer | 
 encryptionMode | String |
 filenameSuffix | String | 

**Amazon S3 Destinations**

For Amazon S3 destinations, we need the protocol details below:

Parameter | Description | 
---------|----------|
 bucket | Your Amazon S3 bucket name | 
 path | Your Amazon S3 bucket path | 

-->
