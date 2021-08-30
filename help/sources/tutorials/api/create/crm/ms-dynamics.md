---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Creare una connessione Microsoft Dynamics Base utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Platform a un account Microsoft Dynamics utilizzando l’API del servizio di flusso.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 2%

---

# Creare una connessione di base [!DNL Microsoft Dynamics] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Microsoft Dynamics] (in seguito denominata &quot;[!DNL Dynamics]&quot;) utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettere correttamente Platform a un account Dynamics utilizzando l’ API [!DNL Flow Service] .

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Dynamics], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L&#39;URL del servizio dell&#39;istanza [!DNL Dynamics]. |
| `username` | Il nome utente dell&#39;account utente [!DNL Dynamics]. |
| `password` | Password per il tuo account [!DNL Dynamics]. |
| `servicePrincipalId` | L&#39;ID client del tuo account [!DNL Dynamics]. Questo ID è necessario quando si utilizzano l’entità del servizio e l’autenticazione basata sulle chiavi. |
| `servicePrincipalKey` | Chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizza l’entità del servizio e l’autenticazione basata sulle chiavi. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL Dynamics] è: `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Per ulteriori informazioni su come iniziare, visita [questo [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Dynamics] come parte dei parametri della richiesta.

### Creare una connessione di base [!DNL Dynamics] utilizzando l&#39;autenticazione di base

Per creare una connessione di base [!DNL Dynamics] utilizzando l’autenticazione di base, invia una richiesta POST all’API [!DNL Flow Service] fornendo al contempo i valori per le connessioni `serviceUri`, `username` e `password` della connessione.

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
| `auth.params.serviceUri` | URI di servizio associato all&#39;istanza [!DNL Dynamics]. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Dynamics]. |
| `auth.params.password` | La password associata al tuo account [!DNL Dynamics]. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso l’identificatore univoco (`id`). Questo ID è necessario per esplorare il tuo sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Creare una connessione di base [!DNL Dynamics] utilizzando l&#39;autenticazione basata sulle chiavi dell&#39;entità servizio

Per creare una connessione di base [!DNL Dynamics] utilizzando l’autenticazione basata sulle chiavi dell’entità servizio, invia una richiesta POST all’API [!DNL Flow Service] fornendo al contempo i valori per le connessioni `serviceUri`, `servicePrincipalId` e `servicePrincipalKey`.

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
| `auth.params.serviceUri` | URI di servizio associato all&#39;istanza [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | L&#39;ID client del tuo account [!DNL Dynamics]. Questo ID è necessario quando si utilizzano l’entità del servizio e l’autenticazione basata sulle chiavi. |
| `auth.params.servicePrincipalKey` | Chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizza l’entità del servizio e l’autenticazione basata sulle chiavi. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso l’identificatore univoco (`id`). Questo ID è necessario per esplorare il tuo sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Dynamics] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nell&#39;esercitazione successiva quando imparerai a [esplorare i sistemi CRM utilizzando l&#39;API del servizio di flusso](../../explore/crm.md).
