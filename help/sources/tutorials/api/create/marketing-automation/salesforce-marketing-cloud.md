---
keywords: Experience Platform;home;argomenti popolari;salesforce marketing cloud;Marketing Cloud Salesforce
solution: Experience Platform
title: Creare una connessione di base del Marketing Cloud Salesforce utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform al Marketing Cloud Salesforce utilizzando l’API del servizio di flusso.
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# Creare una connessione di base [!DNL Salesforce Marketing Cloud] utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>L&#39;origine [!DNL Salesforce Marketing Cloud] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo delle sorgenti con etichetta beta, consulta la [panoramica sulle sorgenti](../../../../home.md#terms-and-conditions) .

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Salesforce Marketing Cloud] utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

La sezione seguente fornisce informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Salesforce Marketing Cloud] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Salesforce Marketing Cloud], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Server host dell&#39;applicazione. Questo è spesso il tuo sottodominio. |
| `clientId` | L&#39;ID client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `clientSecret` | Il segreto client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL Salesforce Marketing Cloud] è: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Salesforce Marketing Cloud] come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per [!DNL Salesforce Marketing Cloud]:

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
            "id": "cea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.clientId` | L&#39;ID client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `auth.params.clientSecret` | Il segreto client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Salesforce Marketing Cloud]: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso l&#39;identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Seguendo questa esercitazione, hai creato una connessione [!DNL Salesforce Marketing Cloud] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID connessione nell’esercitazione successiva per scoprire come [esplorare i sistemi di automazione di marketing utilizzando l’ API del servizio di flusso](../../explore/marketing-automation.md).
