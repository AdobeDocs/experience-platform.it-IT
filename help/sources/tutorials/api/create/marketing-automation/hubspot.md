---
keywords: Experience Platform;home;argomenti popolari;hubspot;Hubspot
solution: Experience Platform
title: Creare una connessione di base HubSpot utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a HubSpot utilizzando l’API del servizio di flusso.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 143f3b4a113c6f36cb1bb0c3624c8503f158a16d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Creare una connessione di base [!DNL HubSpot] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL HubSpot] utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL HubSpot] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL HubSpot], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientId` | L&#39;ID client associato all&#39;applicazione [!DNL HubSpot]. |
| `clientSecret` | Il segreto client associato all&#39;applicazione [!DNL HubSpot]. |
| `accessToken` | Token di accesso ottenuto all’autenticazione iniziale dell’integrazione OAuth. |
| `refreshToken` | Il token di aggiornamento ottenuto all’autenticazione iniziale dell’integrazione OAuth. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL HubSpot] è: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

Per ulteriori informazioni su come iniziare, consulta questo [documento HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL HubSpot] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per [!DNL HubSpot]:

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
| `auth.params.clientId` | L&#39;ID client associato all&#39;applicazione [!DNL HubSpot]. |
| `auth.params.clientSecret` | Il segreto client associato all&#39;applicazione [!DNL HubSpot]. |
| `auth.params.accessToken` | Token di accesso ottenuto all’autenticazione iniziale dell’integrazione OAuth. |
| `auth.params.refreshToken` | Il token di aggiornamento ottenuto all’autenticazione iniziale dell’integrazione OAuth. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL HubSpot]: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso l&#39;identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Seguendo questa esercitazione, hai creato una connessione [!DNL HubSpot] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID connessione nell’esercitazione successiva per scoprire come [esplorare i sistemi di automazione di marketing utilizzando l’ API del servizio di flusso](../../explore/marketing-automation.md).
