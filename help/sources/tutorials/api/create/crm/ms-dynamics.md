---
keywords: ' Experience Platform;home;argomenti più comuni;Microsoft Dynamics;microsoft dDynamics;dDynamics;Dynamics'
solution: Experience Platform
title: Creare un connettore Microsoft Dynamics utilizzando l'API del servizio di flusso
topic: overview
type: Tutorial
description: Questa esercitazione utilizza l'API del servizio di flusso per guidarti attraverso i passaggi necessari per connettere la piattaforma a un account Microsoft Dynamics (in seguito denominato "Dynamics") per la raccolta dei dati CRM.
translation-type: tm+mt
source-git-commit: 75566ef0dc45f59b47af0b85f4692c2496e53f29
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 2%

---


# Creare un connettore [!DNL Microsoft Dynamics] utilizzando l&#39;API [!DNL Flow Service]

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API [!DNL Flow Service] per guidarti attraverso i passaggi necessari per connettere la piattaforma a un account [!DNL Microsoft Dynamics] (in seguito denominato &quot;Dynamics&quot;) per la raccolta dei dati CRM.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  Experience Platform consente l&#39;acquisizione di dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Piattaforma.
* [Sandbox](../../../../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettere correttamente la piattaforma a un account Dynamics utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Dynamics], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L&#39;URL del servizio dell&#39;istanza [!DNL Dynamics]. |
| `username` | Il nome utente per l&#39;account utente [!DNL Dynamics]. |
| `password` | La password dell&#39;account [!DNL Dynamics]. |
| `servicePrincipalId` | L&#39;ID client dell&#39;account [!DNL Dynamics]. Questo ID è richiesto quando si utilizzano l&#39;entità del servizio e l&#39;autenticazione basata sulle chiavi. |
| `servicePrincipalKey` | La chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizzano l&#39;entità del servizio e l&#39;autenticazione basata sulle chiavi. |

Per ulteriori informazioni su come iniziare, visitare [this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi del Experience Platform .

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a1/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API di Experience Platform, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in  Experience Platform, incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL Dynamics], in quanto può essere utilizzata per creare più flussi di dati per inserire dati diversi.

### Creare una connessione [!DNL Dynamics] utilizzando l&#39;autenticazione di base

Per creare una connessione [!DNL Dynamics] utilizzando l&#39;autenticazione di base, effettuare una richiesta di POST all&#39;API [!DNL Flow Service] fornendo al contempo i valori per le connessioni `serviceUri`, `username` e `password`.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL Dynamics], è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta di POST. L&#39;ID della specifica di connessione per [!DNL Dynamics] è `38ad80fe-8b06-4938-94f4-d4ee80266b07`.

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
| `auth.params.serviceUri` | URI del servizio associato all&#39;istanza [!DNL Dynamics]. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Dynamics]. |
| `auth.params.password` | La password associata al tuo account [!DNL Dynamics]. |
| `connectionSpec.id` | Specifica di connessione `id` dell&#39;account [!DNL Dynamics] recuperato nel passaggio precedente. |

**Risposta**

Una risposta corretta restituisce la nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Creare una connessione [!DNL Dynamics] utilizzando l&#39;autenticazione basata sulle chiavi dell&#39;entità del servizio

Per creare una connessione [!DNL Dynamics] utilizzando l&#39;autenticazione basata sulle chiavi dell&#39;entità del servizio, effettuare una richiesta di POST all&#39;API [!DNL Flow Service] fornendo al contempo i valori per le connessioni `serviceUri`, `servicePrincipalId` e `servicePrincipalKey`.

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
| `auth.params.serviceUri` | URI del servizio associato all&#39;istanza [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | L&#39;ID client dell&#39;account [!DNL Dynamics]. Questo ID è richiesto quando si utilizzano l&#39;entità del servizio e l&#39;autenticazione basata sulle chiavi. |
| `auth.params.servicePrincipalKey` | La chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizzano l&#39;entità del servizio e l&#39;autenticazione basata sulle chiavi. |

**Risposta**

Una risposta corretta restituisce la nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Dynamics] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nell&#39;esercitazione successiva per imparare a esplorare i sistemi CRM utilizzando l&#39;API del servizio di flusso](../../explore/crm.md).[