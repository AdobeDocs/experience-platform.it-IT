---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;eliminare account di destinazione;eliminare;api
solution: Experience Platform
title: Eliminare un account di destinazione utilizzando l’API del servizio di flusso
type: Tutorial
description: Scopri come eliminare un account di destinazione utilizzando l’API del servizio di flusso.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: c93a054174bc68ecedf67599ef61ad0b41a56ada
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# Eliminare un account di destinazione utilizzando l’API del servizio di flusso

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

Prima di attivare i dati, è necessario connettersi alla destinazione impostando prima un account di destinazione. Questa esercitazione descrive i passaggi per eliminare gli account di destinazione che non sono più necessari utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>L’eliminazione degli account di destinazione è attualmente supportata solo nell’API del servizio di flusso. Gli account di destinazione non possono essere eliminati utilizzando l&#39;interfaccia utente di Experience Platform.

## Introduzione {#get-started}

Questa esercitazione richiede un ID di connessione valido. L&#39;ID di connessione rappresenta la connessione dell&#39;account alla destinazione. Se non disponi di un ID di connessione valido, seleziona la destinazione scelta dalla [catalogo delle destinazioni](../catalog/overview.md) e seguire i passi descritti in [connettersi alla destinazione](../ui/connect-destination.md) prima di provare questa esercitazione.

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Destinazioni](../home.md): [!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eliminare correttamente un account di destinazione utilizzando [!DNL Flow Service] API.

### Lettura di chiamate API di esempio {#reading-sample-api-calls}

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste {#gather-values-for-required-headers}

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se la `x-sandbox-name` intestazione non specificata, le richieste vengono risolte sotto `prod` sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Trova l&#39;ID di connessione dell&#39;account di destinazione che desideri eliminare {#find-connection-id}

>[!NOTE]
>Questa esercitazione utilizza la funzione [Destinazione dell&#39;aeromobile](../catalog/mobile-engagement/airship-attributes.md) ad esempio, ma i passaggi descritti si applicano a uno qualsiasi dei [destinazioni disponibili](../catalog/overview.md).

Il primo passaggio nell&#39;eliminazione di un account di destinazione consiste nell&#39;individuare l&#39;ID di connessione corrispondente all&#39;account di destinazione che si desidera eliminare.

Nell’interfaccia utente di Experience Platform, seleziona **[!UICONTROL Destinazioni]** > **[!UICONTROL Account]** e seleziona l&#39;account da eliminare selezionando il numero nel **[!UICONTROL Destinazioni]** colonna.

![Selezionare l&#39;account di destinazione da eliminare](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "imsOrgId": "{IMS_ORG}",
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
>Prima di eliminare l&#39;account di destinazione, è necessario eliminare tutti i flussi di dati esistenti nell&#39;account di destinazione.
>Per eliminare i flussi di dati esistenti, fai riferimento alle pagine seguenti:
>* [Utilizzare l’interfaccia utente di Experience Platform](../ui/delete-destinations.md) eliminare i flussi di dati esistenti;
>* [Utilizzare l’API del servizio di flusso](delete-destination-dataflow.md) per eliminare i flussi di dati esistenti.


Una volta ottenuto un ID di connessione e verificato che non siano presenti flussi di dati per l’account di destinazione, esegui una richiesta DELETE al [!DNL Flow Service] API.

**Formato API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | L&#39;unico `id` valore della connessione che si desidera eliminare. |

**Richiesta**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto. Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) alla connessione. L’API restituirà un errore HTTP 404 (Non trovato) che indica che l’account di destinazione è stato eliminato.

## Gestione degli errori API {#api-error-handling}

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!DNL Flow Service] API per eliminare gli account di destinazione esistenti. Per ulteriori informazioni sull’utilizzo delle destinazioni, consulta [panoramica sulle destinazioni](/help/destinations/home.md).