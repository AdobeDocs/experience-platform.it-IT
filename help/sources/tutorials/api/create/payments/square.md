---
keywords: Experience Platform;home;argomenti popolari;Square;square;square;home;popular topic;Square;square
title: Creare una connessione di base quadrata utilizzando l’API del servizio Flusso
description: Scopri come collegare Square a Adobe Experience Platform utilizzando l’API del servizio Flow.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 2%

---

# Creare un [!DNL Square] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Square] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Square] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Square], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| `host` | L’URL del [!DNL Square] dell&#39;istanza. |
| `clientId` | L’ID client associato al tuo [!DNL Square] account. |
| `clientSecret` | Il segreto client associato al tuo [!DNL Square] account. |
| `accessToken` | Il token di accesso viene utilizzato per autenticare il [!DNL Square] con autenticazione OAuth 2.0. Il token di accesso può essere ottenuto da [!DNL Square]. |
| `refreshToken` | Il token di aggiornamento viene utilizzato per generare nuovi token di accesso dopo la scadenza del token di accesso corrente. Il token di aggiornamento può essere ottenuto da [!DNL Square]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Square] è: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Per ulteriori informazioni su queste credenziali e su come ottenerle, vedi la [[!DNL Square] documentazione su OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Square] credenziali di autenticazione come parte dei parametri della richiesta.

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
| `auth.params.host` | L’URL del [!DNL Square] dell&#39;istanza. |
| `auth.params.clientId` | L’ID client associato al tuo [!DNL Square] account. |
| `auth.params.clientSecret` | Il segreto client associato al tuo [!DNL Square] account. |
| `auth.params.accessToken` | Il token di accesso viene utilizzato per autenticare il [!DNL Square] con autenticazione OAuth 2.0. Il token di accesso può essere ottenuto da [!DNL Square]. |
| `auth.params.refreshToken` | Il token di aggiornamento viene utilizzato per generare nuovi token di accesso dopo la scadenza del token di accesso corrente. Il token di aggiornamento può essere ottenuto da [!DNL Square]. |
| `connectionSpec.id` | Il [!DNL Square] ID specifica di connessione: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Square] connessione tramite [!DNL Flow Service] e hanno ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nel prossimo tutorial mentre apprendi come [esplorare l’applicazione dei pagamenti tramite l’API del servizio Flusso](../../explore/payments.md).
