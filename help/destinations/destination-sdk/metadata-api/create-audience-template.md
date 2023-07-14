---
description: Questa pagina esemplifica la chiamata API utilizzata per creare un modello di pubblico tramite Adobe Experience Platform Destination SDK.
title: Creare un modello di pubblico
source-git-commit: 3f31a54c0cf329d374808dacce3fac597a72aa11
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 4%

---


# Creare un modello di pubblico

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Per alcune destinazioni create con Destination SDK, devi creare una configurazione di metadati di pubblico per creare, aggiornare o eliminare in modo programmatico i metadati di pubblico nella destinazione. In questa pagina viene illustrato come utilizzare `/authoring/audience-templates` Endpoint API per creare la configurazione.

Per una descrizione dettagliata delle funzionalità che è possibile configurare tramite questo endpoint, vedi [gestione dei metadati del pubblico](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API dei modelli di pubblico {#get-started}

Prima di continuare, controlla [guida introduttiva](../getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Creare un modello di pubblico {#create}

Per creare un nuovo modello di pubblico, devi eseguire una `POST` richiesta al `/authoring/audience-templates` endpoint.

**Formato API**

```http
POST /authoring/audience-templates
```

+++Richiesta

La richiesta seguente crea un nuovo modello di pubblico, configurato dai parametri forniti nel payload. Il payload riportato di seguito include tutti i parametri accettati dal `/authoring/audience-templates` endpoint. Tieni presente che non è necessario aggiungere tutti i parametri alla chiamata e che il modello è personalizzabile, in base ai requisiti API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Proprietà | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `name` | Stringa | Il nome del modello di metadati del pubblico per la destinazione. Questo nome verrà visualizzato in qualsiasi messaggio di errore specifico del partner nell’interfaccia utente di Experience Platform, seguito dal messaggio di errore analizzato da `metadataTemplate.create.errorSchemaMap`. |
| `url` | Stringa | L’URL e l’endpoint dell’API, utilizzati per creare, aggiornare, eliminare o convalidare i tipi di pubblico nella piattaforma. Due esempi di settore: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` e `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Stringa | Il metodo utilizzato sull’endpoint per creare, aggiornare, eliminare o convalidare a livello di programmazione il pubblico nella destinazione. Ad esempio: `POST`, `PUT`, `DELETE` |
| `headers.header` | Stringa | Specifica eventuali intestazioni HTTP da aggiungere alla chiamata all’API. Ad esempio, `"Content-Type"` |
| `headers.value` | Stringa | Specifica il valore delle intestazioni HTTP da aggiungere alla chiamata all’API. Ad esempio, `"application/x-www-form-urlencoded"` |
| `requestBody` | Stringa | Specifica il contenuto del corpo del messaggio da inviare all’API. I parametri da aggiungere al `requestBody` L’oggetto dipende dai campi accettati dall’API. Ad esempio, consulta [primo esempio di modello](../functionality/audience-metadata-management.md#example-1) nel documento relativo alla funzionalità Metadati del pubblico. |
| `responseFields.name` | Stringa | Specifica eventuali campi di risposta restituiti dall’API quando vengono chiamati. Ad esempio, consulta [esempi di modelli](../functionality/audience-metadata-management.md#examples) nel documento relativo alla funzionalità Metadati del pubblico. |
| `responseFields.value` | Stringa | Specifica il valore di tutti i campi di risposta restituiti dall’API quando vengono chiamati. |
| `responseErrorFields.name` | Stringa | Specifica eventuali campi di risposta restituiti dall’API quando vengono chiamati. Ad esempio, consulta [esempi di modelli](../functionality/audience-metadata-management.md#examples) nel documento relativo alla funzionalità Metadati del pubblico. |
| `responseErrorFields.value` | Stringa | Analizza eventuali messaggi di errore restituiti nelle risposte alle chiamate API dalla destinazione. Questi messaggi di errore verranno visualizzati dagli utenti nell’interfaccia utente di Experience Platform. |
| `validations.field` | Stringa | Indica se è necessario eseguire le convalide per qualsiasi campo prima di effettuare chiamate API alla destinazione. Ad esempio, puoi utilizzare `{{validations.accountId}}` per convalidare l’ID account dell’utente. |
| `validations.regex` | Stringa | Indica come deve essere strutturato il campo affinché la convalida possa passare. |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del modello di pubblico appena creato.

+++

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai quando utilizzare i modelli di pubblico e come configurarli utilizzando `/authoring/audience-templates` Endpoint API Letto [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della destinazione.
