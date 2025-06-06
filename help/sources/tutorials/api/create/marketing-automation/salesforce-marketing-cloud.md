---
title: Creare una connessione di base a Salesforce Marketing Cloud utilizzando l’API del servizio Flow
description: Scopri come autenticare il tuo account Salesforce Marketing Cloud rispetto a Experience Platform utilizzando l’API del servizio Flow.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 7ff0709b62590bb80c1ed664368f28cdc4a950ea
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 4%

---

# Creare una connessione di base [!DNL Salesforce Marketing Cloud] utilizzando l&#39;API [!DNL Flow Service]

>[!WARNING]
>
>L&#39;origine [!DNL Salesforce Marketing Cloud] diventerà obsoleta a gennaio 2026. Una nuova fonte verrà rilasciata nel corso di quest&#39;anno come alternativa. Una volta rilasciata la nuova origine, è necessario pianificare la migrazione alla nuova origine creando nuove connessioni account e flussi di dati prima della fine di gennaio 2026.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Salesforce Marketing Cloud] utilizzando [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

La sezione seguente fornisce informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Salesforce Marketing Cloud] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Salesforce Marketing Cloud], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Server host dell&#39;applicazione. Questo è spesso il tuo sottodominio. **Nota:** Quando si immette il valore `host`, è necessario specificare `{subdomain}.rest.marketingcloudapis.com`. Ad esempio, se l&#39;URL host è `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, è necessario immettere `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` come valore host. |
| `clientId` | L&#39;ID client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `clientSecret` | Il segreto client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce Marketing Cloud]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL Salesforce Marketing Cloud] documento](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## Creare una connessione di base

>[!IMPORTANT]
>
>L&#39;acquisizione di oggetti personalizzati non è attualmente supportata dall&#39;integrazione di origine [!DNL Salesforce Marketing Cloud].

Una connessione di base mantiene le informazioni tra l’origine e Experience Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Salesforce Marketing Cloud] come parte del corpo della richiesta.

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
| `auth.params.clientId` | L&#39;ID client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `auth.params.clientSecret` | Il segreto client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Salesforce Marketing Cloud]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso l&#39;identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Salesforce Marketing Cloud] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati di automazione marketing in Experience Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
