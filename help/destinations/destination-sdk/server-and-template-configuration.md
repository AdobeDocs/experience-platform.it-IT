---
description: Le specifiche del server e del modello possono essere configurate in Adobe Experience Platform Destination SDK tramite l'endpoint comune `/authoring/destination-servers`.
title: Opzioni di configurazione per le specifiche del server e del modello nella Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 8%

---

# Opzioni di configurazione per server di destinazioni in streaming e specifiche di modello

## Panoramica {#overview}

Le specifiche del server e del modello possono essere configurate in Adobe Experience Platform Destination SDK tramite l’endpoint comune `/authoring/destination-servers`. Leggi [Operazioni degli endpoint API delle destinazioni](./destination-server-api.md) per un elenco completo delle operazioni eseguibili sull&#39;endpoint.

## Specifiche del server {#server-specs}

![Configurazione del server evidenziata](./assets/server-configuration.png)

I clienti potranno attivare i dati da Adobe Experience Platform alla tua destinazione tramite esportazioni HTTP. La configurazione del server contiene informazioni sul server che riceve i messaggi (il server sul tuo lato).

Questo processo distribuisce i dati utente sotto forma di serie di messaggi HTTP alla piattaforma di destinazione. I parametri seguenti formano il modello delle specifiche del server HTTP.

| Parametro | Tipo | Descrizione |
|---|---|---|
| `name` | Stringa | *Obbligatorio.* Rappresenta un nome descrittivo del server, visibile solo ad Adobe. Questo nome non è visibile ai partner o clienti. Esempio `Moviestar destination server`. |
| `destinationServerType` | Stringa | *Obbligatorio.* Imposta su `URL_BASED` per le destinazioni di streaming. |
| `templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Utilizzo `PEBBLE_V1` se si utilizza una macro invece di un valore fisso nel `value` campo . Utilizza questa opzione se disponi di un endpoint come: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Utilizzo `NONE` se non è necessaria alcuna trasformazione sul lato Adobe, ad esempio se si dispone di un endpoint come: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Stringa | *Obbligatorio.* Inserisci l’indirizzo dell’endpoint API a cui Experience Platform deve connettersi. |

{style=&quot;table-layout:auto&quot;}

## Specifiche dei modelli {#template-specs}

![Configurazione del modello evidenziata](./assets/template-configuration.png)

La specifica del modello ti consente di configurare la modalità di formattazione del messaggio esportato verso la destinazione. Adobe utilizza un linguaggio modello simile a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) per trasformare i campi dallo schema XDM in un formato supportato dalla destinazione. Per ulteriori informazioni sulla trasformazione, visita i collegamenti seguenti:

* [Formato del messaggio](./message-format.md)
* [Utilizzo di un linguaggio di template per le trasformazioni di identità, attributi e appartenenza ai segmenti ](./message-format.md#using-templating)

>[!TIP]
>
>L’Adobe offre un [strumento per sviluppatori](./create-template.md) che consente di creare e testare un modello di trasformazione del messaggio.

## Configurazione di esempio di destinazione in streaming  {#example-configuration}

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

| Parametro | Tipo | Descrizione |
|---|---|---|
| `httpMethod` | Stringa | *Obbligatorio.* Il metodo che Adobe utilizzerà nelle chiamate al server. Le opzioni sono `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `value` | Stringa | *Obbligatorio.* Questa stringa è la versione con sequenza di caratteri che trasforma i dati dei clienti Platform nel formato previsto dal servizio. <br> Per informazioni su come scrivere il modello, leggere il [Utilizzo della sezione di template](./message-format.md#using-templating). <br> Per ulteriori informazioni sull&#39;escape dei caratteri, consulta la [RFC JSON standard, sezione sette](https://tools.ietf.org/html/rfc8259#section-7). <br> Per un esempio di trasformazione semplice, consulta la sezione [Attributi del profilo](./message-format.md#attributes) trasformazione. |
| `contentType` | Stringa | *Obbligatorio.* Il tipo di contenuto accettato dal server. Questo valore è più probabile `application/json`. |

{style=&quot;table-layout:auto&quot;}