---
description: Le specifiche del server e del modello possono essere configurate in Adobe Experience Platform Destination SDK tramite l’endpoint comune "/authoring/destination-servers".
title: Opzioni di configurazione per le specifiche del server e del modello in Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: a08201c4bc71b0e37202133836e9347ed4d3cd6b
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 8%

---

# Opzioni di configurazione per le specifiche del server e del modello delle destinazioni di streaming

## Panoramica {#overview}

Le specifiche del server e del modello possono essere configurate in Adobe Experience Platform Destination SDK tramite l’endpoint comune `/authoring/destination-servers`. Letto [Operazioni degli endpoint API per le destinazioni](./destination-server-api.md) per un elenco completo delle operazioni che è possibile eseguire sull&#39;endpoint.

## Specifiche del server {#server-specs}

![Configurazione server evidenziata](./assets/server-configuration.png)

I clienti potranno attivare i dati da Adobe Experience Platform alla destinazione tramite esportazioni HTTP. La configurazione del server contiene informazioni sul server che riceve i messaggi (il server sul lato dell’utente).

Questo processo distribuisce i dati utente come una serie di messaggi HTTP alla piattaforma di destinazione. I parametri seguenti costituiscono il modello delle specifiche del server HTTP.

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | *Obbligatorio.* Rappresenta un nome descrittivo del server, visibile solo agli Adobi. Questo nome non è visibile ai partner o ai clienti. Esempio `Moviestar destination server`. |
| `destinationServerType` | Stringa | *Obbligatorio.* Imposta su `URL_BASED` per le destinazioni di streaming. |
| `templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Utilizzare `PEBBLE_V1` se si utilizza una macro invece di un valore fisso nel `value` campo. Utilizza questa opzione se disponi di un endpoint come: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Utilizzare `NONE` se non è necessaria alcuna trasformazione sul lato Adobe, ad esempio se si dispone di un endpoint come: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Stringa | *Obbligatorio.* Inserisci l’indirizzo dell’endpoint API a cui l’Experience Platform deve connettersi. |

{style="table-layout:auto"}

## Specifiche modello {#template-specs}

![Configurazione modello evidenziata](./assets/template-configuration.png)

La specifica del modello consente di configurare la modalità di formattazione del messaggio esportato nella destinazione. L’Adobe utilizza un linguaggio per modelli simile a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) per trasformare i campi dallo schema XDM in un formato supportato dalla destinazione. Per ulteriori informazioni sulla trasformazione, consulta i collegamenti seguenti:

* [Formato del messaggio](./message-format.md)
* [Utilizzo di un linguaggio per modelli per le trasformazioni di identità, attributi e appartenenze a segmenti ](./message-format.md#using-templating)

>[!TIP]
>
>L’Adobe offre una [strumento per sviluppatori](./create-template.md) consente di creare e testare un modello di trasformazione dei messaggi.

## Esempio di configurazione della destinazione di streaming  {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.endpointRegion}}/items"
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

| Parametro | Tipo | Descrizione |
|---|---|---|
| `httpMethod` | Stringa | *Obbligatorio.* Il metodo che Adobe utilizzerà nelle chiamate al server. Le opzioni sono `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `value` | Stringa | *Obbligatorio.* Questa stringa è la versione con escape di carattere che trasforma i dati dei clienti di Platform nel formato previsto dal servizio. <br> Per informazioni su come scrivere il modello, leggere [Sezione Utilizzo dei modelli](./message-format.md#using-templating). <br> Per ulteriori informazioni sull’escape di caratteri, consulta [RFC JSON standard, sezione sette](https://tools.ietf.org/html/rfc8259#section-7). <br> Per un esempio di semplice trasformazione, fai riferimento a [Attributi del profilo](./message-format.md#attributes) trasformazione. |
| `contentType` | Stringa | *Obbligatorio.* Il tipo di contenuto accettato dal server. Questo valore è molto probabile `application/json`. |

{style="table-layout:auto"}