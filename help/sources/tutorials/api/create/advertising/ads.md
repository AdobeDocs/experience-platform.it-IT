---
keywords: Experience Platform;home;argomenti popolari;parole chiave;Google adwords;Google AdWords;adwords
solution: Experience Platform
title: Creare una connessione sorgente Google AdWords utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Google AdWords utilizzando l’API del servizio di flusso.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Google AdWords] utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>Il connettore [!DNL Google AdWords] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Questa esercitazione utilizza l’ [!DNL Flow Service] API per seguire i passaggi necessari per la connessione di [!DNL Experience Platform] a [!DNL Google AdWords].

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente ad Ad utilizzando l’ API [!DNL Flow Service] .

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi ad AdWords, è necessario fornire i valori per le seguenti proprietà di connessione:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| `clientCustomerId` | ID cliente client dell’account AdWords. |
| `developerToken` | Il token sviluppatore associato all’account manager. |
| `refreshToken` | Token di aggiornamento ottenuto da [!DNL Google] per autorizzare l’accesso ad AdWords. |
| `clientId` | L&#39;ID client dell&#39;applicazione [!DNL Google] utilizzata per acquisire il token di aggiornamento. |
| `clientSecret` | Il segreto client dell&#39;applicazione [!DNL Google] utilizzata per acquisire il token di aggiornamento. |
| `connectionSpec` | Identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per [!DNL Google AdWords] è: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Per ulteriori informazioni su questi valori, consulta questo [documento Google AdWords](https://developers.google.com/adwords/api/docs/guides/authentication).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL Google AdWords] in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```https
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL Google AdWords], è necessario fornire l’ID univoco della specifica di connessione come parte della richiesta di POST. L&#39;ID della specifica di connessione per [!DNL Google AdWords] è `d771e9c1-4f26-40dc-8617-ce58c4b53702`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.clientCustomerID` | ID cliente del tuo account [!DNL AdWords]. |
| `auth.params.developerToken` | Il token sviluppatore del tuo account [!DNL AdWords]. |
| `auth.params.refreshToken` | Il token di aggiornamento dell&#39;account [!DNL AdWords]. |
| `auth.params.clientID` | L&#39;ID client del tuo account [!DNL AdWords]. |
| `auth.params.clientSecret` | Il segreto client del tuo account [!DNL AdWords]. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Google AdWords]: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso l’identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Google AdWords] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nell&#39;esercitazione successiva per scoprire come [esplorare i sistemi pubblicitari utilizzando l&#39;API del servizio di flusso](../../explore/advertising.md).
