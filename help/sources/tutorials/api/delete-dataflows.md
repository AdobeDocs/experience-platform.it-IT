---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;API;api;eliminare;eliminare flussi di dati
solution: Experience Platform
title: Eliminare un flusso di dati utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come eliminare i flussi di dati in batch e in streaming utilizzando l’API del servizio Flusso.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 3%

---

# Eliminare un flusso di dati utilizzando l’API del servizio Flusso

Puoi eliminare i flussi di dati batch e in streaming che contengono errori o sono diventati obsoleti utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Questa esercitazione descrive i passaggi per eliminare i flussi di dati creati sia con origini in batch che in streaming utilizzando [!DNL Flow Service].

## Introduzione

Questo tutorial richiede un ID di flusso valido. Se non disponi di un ID di flusso valido, seleziona il connettore desiderato da [panoramica sulle origini](../../home.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questo tutorial richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../landing/api-guide.md).

## Eliminare un flusso di dati

Con un ID di flusso esistente, puoi eliminare un flusso di dati eseguendo una richiesta DELETE al [!DNL Flow Service] API.

**Formato API**

```http
DELETE /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | L&#39;unico `id` valore per il flusso di dati che desideri eliminare. |

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto. Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) nel flusso di dati. L’API restituirà un errore HTTP 404 (Non trovato), che indica che il flusso di dati è stato eliminato.

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!DNL Flow Service] API per eliminare un flusso di dati esistente.

Per i passaggi su come eseguire queste operazioni utilizzando l’interfaccia utente, consulta l’esercitazione su [eliminazione di flussi di dati nell’interfaccia utente](../../tutorials/ui/delete.md)
