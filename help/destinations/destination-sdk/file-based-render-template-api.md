---
description: Questa pagina spiega come utilizzare l’endpoint /authoring/testing/template/render per visualizzare l’aspetto dei campi di dati del cliente formattati definiti nella configurazione di destinazione.
title: Convalida dei campi del cliente formattati
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---


# Convalida dei campi del cliente formattati

## Panoramica {#overview}

La `/authoring/testing/template/render` l’endpoint consente di visualizzare il modello [campi dati del cliente](file-based-destination-configuration.md#customer-data-fields) come definito nella configurazione di destinazione.

L’endpoint genera valori casuali per i campi dei dati del cliente e li restituisce nella risposta. Questo consente di convalidare la struttura semantica dei campi di dati del cliente, ad esempio i nomi dei bucket o i percorsi delle cartelle.

## Introduzione {#getting-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare il `/template/render` endpoint, assicurarsi di soddisfare le seguenti condizioni:

* Una destinazione basata su file esistente creata tramite la Destination SDK può essere visualizzata nella [catalogo delle destinazioni](../ui/destinations-workspace.md).
* Per effettuare correttamente la richiesta API, devi disporre dell’ID dell’istanza di destinazione corrispondente all’istanza di destinazione che stai testando. Ottieni dall’URL l’ID dell’istanza di destinazione da utilizzare nella chiamata API quando esplori una connessione con la destinazione nell’interfaccia utente di Platform.

   ![Immagine dell’interfaccia utente che mostra come ottenere l’ID dell’istanza di destinazione dall’URL.](assets/get-destination-instance-id.png)

## Campi del cliente modello di rendering {#render-customer-fields}

**Formato API**

```http
POST /authoring/testing/template/render/destination
```

Per illustrare il comportamento di questo endpoint API, consideriamo una destinazione basata su file con la seguente configurazione dei campi dati cliente:

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**Richiesta**

La richiesta seguente chiama `/authoring/testing/template/render` endpoint , che restituisce una risposta con valori generati in modo casuale per i due campi di dati cliente sopra menzionati.

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| Parametri | Descrizione |
| -------- | ----------- |
| `destinationId` | ID del [configurazione di destinazione](file-based-destination-configuration.md) che stai testando. |
| `templates` | I nomi dei campi formattati definiti nel [configurazione del server di destinazione](server-and-file-configuration.md). |

**Risposta**

Una risposta corretta restituisce un `HTTP 200 OK` e il corpo include valori generati in modo casuale per i campi modelli.

Questa risposta può essere utile per convalidare la struttura corretta dei campi dati del cliente, ad esempio i nomi dei bucket o i percorsi delle cartelle.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come convalidare la configurazione del campo dati del cliente definita nel [server di destinazione](server-and-file-configuration.md).
