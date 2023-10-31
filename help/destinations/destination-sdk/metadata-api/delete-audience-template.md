---
description: Questa pagina esemplifica la chiamata API utilizzata per eliminare un modello di pubblico esistente tramite il Adobe Experience Platform Destination SDK.
title: Eliminare un modello di pubblico
exl-id: 6eb07e3c-3269-4368-9b11-04bd993cc4ab
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 3%

---

# Eliminare un modello di pubblico

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Questa pagina illustra la richiesta API e il payload che puoi utilizzare per eliminare un modello di pubblico, utilizzando `/authoring/audience-templates` Endpoint API

Per una descrizione dettagliata delle funzionalità che è possibile configurare tramite questo endpoint, vedi [gestione dei metadati del pubblico](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API dei modelli di pubblico {#get-started}

Prima di continuare, controlla [guida introduttiva](../getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Eliminare un modello di pubblico {#delete}

È possibile eliminare un [esistente](create-audience-template.md) modello di pubblico creando un `DELETE` richiesta al `/authoring/audience-templates` endpoint con `{INSTANCE_ID}`del modello di pubblico da eliminare.

Per ottenere un modello di pubblico esistente e i corrispondenti `{INSTANCE_ID}`, consulta l’articolo su [recupero di un modello di pubblico](retrieve-audience-template.md).

**Formato API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | Il `ID` del modello di pubblico da eliminare. |

+++Richiesta

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

+++

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come eliminare un modello di pubblico utilizzando `/authoring/audience-templates` Endpoint API Letto [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della destinazione.
