---
keywords: ' Experience Platform;home;argomenti popolari;Salesforce;salesforce'
solution: Experience Platform
title: Creare un connettore Salesforce utilizzando l'API del servizio di flusso
topic: overview
type: Tutorial
description: Questa esercitazione utilizza l'API del servizio di flusso per guidarti nei passaggi necessari per connettere la piattaforma a un account Salesforce per la raccolta dei dati CRM.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 2%

---


# Creare un connettore [!DNL Salesforce] utilizzando l&#39;API [!DNL Flow Service]

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API [!DNL Flow Service] per guidarti attraverso i passaggi necessari per connettersi [!DNL Platform] a un account [!DNL Salesforce] per la raccolta dei dati CRM.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente [!DNL Platform] a un account [!DNL Salesforce] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Salesforce], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `environmentUrl` | L&#39;URL dell&#39;istanza di origine [!DNL Salesforce]. |
| `username` | Il nome utente per l&#39;account utente [!DNL Salesforce]. |
| `password` | La password per l&#39;account utente [!DNL Salesforce]. |
| `securityToken` | Token di sicurezza per l&#39;account utente [!DNL Salesforce]. |

Per ulteriori informazioni su come iniziare, visita [questo documento Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL Salesforce], in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL Salesforce], è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta di POST. L&#39;ID della specifica di connessione per [!DNL Salesforce] è `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Salesforce]. |
| `auth.params.password` | La password associata al tuo account [!DNL Salesforce]. |
| `auth.params.securityToken` | Token di sicurezza associato all&#39;account [!DNL Salesforce]. |
| `connectionSpec.id` | Specifica di connessione `id` dell&#39;account [!DNL Salesforce] recuperato nel passaggio precedente. |

**Risposta**

Una risposta corretta restituisce la nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Salesforce] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nell&#39;esercitazione successiva per imparare a esplorare i sistemi CRM utilizzando l&#39;API del servizio di flusso](../../explore/crm.md).[