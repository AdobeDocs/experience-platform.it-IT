---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;API;api;elimina;elimina flussi di dati
solution: Experience Platform
title: Eliminare un flusso di dati utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come eliminare i flussi di dati in batch e in streaming utilizzando l’API del servizio di flusso.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 3%

---

# Eliminare un flusso di dati utilizzando l’API del servizio di flusso

Puoi eliminare i flussi di dati in batch e in streaming che contengono errori o che sono diventati obsoleti utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Questa esercitazione descrive i passaggi per eliminare i flussi di dati creati con origini in batch e in streaming utilizzando [!DNL Flow Service].

## Introduzione

Questa esercitazione richiede un ID di flusso valido. Se non disponi di un ID di flusso valido, seleziona il connettore di scelta dal [panoramica di origini](../../home.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Eliminare un flusso di dati

Con un ID flusso esistente, puoi eliminare un flusso di dati eseguendo una richiesta DELETE al [!DNL Flow Service] API.

**Formato API**

```http
DELETE /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | L&#39;unico `id` del flusso di dati da eliminare. |

**Richiesta**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto. Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) al flusso di dati. L’API restituirà un errore HTTP 404 (Non trovato) che indica che il flusso di dati è stato eliminato.

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!DNL Flow Service] API per eliminare un flusso di dati esistente.

Per i passaggi su come eseguire queste operazioni utilizzando l’interfaccia utente, consulta l’esercitazione su [eliminazione dei flussi di dati nell’interfaccia utente](../../tutorials/ui/delete.md)
