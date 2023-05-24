---
description: Questa pagina esemplifica la chiamata API utilizzata per eliminare una configurazione di destinazione esistente tramite Adobe Experience Platform Destination SDK.
title: Eliminare una configurazione di destinazione
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# Eliminare una configurazione di destinazione

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per eliminare una configurazione di destinazione esistente, utilizzando `/authoring/destinations` Endpoint API

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API di configurazione di destinazione {#get-started}

Prima di continuare, controlla [guida introduttiva](../../getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Eliminare una configurazione di destinazione {#delete}

È possibile eliminare un [esistente](create-destination-configuration.md) configurazione del server di destinazione effettuando una `DELETE` richiesta al `/authoring/destinations` endpoint con `{INSTANCE_ID}`della configurazione di destinazione che desideri eliminare.

>[!TIP]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destinations`

Per ottenere una configurazione di destinazione esistente e la corrispondente `{INSTANCE_ID}`, consulta l’articolo su [recupero di una configurazione di destinazione](retrieve-destination-configuration.md).

**Formato API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | Il `ID` della configurazione di destinazione da eliminare. |

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

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come eliminare una configurazione di destinazione esistente tramite la Destination SDK `/authoring/destinations` Endpoint API

Per ulteriori informazioni su cosa è possibile fare con questo endpoint, consulta i seguenti articoli:

* [Creare una configurazione di destinazione](create-destination-configuration.md)
* [Recuperare una configurazione di destinazione](retrieve-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](update-destination-configuration.md)

