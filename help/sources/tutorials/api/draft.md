---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;
title: Flussi Di Dati Bozza Utilizzando L’API Del Servizio Di Flusso
description: Scopri come impostare i flussi di dati in uno stato di bozza utilizzando l’API del servizio di flusso.
badge: label="Nuova funzione" type="Positiva"
source-git-commit: d093e34ae4b353d1ed6db922b6da66cf23f25c48
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 3%

---

# Flussi di dati Bozza tramite l’API del servizio di flusso

Salva i flussi di dati come bozze quando utilizzi l’API del servizio di flusso fornendo il `mode=draft` parametro query durante la chiamata di creazione del flusso. Le bozze possono essere aggiornate in un secondo momento con nuove informazioni e quindi pubblicate una volta pronte. Questa esercitazione descrive i passaggi per impostare i flussi di dati in uno stato di bozza utilizzando l’API del servizio di flusso.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Prerequisiti

Questa esercitazione richiede di aver già generato le risorse necessarie per creare un flusso di dati. Ciò include i seguenti elementi:

* Connessione di base autenticata
* Connessione sorgente
* Uno schema XDM di destinazione
* Un set di dati di destinazione
* Connessione di destinazione
* Mappatura

Se questi valori non sono ancora disponibili, selezionare un&#39;origine da [il catalogo nella panoramica delle origini](../../home.md). Quindi, segui le istruzioni di quella determinata origine per generare le risorse necessarie per creare un flusso di dati.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Impostare un flusso di dati su stato bozza

Le sezioni seguenti descrivono il processo per impostare un flusso di dati come bozza, aggiornare il flusso di dati, pubblicare il flusso di dati e infine eliminare il flusso di dati.

### Bozza un flusso di dati

Per impostare un flusso di dati come bozza, invia una richiesta POST al `/flows` endpoint durante l&#39;aggiunta di `mode=draft` come parametro di query. Questo consente di creare un flusso di dati e salvarlo come bozza.

**Formato API**

```http
POST /flows?mode=draft
```

| Parametro | Descrizione |
| --- | --- |
| `mode` | Parametro di query fornito dall&#39;utente che determina lo stato del flusso di dati. Per impostare un flusso di dati come bozza, imposta `mode` a `draft`. |

**Richiesta**

La seguente richiesta crea un flusso di dati di bozza.

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

Una risposta corretta restituisce il `id` e il corrispondente `etag` del flusso di dati.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Aggiornare un flusso di dati

Per aggiornare la bozza, invia una richiesta PATCH al `/flows` durante la fornitura dell&#39;ID del flusso di dati che si desidera aggiornare. Durante questo passaggio, devi anche fornire un `If-Match` parametro header , che corrisponde al `etag` del flusso di dati da aggiornare.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

Le richieste seguenti aggiungono trasformazioni di mappatura al flusso di dati di bozza.

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

Una risposta corretta restituisce l&#39;ID di flusso e `etag`. Per verificare la modifica, puoi effettuare una richiesta GET al `/flows` durante la fornitura dell&#39;ID flusso.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Pubblicare un flusso di dati

Una volta che la bozza è pronta per essere pubblicata, invia una richiesta a POST `/flows` fornendo l&#39;ID del flusso di dati bozza da pubblicare, nonché un&#39;operazione di pubblicazione.

**Formato API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parametro | Descrizione |
| --- | --- |
| `op` | Operazione che aggiorna lo stato del flusso di dati interrogato. Per pubblicare un flusso di dati bozza, imposta `op` a `publish`. |

**Richiesta**

La seguente richiesta pubblica il flusso di dati della bozza.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce l&#39;ID e il corrispondente `etag` del flusso di dati.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Eliminare un flusso di dati

Per eliminare il flusso di dati, invia una richiesta DELETE al `/flows` durante la fornitura dell&#39;ID del flusso di dati da eliminare. Per passaggi dettagliati su come eliminare un flusso di dati utilizzando l’API del servizio di flusso, consulta la guida su [eliminazione di un flusso di dati nell’API](./delete-dataflows.md).