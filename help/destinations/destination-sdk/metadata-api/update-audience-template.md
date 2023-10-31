---
description: Questa pagina esemplifica la chiamata API utilizzata per aggiornare un modello di pubblico tramite Adobe Experience Platform Destination SDK.
title: Aggiornare un modello di pubblico
exl-id: 8185a015-256d-46a7-af33-8475832fb6c1
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 3%

---

# Aggiornare un modello di pubblico

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Questa pagina illustra la richiesta API e il payload che puoi utilizzare per aggiornare un modello di pubblico, utilizzando `/authoring/audience-templates` Endpoint API

Per una descrizione dettagliata delle funzionalità che è possibile configurare tramite questo endpoint, vedi [gestione dei metadati del pubblico](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API dei modelli di pubblico {#get-started}

Prima di continuare, controlla [guida introduttiva](../getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Aggiornare un modello di pubblico {#create}

È possibile aggiornare una [esistente](create-audience-template.md) modello di pubblico creando un `PUT` richiesta al `/authoring/audience-templates` con il payload aggiornato.

Per ottenere un modello di pubblico esistente e i corrispondenti `{INSTANCE_ID}`, consulta l’articolo su [recupero di un modello di pubblico](retrieve-audience-template.md).

**Formato API**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID del modello di pubblico che desideri aggiornare. Per ottenere un modello di pubblico esistente e i corrispondenti `{INSTANCE_ID}`, vedi [Recuperare un modello di pubblico](retrieve-audience-template.md). |

La richiesta seguente aggiorna un modello di metadati di pubblico esistente, configurato dai parametri forniti nel payload.

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}'
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del modello di pubblico aggiornato.

+++

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai quando utilizzare i modelli di pubblico e come aggiornare un modello di pubblico utilizzando `/authoring/audience-templates` Endpoint API Letto [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della destinazione.
