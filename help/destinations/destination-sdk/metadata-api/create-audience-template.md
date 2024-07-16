---
description: Questa pagina esemplifica la chiamata API utilizzata per creare un modello di pubblico tramite Adobe Experience Platform Destination SDK.
title: Creare un modello di pubblico
exl-id: 98d30002-d462-4008-9337-7de0cd608194
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 3%

---

# Creare un modello di pubblico

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Per alcune destinazioni create con Destination SDK, devi creare una configurazione di metadati di pubblico per creare, aggiornare o eliminare in modo programmatico i metadati di pubblico nella destinazione. Questa pagina mostra come utilizzare l&#39;endpoint API `/authoring/audience-templates` per creare la configurazione.

Per una descrizione dettagliata delle funzionalità che è possibile configurare tramite questo endpoint, vedere [Gestione metadati pubblico](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API dei modelli di pubblico {#get-started}

Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Creare un modello di pubblico {#create}

Per creare un nuovo modello di pubblico, devi eseguire una richiesta `POST` all&#39;endpoint `/authoring/audience-templates`.

**Formato API**

```http
POST /authoring/audience-templates
```

+++Richiesta

La richiesta seguente crea un nuovo modello di pubblico, configurato dai parametri forniti nel payload. Il payload seguente include tutti i parametri accettati dall&#39;endpoint `/authoring/audience-templates`. Tieni presente che non è necessario aggiungere tutti i parametri alla chiamata e che il modello è personalizzabile, in base ai requisiti API.

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
| `name` | Stringa | Il nome del modello di metadati del pubblico per la destinazione. Questo nome verrà visualizzato in qualsiasi messaggio di errore specifico del partner nell&#39;interfaccia utente di Experience Platform, seguito dal messaggio di errore analizzato da `metadataTemplate.create.errorSchemaMap`. |
| `url` | Stringa | L’URL e l’endpoint dell’API, utilizzati per creare, aggiornare, eliminare o convalidare i tipi di pubblico nella piattaforma. Due esempi di settore sono: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` e `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Stringa | Il metodo utilizzato sull’endpoint per creare, aggiornare, eliminare o convalidare a livello di programmazione il pubblico nella destinazione. Esempio: `POST`, `PUT`, `DELETE` |
| `headers.header` | Stringa | Specifica eventuali intestazioni HTTP da aggiungere alla chiamata all’API. Ad esempio, `"Content-Type"` |
| `headers.value` | Stringa | Specifica il valore delle intestazioni HTTP da aggiungere alla chiamata all’API. Ad esempio, `"application/x-www-form-urlencoded"` |
| `requestBody` | Stringa | Specifica il contenuto del corpo del messaggio da inviare all’API. I parametri da aggiungere all&#39;oggetto `requestBody` dipendono dai campi accettati dall&#39;API. Ad esempio, fai riferimento al [primo esempio di modello](../functionality/audience-metadata-management.md#example-1) nel documento di funzionalità dei metadati del pubblico. |
| `responseFields.name` | Stringa | Specifica eventuali campi di risposta restituiti dall’API quando vengono chiamati. Ad esempio, consulta gli [esempi di modelli](../functionality/audience-metadata-management.md#examples) nel documento relativo alla funzionalità per i metadati per il pubblico. |
| `responseFields.value` | Stringa | Specifica il valore di tutti i campi di risposta restituiti dall’API quando vengono chiamati. |
| `responseErrorFields.name` | Stringa | Specifica eventuali campi di risposta restituiti dall’API quando vengono chiamati. Ad esempio, consulta gli [esempi di modelli](../functionality/audience-metadata-management.md#examples) nel documento relativo alla funzionalità per i metadati per il pubblico. |
| `responseErrorFields.value` | Stringa | Analizza eventuali messaggi di errore restituiti nelle risposte alle chiamate API dalla destinazione. Questi messaggi di errore verranno visualizzati dagli utenti nell’interfaccia utente di Experience Platform. |
| `validations.field` | Stringa | Indica se è necessario eseguire le convalide per qualsiasi campo prima di effettuare chiamate API alla destinazione. Ad esempio, è possibile utilizzare `{{validations.accountId}}` per convalidare l&#39;ID account dell&#39;utente. |
| `validations.regex` | Stringa | Indica come deve essere strutturato il campo affinché la convalida possa passare. |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli del modello di pubblico appena creato.

+++

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai quando utilizzare i modelli di pubblico e come configurare un modello di pubblico utilizzando l&#39;endpoint API `/authoring/audience-templates`. Leggi [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della destinazione.
