---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;eliminare account di destinazione;eliminare;api;home;popular topic;flow service;delete destination accounts;delete;api
solution: Experience Platform
title: Eliminare un account di destinazione utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come eliminare un account di destinazione utilizzando l’API del servizio Flusso.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# Eliminare un account di destinazione utilizzando l’API del servizio Flusso

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

Prima di attivare i dati, devi connetterti alla destinazione impostando prima un account di destinazione. Questa esercitazione descrive i passaggi per eliminare gli account di destinazione che non sono più necessari utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>L’eliminazione degli account di destinazione è attualmente supportata solo dall’API del servizio Flusso. Gli account di destinazione non possono essere eliminati utilizzando l’interfaccia utente di Experience Platform.

## Introduzione {#get-started}

Questo tutorial richiede un ID di connessione valido. L’ID di connessione rappresenta la connessione dell’account alla destinazione. Se non disponi di un ID di connessione valido, seleziona la destinazione desiderata tra [catalogo delle destinazioni](../catalog/overview.md) e segui i passaggi descritti per [connettersi alla destinazione](../ui/connect-destination.md) prima di provare questa esercitazione.

Questo tutorial richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Destinazioni](../home.md): [!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per eliminare correttamente un account di destinazione utilizzando [!DNL Flow Service] API.

### Lettura delle chiamate API di esempio {#reading-sample-api-calls}

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste {#gather-values-for-required-headers}

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti a [!DNL Flow Service], sono isolate in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se il `x-sandbox-name` non è specificata, le richieste vengono risolte in `prod` sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Trova l’ID di connessione dell’account di destinazione da eliminare {#find-connection-id}

>[!NOTE]
>Questa esercitazione utilizza [Destinazione dirigibile](../catalog/mobile-engagement/airship-attributes.md) ad esempio, ma i passaggi descritti si applicano a qualsiasi [destinazioni disponibili](../catalog/overview.md).

Il primo passaggio nell’eliminazione di un account di destinazione consiste nell’individuare l’ID di connessione corrispondente all’account di destinazione che desideri eliminare.

Nell’interfaccia utente di Experience Platform, passa a **[!UICONTROL Destinazioni]** > **[!UICONTROL Account]** e selezionare l&#39;account che si desidera eliminare selezionando il numero nel **[!UICONTROL Destinazioni]** colonna.

![Seleziona account di destinazione da eliminare](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Successivamente, puoi recuperare l’ID di connessione dell’account di destinazione dall’URL nel browser.

![Recupera ID connessione da URL](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## Elimina connessione {#delete-connection}

>[!IMPORTANT]
>
>Prima di eliminare l’account di destinazione, devi eliminare tutti i flussi di dati esistenti dall’account di destinazione.
>Per eliminare i flussi di dati esistenti, consulta le pagine seguenti:
>* [Utilizzare l’interfaccia utente di Experience Platform](../ui/delete-destinations.md) eliminare i flussi di dati esistenti;
>* [Utilizzare l’API del servizio Flusso](delete-destination-dataflow.md) per eliminare i flussi di dati esistenti.


Dopo aver ottenuto un ID di connessione e aver verificato che non vi siano flussi di dati per l’account di destinazione, esegui una richiesta DELETE a [!DNL Flow Service] API.

**Formato API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | L&#39;unico `id` valore per la connessione che si desidera eliminare. |

**Richiesta**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto. Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) alla connessione. L’API restituirà un errore HTTP 404 (Non trovato), che indica che l’account di destinazione è stato eliminato.

## Gestione degli errori API {#api-error-handling}

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!DNL Flow Service] API per eliminare gli account di destinazione esistenti. Per ulteriori informazioni sull’utilizzo delle destinazioni, consulta [panoramica sulle destinazioni](/help/destinations/home.md).