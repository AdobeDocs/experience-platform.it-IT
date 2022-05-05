---
keywords: Experience Platform;home;argomenti popolari;parole adwords di Google;Google AdWords;adwords
solution: Experience Platform
title: Creare una connessione di base Google AdWords utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform ad Google AdWords utilizzando l’API del servizio di flusso.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 2%

---

# Crea un [!DNL Google AdWords] connessione di base utilizzando [!DNL Flow Service] API

>[!NOTE]
>
>La [!DNL Google AdWords] connettore in versione beta. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo dei connettori con etichetta beta.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Google AdWords] (in appresso denominato &quot;[!DNL AdWords]&quot;) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL AdWords] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL AdWords], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientCustomerId` | L&#39;ID cliente del [!DNL AdWords] conto. |
| `developerToken` | Il token sviluppatore associato all’account manager. |
| `refreshToken` | Il token di aggiornamento ottenuto da [!DNL Google] per autorizzare l&#39;accesso a [!DNL AdWords]. |
| `clientId` | L&#39;ID client del [!DNL Google] applicazione utilizzata per acquisire il token di aggiornamento. |
| `clientSecret` | Il segreto del cliente [!DNL Google] applicazione utilizzata per acquisire il token di aggiornamento. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL AdWords] è: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Per ulteriori informazioni su questi valori, consulta [Documento Google AdWords](https://developers.google.com/adwords/api/docs/guides/authentication).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL AdWords] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL AdWords]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
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
| `auth.params.clientCustomerID` | ID cliente del tuo [!DNL AdWords] conto. |
| `auth.params.developerToken` | Token sviluppatore del tuo [!DNL AdWords] conto. |
| `auth.params.refreshToken` | Il token di aggiornamento del [!DNL AdWords] conto. |
| `auth.params.clientID` | L&#39;ID cliente del tuo [!DNL AdWords] conto. |
| `auth.params.clientSecret` | Il segreto cliente del tuo [!DNL AdWords] conto. |
| `connectionSpec.id` | La [!DNL Google AdWords] ID specifica di connessione: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Google AdWords] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per portare i dati pubblicitari su Platform utilizzando [!DNL Flow Service] API](../../collect/advertising.md)
