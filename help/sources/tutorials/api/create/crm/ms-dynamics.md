---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Microsoft Dynamics utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 5839e4695589455bd32b6e3e33a7c377343f920d
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---


# Creare un [!DNL Microsoft Dynamics] connettore utilizzando l&#39; [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per guidarti attraverso i passaggi necessari per connettersi [!DNL Platform] a un account [!DNL Microsoft Dynamics] (in seguito denominato &quot;Dynamics&quot;) per la raccolta dei dati CRM.

Se si preferisce utilizzare l&#39;interfaccia utente in [!DNL Experience Platform], l&#39;esercitazione [dell&#39;interfaccia utente del connettore di origine](../../../ui/create/crm/dynamics.md) Dynamics fornisce istruzioni dettagliate per eseguire azioni simili.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md): E[!DNL xperience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente [!DNL Platform] a un account Dynamics utilizzando l&#39; [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] collegarsi a [!DNL Dynamics], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L’URL del servizio dell’ [!DNL Dynamics] istanza. |
| `username` | Nome utente per l’account [!DNL Dynamics] utente. |
| `password` | La password del tuo [!DNL Dynamics] account. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)di Dynamics.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti al gruppo [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Cercare le specifiche di connessione

Prima [!DNL Platform] di connettersi a un [!DNL Dynamics] account, è necessario verificare l&#39;esistenza delle specifiche di connessione per [!DNL Dynamics]. Se le specifiche di connessione non esistono, non è possibile stabilire una connessione.

Ogni origine disponibile dispone di un proprio set di specifiche di connessione per descrivere le proprietà del connettore, ad esempio i requisiti di autenticazione. Potete cercare le specifiche di connessione [!DNL Dynamics] eseguendo una richiesta GET e utilizzando i parametri di query.

**Formato API**

L&#39;invio di una richiesta GET senza parametri di query restituirà le specifiche di connessione per tutte le origini disponibili. È possibile includere la query `property=name=="dynamics-online"` per ottenere informazioni specifiche per [!DNL Dynamics].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**Richiesta**

La richiesta seguente recupera le specifiche di connessione per [!DNL Dynamics].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce le specifiche di connessione per [!DNL Dynamics], incluso il relativo identificatore univoco (`id`). Questo ID è richiesto nel passaggio successivo per creare una connessione di base.

```json
{
    "items": [
        {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "name": "dynamics-online",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for Dynamics-Online",
                    "settings": {
                        "authenticationType": "Office365",
                        "deploymentType": "Online"
                    },
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to dynamics-online",
                        "properties": {
                            "serviceUri": {
                                "type": "string",
                                "description": "The service URL of your Dynamics instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "serviceUri"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Creazione di una connessione di base

Una connessione di base specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione di base per [!DNL Dynamics] account, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

Eseguite la seguente richiesta POST per creare una connessione di base.

**Formato API**

```http
POST /connections
```

**Richiesta**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics Base Connection",
        "description": "Base connection for Dynamics account",
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
| `auth.params.serviceUri` | URI del servizio associato all’ [!DNL Dynamics] istanza. |
| `auth.params.username` | Nome utente associato al tuo [!DNL Dynamics] account. |
| `auth.params.password` | La password associata al tuo [!DNL Dynamics] account. |
| `connectionSpec.id` | Specifica di connessione `id` dell’ [!DNL Dynamics] account recuperato nel passaggio precedente. |

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco (`id`) della connessione di base. Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione di base per il tuo [!DNL Dynamics] account utilizzando le API e un ID univoco è stato ottenuto come parte del corpo della risposta. Puoi utilizzare questo ID di connessione di base nell&#39;esercitazione successiva per imparare a [esplorare i sistemi CRM utilizzando l&#39;API](../../explore/crm.md)del servizio di flusso.