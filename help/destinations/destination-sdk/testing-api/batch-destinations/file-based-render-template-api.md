---
description: Questa pagina spiega come utilizzare l’endpoint /authoring/testing/template/render per visualizzare l’aspetto dei campi dati cliente definiti nella configurazione di destinazione.
title: Convalida campi cliente con modello
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 6bd169075cd3826ae2a0907e6e624fd901076a4a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---


# Convalida campi cliente con modello

## Panoramica {#overview}

L&#39;endpoint `/authoring/testing/template/render` consente di visualizzare l&#39;aspetto dei [campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md) definiti nella configurazione di destinazione.

L’endpoint genera valori casuali per i campi dati del cliente e li restituisce nella risposta. Questo consente di convalidare la struttura semantica dei campi dati del cliente, ad esempio i nomi dei bucket o i percorsi delle cartelle.

## Introduzione {#getting-started}

Prima di continuare, consulta la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare l&#39;endpoint `/template/render`, verificare di soddisfare le seguenti condizioni:

* Hai già una destinazione basata su file creata tramite la Destination SDK e la puoi visualizzare nel [catalogo delle destinazioni](../../../ui/destinations-workspace.md).
* Per eseguire correttamente la richiesta API, è necessario disporre dell’ID dell’istanza di destinazione corrispondente all’istanza di destinazione da testare. Ottieni dall’URL l’ID dell’istanza di destinazione da utilizzare nella chiamata API per la navigazione di una connessione con la destinazione nell’interfaccia utente di Platform.

  ![Immagine dell&#39;interfaccia utente che mostra come ottenere l&#39;ID dell&#39;istanza di destinazione dall&#39;URL.](../../assets/testing-api/get-destination-instance-id.png)

## Campi cliente con modello di rendering {#render-customer-fields}

**Formato API**

```http
POST /authoring/testing/template/render/destination
```

Per illustrare il comportamento di questo endpoint API, prendiamo in considerazione una destinazione basata su file con la seguente configurazione dei campi dati del cliente:

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

La richiesta seguente chiama l&#39;endpoint `/authoring/testing/template/render`, che restituisce una risposta con valori generati in modo casuale per i due campi dati cliente sopra menzionati.

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

| Elemento “parameters” | Descrizione |
| -------- | ----------- |
| `destinationId` | ID della [configurazione di destinazione](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) che si sta testando. |
| `templates` | I nomi dei campi con modelli definiti nella [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato `HTTP 200 OK` e il corpo include valori generati in modo casuale per i campi modello.

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

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, sai come convalidare la configurazione del campo dati cliente definita nel [server di destinazione](../../authoring-api/destination-server/create-destination-server.md).
