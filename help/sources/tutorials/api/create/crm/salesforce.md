---
keywords: Experience Platform;home;argomenti popolari;Salesforce;salesforce
solution: Experience Platform
title: Creare una connessione di base Salesforce utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un account Salesforce utilizzando l’API del servizio di flusso.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 2%

---

# Crea un [!DNL Salesforce] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Salesforce] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente [!DNL Platform] a [!DNL Salesforce] l&#39;utilizzo dell&#39;account [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi a [!DNL Salesforce], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `environmentUrl` | L’URL della [!DNL Salesforce] istanza sorgente. |
| `username` | Il nome utente per il [!DNL Salesforce] account utente. |
| `password` | La password per [!DNL Salesforce] account utente. |
| `securityToken` | Token di sicurezza per [!DNL Salesforce] account utente. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL AdWords] è: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni su come iniziare, visita [presente documento Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Salesforce] credenziali di autenticazione come parte dei parametri della richiesta.


**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Salesforce]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Connection",
        "description": "Connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Salesforce] conto. |
| `auth.params.password` | La password associata al [!DNL Salesforce] conto. |
| `auth.params.securityToken` | Il token di sicurezza associato al [!DNL Salesforce] conto. |
| `connectionSpec.id` | La [!DNL Salesforce] ID specifica di connessione: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il tuo sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Salesforce] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per portare i dati CRM in Platform utilizzando [!DNL Flow Service] API](../../collect/crm.md)
