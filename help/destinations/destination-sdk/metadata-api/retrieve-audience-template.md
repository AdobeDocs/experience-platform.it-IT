---
description: Questa pagina esemplifica la chiamata API utilizzata per recuperare un modello di pubblico tramite Adobe Experience Platform Destination SDK.
title: Recuperare un modello di pubblico
exl-id: 44f2d571-49c5-4112-b3ee-bc839f2b0874
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 1%

---

# Recuperare un modello di pubblico

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per recuperare un modello di metadati di pubblico, utilizzando l&#39;endpoint API `/authoring/audience-templates`.

Per una descrizione dettagliata delle funzionalità che è possibile configurare tramite questo endpoint, vedere [Gestione metadati pubblico](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API dei modelli di pubblico {#get-started}

Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Recuperare un modello di pubblico {#retrieve}

Per recuperare un modello di pubblico esistente, devi eseguire una richiesta `GET` all&#39;endpoint `/authoring/audience-templates`.

**Formato API**

Utilizza il seguente formato API per recuperare tutti i modelli di pubblico per il tuo account.

```http
GET /authoring/audience-templates
```

Utilizza il seguente formato API per recuperare un modello di pubblico specifico, definito dal parametro `{INSTANCE_ID}`.

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

Le due richieste seguenti recuperano tutti i modelli di pubblico per l’organizzazione IMS o un modello di pubblico specifico, a seconda che nella richiesta venga passato il parametro `INSTANCE_ID`.

Seleziona ciascuna scheda di seguito per visualizzare il payload corrispondente.

>[!BEGINTABS]

>[!TAB Recupera tutti i modelli di pubblico]

La richiesta seguente recupererà l&#39;elenco dei modelli di pubblico a cui hai accesso, in base a [!DNL IMS Org ID] e alla configurazione sandbox.

+++Richiesta

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di modelli di pubblico a cui hai accesso, in base a [!DNL IMS Org ID] e al nome di sandbox utilizzati. Un `instanceId` corrisponde a un modello di pubblico.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

+++

>[!TAB Recuperare un modello di pubblico specifico]

La richiesta seguente recupererà l&#39;elenco dei modelli di pubblico a cui hai accesso, in base a [!DNL IMS Org ID] e alla configurazione sandbox.

+++Richiesta

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID del modello di pubblico da recuperare. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del modello di pubblico corrispondenti al `{INSTANCE_ID}` fornito nella chiamata.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

+++

>[!ENDTABS]

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, saprai come recuperare i dettagli sulla configurazione del server di destinazione utilizzando l&#39;endpoint API `/authoring/destination-servers`. Leggi [come utilizzare Destination SDK per configurare la tua destinazione](../guides/configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della tua destinazione.
