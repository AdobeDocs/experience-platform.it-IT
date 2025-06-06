---
keywords: Experience Platform;home;argomenti popolari;quadrato;;home;popular topic;Square;square
title: Creare una connessione di base quadrata utilizzando l’API del servizio Flusso
description: Scopri come collegare Square a Adobe Experience Platform utilizzando l’API del servizio Flow.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 4%

---

# Creare una connessione di base [!DNL Square] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Square] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Square] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Square], è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| --- | --- |
| `host` | URL dell&#39;istanza [!DNL Square]. |
| `clientId` | ID client associato all&#39;account [!DNL Square]. |
| `clientSecret` | Il segreto client associato al tuo account [!DNL Square]. |
| `accessToken` | Il token di accesso viene utilizzato per autenticare l&#39;account [!DNL Square] con autenticazione OAuth 2.0. Il token di accesso può essere ottenuto da [!DNL Square]. |
| `refreshToken` | Il token di aggiornamento viene utilizzato per generare nuovi token di accesso dopo la scadenza del token di accesso corrente. Il token di aggiornamento può essere ottenuto da [!DNL Square]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Square]: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Per ulteriori informazioni su queste credenziali e su come ottenerle, consulta la [[!DNL Square] documentazione su OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Experience Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID connessione di base, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Square] come parte dei parametri della richiesta.

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
| `auth.params.host` | URL dell&#39;istanza [!DNL Square]. |
| `auth.params.clientId` | ID client associato all&#39;account [!DNL Square]. |
| `auth.params.clientSecret` | Il segreto client associato al tuo account [!DNL Square]. |
| `auth.params.accessToken` | Il token di accesso viene utilizzato per autenticare l&#39;account [!DNL Square] con autenticazione OAuth 2.0. Il token di accesso può essere ottenuto da [!DNL Square]. |
| `auth.params.refreshToken` | Il token di aggiornamento viene utilizzato per generare nuovi token di accesso dopo la scadenza del token di accesso corrente. Il token di aggiornamento può essere ottenuto da [!DNL Square]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Square]: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso l&#39;identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Square] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. È possibile utilizzare questo ID nell&#39;esercitazione successiva mentre si apprende come [esplorare l&#39;applicazione di pagamento utilizzando l&#39;API del servizio Flusso](../../explore/payments.md).
