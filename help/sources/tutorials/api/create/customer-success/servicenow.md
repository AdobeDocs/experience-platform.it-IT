---
keywords: Experience Platform;home;argomenti popolari;servicenow;ServiceNow
solution: Experience Platform
title: Creare una connessione di base ServiceNow utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un server ServiceNow utilizzando l’API del servizio di flusso.
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 2%

---

# Crea un [!DNL ServiceNow] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Google ServiceNow] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a un [!DNL ServiceNow] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi a [!DNL ServiceNow], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `endpoint` | Il punto finale del [!DNL ServiceNow] server. |
| `username` | Il nome utente utilizzato per connettersi al [!DNL ServiceNow] server per l&#39;autenticazione. |
| `password` | Password per la connessione al [!DNL ServiceNow] server per l&#39;autenticazione. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL ServiceNow] è: `eb13cb25-47ab-407f-ba89-c0125281c563`. |

Per ulteriori informazioni su come iniziare, consulta [documento ServiceNow](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL ServiceNow] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL ServiceNow]:

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for service-now",
        "description": "Connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.server` | L&#39;endpoint della [!DNL ServiceNow] server. |
| `auth.params.username` | Il nome utente utilizzato per connettersi al [!DNL ServiceNow] server per l&#39;autenticazione. |
| `auth.params.password` | Password per la connessione al [!DNL ServiceNow] server per l&#39;autenticazione. |
| `connectionSpec.id` | La [!DNL ServiceNow] ID specifica di connessione: `eb13cb25-47ab-407f-ba89-c0125281c563` |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il tuo sistema CRM nel passaggio successivo.

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL ServiceNow] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per portare i dati di successo dei clienti su Platform utilizzando [!DNL Flow Service] API](../../collect/customer-success.md)
