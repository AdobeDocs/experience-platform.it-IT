---
description: Questa pagina esemplifica la chiamata API utilizzata per recuperare una configurazione del server di destinazione tramite il Adobe Experience Platform Destination SDK.
title: Recuperare una configurazione del server di destinazione
exl-id: 1b375343-e793-4c91-856f-af66fe71822e
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---

# Recuperare una configurazione del server di destinazione

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per recuperare informazioni su una configurazione del server di destinazione esistente utilizzando `/authoring/destination-servers` Endpoint API

Per una descrizione dettagliata delle funzionalità utilizzate dai server di destinazione, leggi i seguenti articoli:

* [Specifiche del server per le destinazioni create con Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Specifiche di modello per le destinazioni create con Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato del messaggio](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configurazione formattazione file](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API del server di destinazione {#get-started}

Prima di continuare, controlla [guida introduttiva](../../getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Recuperare una configurazione del server di destinazione {#retrieve}

È possibile recuperare una configurazione server di destinazione esistente effettuando una `GET` richiesta al `/authoring/destination-servers` endpoint.

>[!TIP]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**Formato API**

Utilizza il seguente formato API per recuperare tutte le configurazioni del server di destinazione per il tuo account.

```http
GET /authoring/destination-servers
```

Utilizza il seguente formato API per recuperare una configurazione server di destinazione specifica, definita da `{INSTANCE_ID}` parametro.

```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

Le due richieste seguenti recuperano tutte le configurazioni del server di destinazione per l’organizzazione IMS o una configurazione del server di destinazione specifica, a seconda che venga passato o meno il `INSTANCE_ID` nella richiesta.

Seleziona ciascuna scheda di seguito per visualizzare il payload corrispondente e le relative risposte.

>[!BEGINTABS]

>[!TAB Recupera tutte le configurazioni del server di destinazione]

La richiesta seguente recupererà l’elenco delle configurazioni del server di destinazione a cui hai accesso, in base a [!DNL IMS Org ID] e la configurazione della sandbox.

+++Richiesta

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco delle configurazioni del server di destinazione a cui hai accesso, in base al [!DNL IMS Org ID] e il nome della sandbox che hai utilizzato. Uno `instanceId` corrisponde a un server di destinazione. La risposta di esempio seguente include due configurazioni del server di destinazione.

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

+++

>[!TAB Recuperare una configurazione server di destinazione specifica]

La richiesta seguente recupererà una specifica configurazione del server di destinazione definita da `{INSTANCE_ID}` parametro.

+++Richiesta

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione del server di destinazione che desideri recuperare. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con la configurazione del server di destinazione corrispondente al `{INSTANCE_ID}` hai fornito.

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
      }
   ]
}
```

+++

>[!ENDTABS]

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come recuperare una configurazione del server di destinazione tramite Destination SDK `/authoring/destination-servers` Endpoint API

Per ulteriori informazioni su cosa è possibile fare con questo endpoint, consulta i seguenti articoli:

* [Creare una configurazione del server di destinazione](create-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](update-destination-server.md)
* [Eliminare una configurazione del server di destinazione](delete-destination-server.md)
