---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Creare una connessione Microsoft Dynamics Base utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Platform a un account Microsoft Dynamics utilizzando l’API del servizio di flusso.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 2%

---

# Crea un [!DNL Microsoft Dynamics] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Microsoft Dynamics] (in appresso denominato &quot;[!DNL Dynamics]&quot;) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegare correttamente Platform a un account Dynamics utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi a [!DNL Dynamics], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L’URL di servizio della [!DNL Dynamics] istanza. |
| `username` | Nome utente per il [!DNL Dynamics] account utente. |
| `password` | La password [!DNL Dynamics] conto. |
| `servicePrincipalId` | L&#39;ID cliente del tuo [!DNL Dynamics] conto. Questo ID è necessario quando si utilizzano l’entità del servizio e l’autenticazione basata sulle chiavi. |
| `servicePrincipalKey` | Chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizza l’entità del servizio e l’autenticazione basata sulle chiavi. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Dynamics] è: `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Per ulteriori informazioni su come iniziare, visita [questo [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Dynamics] credenziali di autenticazione come parte dei parametri della richiesta.

### Crea un [!DNL Dynamics] connessione di base tramite autenticazione di base

Per creare una [!DNL Dynamics] connessione di base utilizzando l’autenticazione di base, effettuare una richiesta di POST al [!DNL Flow Service] API fornendo al contempo i valori per la connessione `serviceUri`, `username`e `password`.

**Formato API**

```http
POST /connections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.serviceUri` | L&#39;URI di servizio associato al [!DNL Dynamics] istanza. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Dynamics] conto. |
| `auth.params.password` | La password associata al [!DNL Dynamics] conto. |
| `connectionSpec.id` | La [!DNL Dynamics] ID specifica di connessione: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il tuo sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Crea un [!DNL Dynamics] connessione di base tramite autenticazione basata su chiave dell&#39;entità servizio

Per creare una [!DNL Dynamics] connessione di base utilizzando l&#39;autenticazione basata su chiave principale del servizio, effettuare una richiesta di POST al [!DNL Flow Service] API fornendo al contempo i valori per la connessione `serviceUri`, `servicePrincipalId`e `servicePrincipalKey`.

**Formato API**

```http
POST /connections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.serviceUri` | L&#39;URI di servizio associato al [!DNL Dynamics] istanza. |
| `auth.params.servicePrincipalId` | L&#39;ID cliente del tuo [!DNL Dynamics] conto. Questo ID è necessario quando si utilizzano l’entità del servizio e l’autenticazione basata sulle chiavi. |
| `auth.params.servicePrincipalKey` | Chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizza l’entità del servizio e l’autenticazione basata sulle chiavi. |
| `connectionSpec.id` | La [!DNL Dynamics] ID specifica di connessione: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il tuo sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Microsoft Dynamics] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per portare i dati CRM in Platform utilizzando [!DNL Flow Service] API](../../collect/crm.md)
