---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;eliminare account di destinazione;eliminare;api;home;popular topic;flow service;delete destination accounts;delete;api
solution: Experience Platform
title: Eliminare un account di destinazione utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come eliminare un account di destinazione utilizzando l’API del servizio Flusso.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 16%

---

# Eliminare un account di destinazione utilizzando l’API del servizio Flusso

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

Prima di attivare i dati, devi connetterti alla destinazione impostando prima un account di destinazione. Questo tutorial illustra i passaggi necessari per eliminare gli account di destinazione che non sono più necessari utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>L’eliminazione degli account di destinazione è attualmente supportata solo dall’API del servizio Flusso. Gli account di destinazione non possono essere eliminati utilizzando l’interfaccia utente di Experience Platform.

## Introduzione {#get-started}

Questo tutorial richiede un ID di connessione valido. L’ID di connessione rappresenta la connessione dell’account alla destinazione. Se non disponi di un ID di connessione valido, seleziona la destinazione desiderata dal [catalogo delle destinazioni](../catalog/overview.md) e segui i passaggi descritti per [connetterti alla destinazione](../ui/connect-destination.md) prima di provare questa esercitazione.

Questo tutorial richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Destinazioni](../home.md): [!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l&#39;attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per eliminare correttamente un account di destinazione utilizzando l&#39;API [!DNL Flow Service].

### Lettura delle chiamate API di esempio {#reading-sample-api-calls}

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste {#gather-values-for-required-headers}

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se l&#39;intestazione `x-sandbox-name` non è specificata, le richieste vengono risolte nella sandbox `prod`.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Trova l’ID di connessione dell’account di destinazione da eliminare {#find-connection-id}

>[!NOTE]
>Questa esercitazione utilizza come esempio la [destinazione dirigibile](../catalog/mobile-engagement/airship-attributes.md), ma i passaggi descritti si applicano a una qualsiasi delle [destinazioni disponibili](../catalog/overview.md).

Il primo passaggio nell’eliminazione di un account di destinazione consiste nell’individuare l’ID di connessione corrispondente all’account di destinazione che desideri eliminare.

Nell&#39;interfaccia utente di Experience Platform, passa a **[!UICONTROL Destinazioni]** > **[!UICONTROL Account]** e seleziona l&#39;account da eliminare selezionando il numero nella colonna **[!UICONTROL Destinazioni]**.

![Seleziona account di destinazione da eliminare](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Successivamente, puoi recuperare l’ID di connessione dell’account di destinazione dall’URL nel browser.

![Recupera ID connessione dall&#39;URL](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

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
>* [Utilizza l&#39;interfaccia utente di Experience Platform](../ui/delete-destinations.md) per eliminare i flussi di dati esistenti;
>* [Utilizzare l&#39;API del servizio Flusso](delete-destination-dataflow.md) per eliminare i flussi di dati esistenti.

Dopo aver ottenuto un ID di connessione e aver verificato che non esistono flussi di dati per l&#39;account di destinazione, eseguire una richiesta DELETE all&#39;API [!DNL Flow Service].

**Formato API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valore `id` univoco per la connessione da eliminare. |

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

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Seguendo questa esercitazione, hai usato correttamente l&#39;API [!DNL Flow Service] per eliminare gli account di destinazione esistenti. Per ulteriori informazioni sull&#39;utilizzo delle destinazioni, consulta la [panoramica delle destinazioni](/help/destinations/home.md).