---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Google AdWords utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 11431ffcfc2204931fe3e863bfadc7878a40b49c
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 2%

---


# Creare un [!DNL Google AdWords] connettore utilizzando l&#39; [!DNL Flow Service] API

>[!NOTE]
>Il [!DNL Google AdWords] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per guidarvi nei passaggi da seguire per la connessione [!DNL Experience Platform] a [!DNL Google AdWords].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrete conoscere per collegarvi correttamente ad Ad utilizzando l&#39; [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] connettersi ad AdWords, è necessario fornire valori per le seguenti proprietà di connessione:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| ID cliente client | L&#39;ID cliente client dell&#39;account AdWords. |
| Token sviluppatore | Token sviluppatore associato all&#39;account manager. |
| Aggiorna token | Token di aggiornamento ottenuto da [!DNL Google] per autorizzare l&#39;accesso ad AdWords. |
| ID client | L&#39;ID client dell&#39; [!DNL Google] applicazione utilizzata per acquisire il token di aggiornamento. |
| Segreto cliente | Il segreto client dell&#39; [!DNL Google] applicazione utilizzata per acquisire il token di aggiornamento. |
| ID specifica connessione | Identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per [!DNL Google AdWords] è: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Per ulteriori informazioni su questi valori, consulta questo documento [](https://developers.google.com/adwords/api/docs/guides/authentication)Google AdWords.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per [!DNL Google AdWords] account, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una nuova connessione AdWords, configurata dalle proprietà fornite nel payload:


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
| `auth.params.clientCustomerID` | L&#39;ID cliente cliente del tuo [!DNL AdWords] account. |
| `auth.params.developerToken` | Token sviluppatore dell’ [!DNL AdWords] account. |
| `auth.params.refreshToken` | Token di aggiornamento dell’ [!DNL AdWords] account. |
| `auth.params.clientID` | L&#39;ID cliente del tuo [!DNL AdWords] account. |
| `auth.params.clientSecret` | Il segreto cliente del tuo [!DNL AdWords] account. |
| `connectionSpec.id` | ID specifica [!DNL Google AdWords] connessione: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Google AdWords] connessione utilizzando l&#39; [!DNL Flow Service] API e hai ottenuto il valore ID univoco della connessione. Potete utilizzare questo ID nell&#39;esercitazione successiva per apprendere come [esplorare i sistemi pubblicitari mediante l&#39;API](../../explore/advertising.md)di servizio di flusso.
