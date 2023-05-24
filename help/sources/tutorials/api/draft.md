---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;
title: Flussi Di Dati Bozza Utilizzando L’API Del Servizio Flusso
description: Scopri come impostare i flussi di dati in stato di bozza utilizzando l’API del servizio Flusso.
badge: label="New Feature" type="Positivo"
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 3%

---

# Flussi di dati in bozza utilizzando l’API del servizio Flusso

Salva i flussi di dati come bozze quando utilizzi l’API del servizio Flusso fornendo il `mode=draft` parametro query durante la chiamata di creazione del flusso. Le bozze possono essere aggiornate in un secondo momento con nuove informazioni e quindi pubblicate quando sono pronte. Questo tutorial illustra i passaggi necessari per impostare i flussi di dati in stato di bozza utilizzando l’API del servizio Flusso.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Prerequisiti

Questo tutorial richiede di aver già generato le risorse necessarie per creare un flusso di dati. Ciò include quanto segue:

* Una connessione di base autenticata
* Una connessione sorgente
* Uno schema XDM di destinazione
* Un set di dati di destinazione
* Una connessione di destinazione
* Una mappatura

Se non disponi ancora di questi valori, seleziona un’origine da [il catalogo nella panoramica delle origini](../../home.md). Quindi, segui le istruzioni di quella determinata origine per generare le risorse necessarie per la bozza di un flusso di dati.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../landing/api-guide.md).

## Impostare un flusso di dati sullo stato Bozza

Le sezioni seguenti descrivono il processo per impostare un flusso di dati come bozza, aggiornarlo, pubblicarlo e infine eliminarlo.

### Creare un flusso di dati

Per impostare un flusso di dati come bozza, effettua una richiesta POST al `/flows` endpoint durante l&#39;aggiunta di `mode=draft` come parametro di query. Questo consente di creare un flusso di dati e salvarlo come bozza.

**Formato API**

```http
POST /flows?mode=draft
```

| Parametro | Descrizione |
| --- | --- |
| `mode` | Parametro di query fornito dall’utente che determina lo stato del flusso di dati. Per impostare un flusso di dati come sformo, impostate `mode` a `draft`. |

**Richiesta**

La richiesta seguente crea un flusso di dati bozza.

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**Risposta**

Una risposta corretta restituisce `id` e il corrispondente `etag` del flusso di dati.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Aggiornare un flusso di dati

Per aggiornare la bozza, effettua una richiesta PATCH al `/flows` fornendo l’ID del flusso di dati che desideri aggiornare. Durante questo passaggio, devi anche fornire un `If-Match` parametro di intestazione, che corrisponde al `etag` del flusso di dati che desideri aggiornare.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

Le seguenti richieste aggiungono trasformazioni di mappatura al flusso di dati di bozza.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e `etag`. Per verificare la modifica, puoi effettuare una richiesta GET al `/flows` mentre fornisci l’ID di flusso.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Pubblicare un flusso di dati

Quando la bozza è pronta per la pubblicazione, invia una richiesta POST al `/flows` endpoint, fornendo l’ID del flusso di dati bozza da pubblicare e un’operazione di pubblicazione.

**Formato API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parametro | Descrizione |
| --- | --- |
| `op` | Operazione che aggiorna lo stato del flusso di dati sottoposto a query. Per pubblicare un flusso di dati 2D, impostate `op` a `publish`. |

**Richiesta**

La richiesta seguente pubblica il flusso di dati della bozza.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID e i corrispondenti `etag` del flusso di dati.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Eliminare un flusso di dati

Per eliminare il flusso di dati, effettua una richiesta DELETE al `/flows` endpoint, fornendo l’ID del flusso di dati da eliminare. Per i passaggi dettagliati su come eliminare un flusso di dati utilizzando l’API del servizio Flusso, consulta la guida su [eliminazione di un flusso di dati nell’API](./delete-dataflows.md).
