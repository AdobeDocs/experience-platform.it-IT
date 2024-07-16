---
description: Questa pagina esemplifica la chiamata API utilizzata per eliminare una configurazione del server di destinazione esistente tramite il Adobe Experience Platform Destination SDK.
title: Eliminare una configurazione del server di destinazione
exl-id: 2322a2ce-220e-4590-a553-b15152412752
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# Eliminare una configurazione del server di destinazione

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per eliminare una configurazione del server di destinazione esistente, utilizzando l&#39;endpoint API `/authoring/destination-servers`.

Per una descrizione dettagliata delle funzionalità che è possibile eliminare tramite questo endpoint, leggi i seguenti articoli:

* [Specifiche del server per le destinazioni create con Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Specifiche di modello per le destinazioni create con Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Formato del messaggio](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configurazione formattazione file](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API del server di destinazione {#get-started}

Prima di continuare, consulta la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Eliminare una configurazione del server di destinazione {#delete}

È possibile eliminare una configurazione del server di destinazione [esistente](create-destination-server.md) effettuando una richiesta `DELETE` all&#39;endpoint `/authoring/destination-servers` con `{INSTANCE_ID}` della configurazione del server di destinazione che si desidera eliminare.

>[!TIP]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Per ottenere una configurazione del server di destinazione esistente e i relativi `{INSTANCE_ID}`, vedere l&#39;articolo relativo al [recupero di una configurazione del server di destinazione](retrieve-destination-server.md).

**Formato API**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` della configurazione del server di destinazione da eliminare. |

+++Richiesta

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come eliminare un server di destinazione esistente tramite l&#39;endpoint API Destination SDK `/authoring/destination-servers`.

Per ulteriori informazioni su cosa è possibile fare con questo endpoint, consulta i seguenti articoli:

* [Creare una configurazione del server di destinazione](create-destination-server.md)
* [Recuperare una configurazione del server di destinazione](retrieve-destination-server.md)
* [Aggiornare una configurazione del server di destinazione](update-destination-server.md)
