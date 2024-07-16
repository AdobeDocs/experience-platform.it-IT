---
description: Questa pagina esemplifica la chiamata API utilizzata per eliminare una configurazione di destinazione esistente tramite il Adobe Experience Platform Destination SDK.
title: Eliminare una configurazione di destinazione
exl-id: c7309ab7-1b8d-46d4-8017-fd4aa5918cdd
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%

---

# Eliminare una configurazione di destinazione

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per eliminare una configurazione di destinazione esistente, utilizzando l&#39;endpoint API `/authoring/destinations`.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API di configurazione di destinazione {#get-started}

Prima di continuare, consulta la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Eliminare una configurazione di destinazione {#delete}

È possibile eliminare una configurazione del server di destinazione [esistente](create-destination-configuration.md) effettuando una richiesta `DELETE` all&#39;endpoint `/authoring/destinations` con `{INSTANCE_ID}` della configurazione di destinazione da eliminare.

>[!TIP]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destinations`

Per ottenere una configurazione di destinazione esistente e i corrispondenti `{INSTANCE_ID}`, vedere l&#39;articolo relativo al [recupero di una configurazione di destinazione](retrieve-destination-configuration.md).

**Formato API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` della configurazione di destinazione da eliminare. |

+++Richiesta

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.


## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come eliminare una configurazione di destinazione esistente tramite l&#39;endpoint API Destination SDK `/authoring/destinations`.

Per ulteriori informazioni su cosa è possibile fare con questo endpoint, consulta i seguenti articoli:

* [Creare una configurazione di destinazione](create-destination-configuration.md)
* [Recuperare una configurazione di destinazione](retrieve-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](update-destination-configuration.md)
