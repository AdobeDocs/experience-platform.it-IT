---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;API;api;eliminare;eliminare flussi di dati
solution: Experience Platform
title: Eliminare un flusso di dati utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come eliminare i flussi di dati in batch e in streaming utilizzando l’API del servizio Flusso.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 3%

---

# Eliminare un flusso di dati utilizzando l’API del servizio Flusso

È possibile eliminare i flussi di dati batch e in streaming che contengono errori o che sono diventati obsoleti utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Questo tutorial illustra i passaggi necessari per eliminare i flussi di dati creati con origini batch e di streaming utilizzando [!DNL Flow Service].

## Introduzione

Questo tutorial richiede un ID di flusso valido. Se non disponi di un ID di flusso valido, seleziona il connettore desiderato dalla [panoramica origini](../../home.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questo tutorial richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Eliminare un flusso di dati

Con un ID di flusso esistente, puoi eliminare un flusso di dati eseguendo una richiesta DELETE all&#39;API [!DNL Flow Service].

**Formato API**

```http
DELETE /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | Valore `id` univoco per il flusso di dati che si desidera eliminare. |

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

Seguendo questa esercitazione, hai utilizzato correttamente l&#39;API [!DNL Flow Service] per eliminare un flusso di dati esistente.

Per i passaggi su come eseguire queste operazioni utilizzando l&#39;interfaccia utente, fare riferimento al tutorial su [eliminazione dei flussi di dati nell&#39;interfaccia utente](../../tutorials/ui/delete.md)
