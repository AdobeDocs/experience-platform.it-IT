---
keywords: Experience Platform;home;argomenti popolari;salesforce marketing cloud;Marketing Cloud Salesforce
solution: Experience Platform
title: Creare una connessione di base del Marketing Cloud Salesforce utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform al Marketing Cloud Salesforce utilizzando l’API del servizio di flusso.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: c0d750ef61ad2e295568cccabca5c52a758997c2
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 2%

---

# Crea un [!DNL Salesforce Marketing Cloud] connessione di base utilizzando [!DNL Flow Service] API

>[!NOTE]
>
>La [!DNL Salesforce Marketing Cloud] la sorgente è in versione beta. Consulta la sezione [panoramica di origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Salesforce Marketing Cloud] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente l’acquisizione di dati da varie sorgenti e allo stesso tempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

La sezione seguente fornisce informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Salesforce Marketing Cloud] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Salesforce Marketing Cloud], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Server host dell&#39;applicazione. Questo è spesso il tuo sottodominio. **Nota:** Quando immetti il tuo `host` devi solo specificare il sottodominio e non l’intero URL. Ad esempio, se l&#39;URL host è `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, quindi devi solo entrare `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` come valore host. |
| `clientId` | L&#39;ID client associato al [!DNL Salesforce Marketing Cloud] applicazione. |
| `clientSecret` | Il segreto client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce Marketing Cloud] è: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Per ulteriori informazioni su come iniziare, consulta questo articolo [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Salesforce Marketing Cloud] credenziali di autenticazione come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Marketing Cloud base connection",
        "description": "Salesforce Marketing Cloud base connection",
        "auth": {
            "specName": "Client-Id-Secret Based Authentication",
            "params": {
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.clientId` | L&#39;ID client associato al [!DNL Salesforce Marketing Cloud] applicazione. |
| `auth.params.clientSecret` | Il segreto client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |
| `connectionSpec.id` | La [!DNL Salesforce Marketing Cloud] ID specifica di connessione: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso il relativo identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Salesforce Marketing Cloud] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per trasferire i dati di automazione del marketing a Platform utilizzando [!DNL Flow Service] API](../../collect/marketing-automation.md)
