---
title: Creare una connessione di base al Marketing Cloud Salesforce utilizzando l’API del servizio Flow
description: Scopri come autenticare l’account di Marketing Cloud Salesforce in base a Experienci Platform utilizzando l’API del servizio Flow.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 635ab266fac9d3dc232307d7cb49f83904197782
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 5%

---

# Creare un [!DNL Salesforce Marketing Cloud] connessione di base tramite [!DNL Flow Service] API

>[!IMPORTANT]
>
>L’acquisizione di oggetti personalizzati non è attualmente supportata da [!DNL Salesforce Marketing Cloud] integrazione sorgente.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Salesforce Marketing Cloud] utilizzando [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

La sezione seguente fornisce informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Salesforce Marketing Cloud] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Salesforce Marketing Cloud], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Server host dell&#39;applicazione. Questo è spesso il tuo sottodominio. **Nota:** Quando si immette il `host` valore, è necessario specificare il valore `{subdomain}.rest.marketingcloudapis.com`. Ad esempio, se l’URL host è `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, è sufficiente inserire `acme-ab12c3d4e5fg6hijk7lmnop8qrstauth.marketingcloudapis.com/` come valore host. |
| `clientId` | L’ID client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |
| `clientSecret` | Il segreto client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce Marketing Cloud] è: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Per ulteriori informazioni su come iniziare, consulta questa [[!DNL Salesforce Marketing Cloud] documento](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Salesforce Marketing Cloud] credenziali di autenticazione come parte del corpo della richiesta.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Marketing Cloud base connection",
      "description": "Salesforce Marketing Cloud base connection",
      "auth": {
          "specName": "Client-Id-Secret Based Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "acme-salesforce-marketing-cloud",
              "clientSecret": "xxxx"
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
| `auth.params.clientId` | L’ID client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |
| `auth.params.clientSecret` | Il segreto client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |
| `connectionSpec.id` | Il [!DNL Salesforce Marketing Cloud] ID specifica di connessione: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Salesforce Marketing Cloud] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati di automazione marketing su Platform utilizzando [!DNL Flow Service] API](../../collect/marketing-automation.md)
