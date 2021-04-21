---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Creare una connessione Microsoft Dynamics Source utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Platform a un account Microsoft Dynamics utilizzando l’API del servizio di flusso.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 2%

---

# Creare una connessione sorgente [!DNL Microsoft Dynamics] utilizzando l&#39;API [!DNL Flow Service]

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Questa esercitazione utilizza l’ API [!DNL Flow Service] per seguire i passaggi necessari per collegare Platform a un account [!DNL Microsoft Dynamics] (in seguito denominato &quot;Dynamics&quot;) tramite l’API del servizio di flusso.

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

Per ulteriori informazioni su come iniziare, visita [questo [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in Experience Platform, incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL Dynamics] in quanto può essere utilizzata per creare più flussi di dati per inserire dati diversi.

### Creare una connessione [!DNL Dynamics] utilizzando l&#39;autenticazione di base

Per creare una connessione [!DNL Dynamics] utilizzando l’autenticazione di base, invia una richiesta POST all’API [!DNL Flow Service] fornendo al contempo i valori per le connessioni `serviceUri`, `username` e `password`.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL Dynamics], è necessario fornire l’ID univoco della specifica di connessione come parte della richiesta di POST. L&#39;ID della specifica di connessione per [!DNL Dynamics] è `38ad80fe-8b06-4938-94f4-d4ee80266b07`.

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
| `connectionSpec.id` | Specifica di connessione `id` dell&#39;account [!DNL Dynamics] recuperato nel passaggio precedente. |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso l’identificatore univoco (`id`). Questo ID è necessario per esplorare il tuo sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Creare una connessione [!DNL Dynamics] utilizzando l&#39;autenticazione basata sulle chiavi dell&#39;entità del servizio

Per creare una connessione [!DNL Dynamics] utilizzando l’autenticazione basata sulle chiavi dell’entità servizio, invia una richiesta POST all’API [!DNL Flow Service] fornendo al contempo i valori per le connessioni `serviceUri`, `servicePrincipalId` e `servicePrincipalKey`.

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
