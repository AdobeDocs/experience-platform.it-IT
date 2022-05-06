---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;eliminare account;eliminare;api
solution: Experience Platform
title: Eliminare un account tramite l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come eliminare un account utilizzando l’API del servizio di flusso.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# Eliminare un account tramite l’API del servizio di flusso

È possibile eliminare account di origine contenenti errori o diventati obsoleti utilizzando la variabile [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Per informazioni su come eliminare un account utilizzando l’API, consulta la seguente esercitazione.

## Introduzione

Questa esercitazione richiede un ID di connessione valido. Se non si dispone di un ID di connessione valido, selezionare il connettore di scelta dal [panoramica di origini](../../home.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Elimina account

>[!TIP]
>
>Prima di eliminare l&#39;account di origine, è necessario eliminare tutti i flussi di dati esistenti associati all&#39;account di origine. Per eliminare i flussi di dati esistenti, consulta l’esercitazione su [eliminazione dei flussi di dati di origini](./delete-dataflows.md).

Per eliminare un account, effettua una richiesta DELETE al [!DNL Flow Service] API fornendo l’ID di connessione di base corrispondente all’account da eliminare.

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

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) alla connessione.

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!DNL Flow Service] API per eliminare gli account esistenti.

Per i passaggi su come eseguire queste operazioni utilizzando l’interfaccia utente, consulta l’esercitazione su [eliminazione di account nell’interfaccia utente](../../tutorials/ui/delete-accounts.md).
