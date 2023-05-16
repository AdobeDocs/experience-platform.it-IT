---
description: Questa pagina esemplifica la chiamata API utilizzata per eliminare una configurazione del server di destinazione esistente tramite Adobe Experience Platform Destination SDK.
title: Eliminare una configurazione del server di destinazione
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 3%

---


# Eliminare una configurazione del server di destinazione

Questa pagina esemplifica la richiesta API e il payload che puoi utilizzare per eliminare una configurazione del server di destinazione esistente, utilizzando `/authoring/destination-servers` Endpoint API.

Per una descrizione dettagliata delle funzionalità che è possibile eliminare tramite questo endpoint, consulta i seguenti articoli:

* [Specifiche server per le destinazioni create con Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Specifiche dei modelli per le destinazioni create con Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato del messaggio](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configurazione della formattazione dei file](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API del server di destinazione {#get-started}

Prima di continuare, controlla la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Eliminare una configurazione del server di destinazione {#delete}

È possibile eliminare un [esistente](create-destination-server.md) configurazione del server di destinazione effettuando una `DELETE` richiesta al `/authoring/destination-servers` punto finale con `{INSTANCE_ID}`della configurazione del server di destinazione che si desidera eliminare.

>[!TIP]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Per ottenere una configurazione del server di destinazione esistente e la relativa `{INSTANCE_ID}`, consulta l’articolo [recupero di una configurazione del server di destinazione](retrieve-destination-server.md).

**Formato API**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | La `ID` della configurazione del server di destinazione da eliminare. |

+++Richiesta

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Risposta

Una risposta corretta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come eliminare un server di destinazione esistente attraverso la Destination SDK `/authoring/destination-servers` Endpoint API.

Per ulteriori informazioni sulle operazioni che è possibile eseguire con questo endpoint, consulta i seguenti articoli:

* [Creare una configurazione del server di destinazione](create-destination-server.md)
* [Recupera una configurazione del server di destinazione](retrieve-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](update-destination-server.md)

