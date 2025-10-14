---
title: Connettere Google Ads ad Experience Platform utilizzando le API
description: Scopri come collegare Adobe Experience Platform a Google Ads utilizzando l’API del servizio Flusso.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Connetti [!DNL Google Ads] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>L&#39;origine [!DNL Google Ads] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, vedere [Panoramica origini](../../../../home.md#terms-and-conditions).

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Leggi questo tutorial per scoprire come collegare il tuo account [!DNL Google Ads] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Google Ads] utilizzando l&#39;API [!DNL Flow Service].

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Google Ads] panoramica origine](../../../../connectors/advertising/ads.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Experience Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione di Google Ads come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per Google Ads:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "refreshToken": "{REFRESH_TOKEN}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "googleAdsApiVersion": "v17"

          }
      },
      "connectionSpec": {
          "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.clientCustomerID` | L&#39;ID cliente client dell&#39;account [!DNL Google Ads]. |
| `auth.params.loginCustomerID` | L&#39;ID cliente di accesso che corrisponde all&#39;account manager [!DNL Google Ads]. |
| `auth.params.developerToken` | Token sviluppatore dell&#39;account [!DNL Google Ads]. |
| `auth.params.refreshToken` | Token di aggiornamento dell&#39;account [!DNL Google Ads]. |
| `auth.params.clientID` | ID client dell&#39;account [!DNL Google Ads]. |
| `auth.params.clientSecret` | Il segreto client dell&#39;account [!DNL Google Ads]. |
| `auth.params.googleAdsApiVersion` | Versione API [!DNL Google Ads] in uso. La versione più recente supportata su Experience Platform è `v17`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Google Ads]: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Creare un flusso di dati per acquisire i dati pubblicitari

Seguendo questa esercitazione, hai creato una connessione di base [!DNL Google Ads] utilizzando l&#39;API [!DNL Flow Service] e hai connesso l&#39;account [!DNL Google Ads] ad Experience Platform. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati pubblicitari su Experience Platform utilizzando l&#39;API  [!DNL Flow Service] &#x200B;](../../collect/advertising.md)
