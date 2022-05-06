---
keywords: Experience Platform;home;argomenti popolari;quadrato;quadrato
title: Creare una connessione di base quadrata utilizzando l’API del servizio di flusso
description: Scopri come collegare Square a Adobe Experience Platform utilizzando l’API del servizio di flusso.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 2%

---

# Crea un [!DNL Square] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Square] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Square] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Square], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| `host` | L’URL della [!DNL Square] istanza. |
| `clientId` | L&#39;ID client associato al [!DNL Square] conto. |
| `clientSecret` | Il segreto client associato al tuo [!DNL Square] conto. |
| `accessToken` | Il token di accesso viene utilizzato per autenticare il [!DNL Square] account con autenticazione OAuth 2.0. Il token di accesso può essere ottenuto da [!DNL Square]. |
| `refreshToken` | Il token di aggiornamento viene utilizzato per generare nuovi token di accesso una volta scaduto il token di accesso corrente. Il token di aggiornamento può essere ottenuto da [!DNL Square]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Square] è: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Per ulteriori informazioni su queste credenziali e su come ottenerle, consulta la [[!DNL Square] documentazione su OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Square] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Square]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.host` | L’URL della [!DNL Square] istanza. |
| `auth.params.clientId` | L&#39;ID client associato al [!DNL Square] conto. |
| `auth.params.clientSecret` | Il segreto client associato al tuo [!DNL Square] conto. |
| `auth.params.accessToken` | Il token di accesso viene utilizzato per autenticare il [!DNL Square] account con autenticazione OAuth 2.0. Il token di accesso può essere ottenuto da [!DNL Square]. |
| `auth.params.refreshToken` | Il token di aggiornamento viene utilizzato per generare nuovi token di accesso una volta scaduto il token di accesso corrente. Il token di aggiornamento può essere ottenuto da [!DNL Square]. |
| `connectionSpec.id` | La [!DNL Square] ID specifica di connessione: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso il relativo identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Square] connessione tramite [!DNL Flow Service] e hanno ottenuto il valore ID univoco della connessione. Puoi usare questo ID nell&#39;esercitazione successiva per scoprire come [esplorare l’applicazione di pagamento tramite l’API del servizio di flusso](../../explore/payments.md).
