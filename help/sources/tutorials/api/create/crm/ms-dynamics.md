---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Creare una connessione di base Microsoft Dynamics utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come connettere Platform a un account Microsoft Dynamics utilizzando l’API del servizio Flusso.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 2%

---

# Creare un [!DNL Microsoft Dynamics] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Microsoft Dynamics] (in seguito denominati &quot;[!DNL Dynamics]&quot;) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettere correttamente Platform a un account Dynamics utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi a [!DNL Dynamics], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L’URL del servizio del tuo [!DNL Dynamics] dell&#39;istanza. |
| `username` | Il nome utente per il [!DNL Dynamics] account utente. |
| `password` | La password per [!DNL Dynamics] account. |
| `servicePrincipalId` | L’ID client del tuo [!DNL Dynamics] account. Questo ID è necessario quando si utilizza l’entità servizio e l’autenticazione basata su chiave. |
| `servicePrincipalKey` | Chiave segreta dell&#39;entità servizio. Questa credenziale è necessaria quando si utilizza l&#39;entità servizio e l&#39;autenticazione basata su chiave. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Dynamics] è: `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Per ulteriori informazioni su come iniziare, visita [questo [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Dynamics] credenziali di autenticazione come parte dei parametri della richiesta.

### Creare un [!DNL Dynamics] connessione di base tramite autenticazione di base

Per creare un [!DNL Dynamics] connessione di base tramite autenticazione di base, invia una richiesta POST al [!DNL Flow Service] fornendo valori per la connessione `serviceUri`, `username`, e `password`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | L&#39;URI del servizio associato a [!DNL Dynamics] dell&#39;istanza. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Dynamics] account. |
| `auth.params.password` | La password associata al tuo [!DNL Dynamics] account. |
| `connectionSpec.id` | Il [!DNL Dynamics] ID specifica di connessione: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Creare un [!DNL Dynamics] connessione di base tramite autenticazione basata su chiave dell&#39;entità servizio

Per creare un [!DNL Dynamics] connessione di base utilizzando l&#39;autenticazione basata su chiave dell&#39;entità servizio, effettuare una richiesta POST al [!DNL Flow Service] fornendo valori per la connessione `serviceUri`, `servicePrincipalId`, e `servicePrincipalKey`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | L&#39;URI del servizio associato a [!DNL Dynamics] dell&#39;istanza. |
| `auth.params.servicePrincipalId` | L’ID client del tuo [!DNL Dynamics] account. Questo ID è necessario quando si utilizza l’entità servizio e l’autenticazione basata su chiave. |
| `auth.params.servicePrincipalKey` | Chiave segreta dell&#39;entità servizio. Questa credenziale è necessaria quando si utilizza l&#39;entità servizio e l&#39;autenticazione basata su chiave. |
| `connectionSpec.id` | Il [!DNL Dynamics] ID specifica di connessione: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Microsoft Dynamics] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati CRM in Platform utilizzando [!DNL Flow Service] API](../../collect/crm.md)
