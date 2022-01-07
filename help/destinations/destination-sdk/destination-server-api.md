---
description: Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando l'endpoint API `/authoring/destination-servers`. Le specifiche del server e del modello per la destinazione possono essere configurate in Adobe Experience Platform Destination SDK tramite l'endpoint comune `/authoring/destination-servers`.
title: Operazioni API dell’endpoint server di destinazione
exl-id: a144b0fb-d34f-42d1-912b-8576296e59d2
source-git-commit: 6dd8a94e46b9bee6d1407e7ec945a722d8d7ecdb
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 6%

---

# Operazioni API dell’endpoint server di destinazione

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando `/authoring/destination-servers` Endpoint API. Le specifiche del server e del modello per la destinazione possono essere configurate in Adobe Experience Platform Destination SDK tramite l’endpoint comune `/authoring/destination-servers`. Per una descrizione della funzionalità fornita da questo endpoint, leggere [specifiche del server e del modello](./server-and-template-configuration.md).

## Guida introduttiva alle operazioni API del server di destinazione {#get-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Creare una configurazione per un server di destinazione {#create}

Puoi creare una nuova configurazione del server di destinazione effettuando una richiesta di POST al `/authoring/destination-servers` punto finale.

**Formato API**


```http
POST /authoring/destination-servers
```

**Richiesta**

La richiesta seguente crea una nuova configurazione del server di destinazione, configurata dai parametri forniti nel payload. Il payload seguente include tutti i parametri accettati dal `/authoring/destination-servers` punto finale. Non è necessario aggiungere tutti i parametri alla chiamata e il modello è personalizzabile, in base ai requisiti API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
| -------- | ----------- | ----------- |
| `name` | Stringa | *Obbligatorio.* Rappresenta un nome descrittivo del server, visibile solo ad Adobe. Questo nome non è visibile ai partner o clienti. Esempio `Moviestar destination server`. |
| `destinationServerType` | Stringa | *Obbligatorio.* `URL_BASED` al momento è l’unica opzione disponibile. |
| `urlBasedDestination.url.templatingStrategy` | Stringa | *Obbligatorio.* <ul><li>Utilizzo `PEBBLE_V1` se Adobe deve trasformare l’URL nel `value` campo sottostante. Utilizza questa opzione se disponi di un endpoint come: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Utilizzo `NONE` se non è necessaria alcuna trasformazione sul lato Adobe, ad esempio se si dispone di un endpoint come: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Stringa | *Obbligatorio.* Inserisci l’indirizzo dell’endpoint API a cui Experience Platform deve connettersi. |
| `httpTemplate.httpMethod` | Stringa | *Obbligatorio.* Il metodo che Adobe utilizzerà nelle chiamate al server. Le opzioni sono `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Stringa | *Obbligatorio.* Seleziona `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Stringa | *Obbligatorio.* Questa stringa è la versione con sequenza di caratteri che trasforma i dati dei clienti Platform nel formato previsto dal servizio. <br> <ul><li> Per informazioni su come scrivere il modello, leggi il [Utilizzo della sezione di template](./message-format.md#using-templating). </li><li> Per ulteriori informazioni sull&#39;escape dei caratteri, consulta la [RFC JSON standard, sezione sette](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Per un esempio di trasformazione semplice, consulta la sezione [Attributi del profilo](./message-format.md#attributes) trasformazione. </li></ul> |
| `httpTemplate.contentType` | Stringa | *Obbligatorio.* Il tipo di contenuto accettato dal server. Questo valore è più probabile `application/json`. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione del server di destinazione appena creata.

## Elenca configurazioni server di destinazione {#retrieve-list}

Puoi recuperare un elenco di tutte le configurazioni del server di destinazione per la tua organizzazione IMS effettuando una richiesta di GET al `/authoring/destination-servers` punto finale.

**Formato API**


```http
GET /authoring/destination-servers
```

**Richiesta**

La seguente richiesta recupererà l’elenco delle configurazioni del server di destinazione a cui hai accesso, in base alla configurazione dell’organizzazione IMS e della sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta seguente restituisce lo stato HTTP 200 con un elenco di configurazioni del server di destinazione a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Uno `instanceId` corrisponde al modello per un server di destinazione. La risposta viene troncata per brevità.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      },
      {
         "instanceId":"d88de647-a352-4824-8b46-354afc7acbff",
         "createdDate":"2020-11-17T16:50:59.635228Z",
         "lastModifiedDate":"2020-11-17T16:50:59.635228Z",
         "name":"Test11 Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
    
```

## Aggiornare una configurazione del server di destinazione esistente {#update}

È possibile aggiornare una configurazione del server di destinazione esistente effettuando una richiesta di PUT al `/authoring/destination-servers` e fornisce l&#39;ID istanza della configurazione del server di destinazione che desideri aggiornare. Nel corpo della chiamata , fornisci la configurazione aggiornata del server di destinazione.

**Formato API**


```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione del server di destinazione da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna una configurazione del server di destinazione esistente, configurata dai parametri forniti nel payload.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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





## Recupera una configurazione specifica del server di destinazione {#get}

È possibile recuperare informazioni dettagliate su una configurazione specifica del server di destinazione effettuando una richiesta GET al `/authoring/destination-servers` e fornisce l&#39;ID istanza della configurazione del server di destinazione che desideri aggiornare.

**Formato API**


```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione del server di destinazione da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla configurazione del server di destinazione specificata.

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


## Eliminare una configurazione specifica del server di destinazione {#delete}

È possibile eliminare la configurazione del server di destinazione specificata effettuando una richiesta di DELETE al `/authoring/destination-servers` e fornisce l’ID della configurazione del server di destinazione che desideri eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | La `id` della configurazione del server di destinazione da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come configurare il server di destinazione e il modello utilizzando `/authoring/destination-servers` Endpoint API. Leggi [come utilizzare Destination SDK per configurare la destinazione](./configure-destination-instructions.md) per capire dove si adatta questo passaggio al processo di configurazione della destinazione.
