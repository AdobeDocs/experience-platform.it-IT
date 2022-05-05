---
keywords: Experience Platform;home;argomenti popolari;Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: Creare una connessione Salesforce Service Cloud Source utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Salesforce Service Cloud utilizzando l’API del servizio di flusso.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Crea un [!DNL Salesforce Service Cloud] connessione di origine tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Salesforce Service Cloud] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Salesforce Service Cloud] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Salesforce Service Cloud], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `username` | Nome utente per il tuo [!DNL Salesforce Service Cloud] account utente. |
| `password` | La password [!DNL Salesforce Service Cloud] conto. |
| `securityToken` | Token di sicurezza per il [!DNL Salesforce Service Cloud] conto. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce Service Cloud] è: `b66ab34-8619-49cb-96d1-39b37ede86ea`. |

Per ulteriori informazioni su come iniziare, consulta [questo documento Cloud di Salesforce Service](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Salesforce Service Cloud] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Salesforce Service Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Salesforce Service Cloud] conto. |
| `auth.params.password` | La password associata al [!DNL Salesforce Service Cloud] conto. |
| `auth.params.securityToken` | Il token di sicurezza associato al [!DNL Salesforce Service Cloud] conto. |
| `connectionSpec.id` | La [!DNL Salesforce Service Cloud] ID specifica di connessione: `b66ab34-8619-49cb-96d1-39b37ede86ea` |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il tuo sistema CRM nel passaggio successivo.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Salesforce Service Cloud] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per portare i dati di successo dei clienti su Platform utilizzando [!DNL Flow Service] API](../../collect/customer-success.md)
