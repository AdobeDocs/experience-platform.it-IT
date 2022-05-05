---
keywords: Experience Platform;home;argomenti popolari;hubspot;Hubspot
solution: Experience Platform
title: Creare una connessione di base HubSpot utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a HubSpot utilizzando l’API del servizio di flusso.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 1f2ae53e5503618b7ac12628923b30c457fd17e2
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 2%

---

# Crea un [!DNL HubSpot] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL HubSpot] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL HubSpot] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL HubSpot], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientId` | L&#39;ID client associato al [!DNL HubSpot] applicazione. |
| `clientSecret` | Il segreto client associato al tuo [!DNL HubSpot] applicazione. |
| `accessToken` | Token di accesso ottenuto all’autenticazione iniziale dell’integrazione OAuth. |
| `refreshToken` | Il token di aggiornamento ottenuto all’autenticazione iniziale dell’integrazione OAuth. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL HubSpot] è: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

Per ulteriori informazioni su come iniziare, consulta questo articolo [Documento HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL HubSpot] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL HubSpot]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for HubSpot",
        "description": "connection for HubSpot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.clientId` | L&#39;ID client associato al [!DNL HubSpot] applicazione. |
| `auth.params.clientSecret` | Il segreto client associato al tuo [!DNL HubSpot] applicazione. |
| `auth.params.accessToken` | Token di accesso ottenuto all’autenticazione iniziale dell’integrazione OAuth. |
| `auth.params.refreshToken` | Il token di aggiornamento ottenuto all’autenticazione iniziale dell’integrazione OAuth. |
| `connectionSpec.id` | La [!DNL HubSpot] ID specifica di connessione: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso il relativo identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL HubSpot] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per trasferire i dati di automazione del marketing a Platform utilizzando [!DNL Flow Service] API](../../collect/marketing-automation.md)
