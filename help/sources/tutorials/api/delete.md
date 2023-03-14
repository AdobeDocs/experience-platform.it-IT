---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;eliminare account;eliminare;api;home;popular topic;flow service;delete accounts;delete;api
solution: Experience Platform
title: Eliminare un account utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come eliminare un account utilizzando l’API del servizio Flusso.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# Eliminare un account utilizzando l’API del servizio Flusso

È possibile eliminare i conti di origine che contengono errori o che sono diventati obsoleti utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Consulta il seguente tutorial per i passaggi su come eliminare un account utilizzando l’API.

## Introduzione

Questo tutorial richiede un ID di connessione valido. Se non si dispone di un ID di connessione valido, selezionare il connettore desiderato dall&#39;elenco [panoramica sulle origini](../../home.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questo tutorial richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../landing/api-guide.md).

## Elimina account

>[!TIP]
>
>Prima di eliminare l’account di origine, devi eliminare tutti i flussi di dati esistenti associati all’account di origine. Per eliminare i flussi di dati esistenti, consulta l’esercitazione su [eliminazione dei flussi di dati di origine](./delete-dataflows.md).

Per eliminare un account, effettua una richiesta DELETE al [!DNL Flow Service] fornendo l’ID connessione di base corrispondente all’account che desideri eliminare.

**Formato API**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID di connessione di base dell&#39;account di origine che si desidera eliminare. |

**Richiesta**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto.

Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) alla connessione.

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!DNL Flow Service] API per eliminare gli account esistenti.

Per i passaggi su come eseguire queste operazioni utilizzando l’interfaccia utente, consulta l’esercitazione su [eliminazione di account nell’interfaccia utente](../../tutorials/ui/delete-accounts.md).
