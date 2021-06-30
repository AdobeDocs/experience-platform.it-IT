---
keywords: Experience Platform;home;argomenti popolari;bigquery;Google;google;Google BigQuery
solution: Experience Platform
title: Creare una connessione Google BigQuery Base utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Google BigQuery utilizzando l’API del servizio di flusso.
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: e8c6620a6d2447a577bd56192030ff4353c62c62
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Creare una connessione di base [!DNL Google BigQuery] utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>Il connettore [!DNL Google BigQuery] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Google BigQuery] (in seguito denominata &quot;[!DNL BigQuery]&quot;) utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL BigQuery] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Per consentire a [!DNL Flow Service] di connettersi a [!DNL BigQuery] Platform, è necessario fornire i seguenti valori di autenticazione OAuth 2.0:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `project` | ID del progetto [!DNL BigQuery] predefinito su cui eseguire la query. |
| `clientID` | Il valore ID utilizzato per generare il token di aggiornamento. |
| `clientSecret` | Il valore segreto utilizzato per generare il token di aggiornamento. |
| `refreshToken` | Il token di aggiornamento ottenuto da [!DNL Google] utilizzato per autorizzare l&#39;accesso a [!DNL BigQuery]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL BigQuery] è: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

Per ulteriori informazioni su questi valori, consulta questo [[!DNL BigQuery] documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL BigQuery] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per [!DNL BigQuery]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.project` | ID del progetto [!DNL BigQuery] predefinito da interrogare. contro. |
| `auth.params.clientId` | Il valore ID utilizzato per generare il token di aggiornamento. |
| `auth.params.clientSecret` | Il valore client utilizzato per generare il token di aggiornamento. |
| `auth.params.refreshToken` | Il token di aggiornamento ottenuto da [!DNL Google] utilizzato per autorizzare l&#39;accesso a [!DNL BigQuery]. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Google BigQuery]: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso l’identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL BigQuery] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. È possibile utilizzare questo ID connessione nell&#39;esercitazione successiva per imparare a [esplorare i database o i sistemi NoSQL utilizzando l&#39;API del servizio di flusso](../../explore/database-nosql.md).
