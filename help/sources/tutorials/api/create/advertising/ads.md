---
title: Creare una connessione di base di Google Ads utilizzando l’API del servizio Flusso
description: Scopri come collegare Adobe Experience Platform a Google Ads utilizzando l’API del servizio Flusso.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 3%

---

# Creare una connessione di base di Google Ads utilizzando [!DNL Flow Service] API

>[!WARNING]
>
>Il [!DNL Google Ads] origine temporaneamente non disponibile. Adobe sta lavorando per risolvere i problemi con questa origine.

>[!NOTE]
>
>Il codice sorgente di Google Ads è in versione beta. Consulta la [Panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per Google Ads utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Guida introduttuva

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): Experienci Platform consente di acquisire dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experienci Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Experienci Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a Google Ads utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con Google Ads, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientCustomerId` | L’ID cliente client è il numero di account che corrisponde all’account client di Google Ads che desideri gestire con l’API di Google Ads. Questo ID segue il modello di `123-456-7890`. |
| `loginCustomerId` | L’ID cliente di accesso è il numero di account che corrisponde all’account di Google Ads Manager e viene utilizzato per recuperare i dati del rapporto da un cliente operativo specifico. Per ulteriori informazioni sull’ID cliente di accesso, leggi [Documentazione API di Google Ads](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | Il token sviluppatore ti consente di accedere all’API di Google Ads. Puoi utilizzare lo stesso token sviluppatore per effettuare richieste su tutti gli account Google Ads. Recupera il token di sviluppo tramite [accesso al tuo account manager](https://ads.google.com/home/tools/manager-accounts/) e quindi passare al [!DNL API Center] pagina. |
| `refreshToken` | Il token di aggiornamento fa parte di [!DNL OAuth2] autenticazione. Questo token ti consente di rigenerare i token di accesso dopo la scadenza. |
| `clientId` | L’ID client viene utilizzato insieme al segreto client come parte di [!DNL OAuth2] autenticazione. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto dell’account identificando l’applicazione in Google. |
| `clientSecret` | Il segreto client viene utilizzato insieme all&#39;ID client come parte [!DNL OAuth2] autenticazione. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto dell’account identificando l’applicazione in Google. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per Google Ads è: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Leggi il documento di panoramica API per [ulteriori informazioni su come iniziare a utilizzare Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` fornendo le credenziali di autenticazione di Google Ads come parte dei parametri di richiesta.

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
              "authenticationType": "{AUTHENTICATION_TYPE}"
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "refreshToken": "{REFRESH_TOKEN}"
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
| `auth.params.clientCustomerID` | L’ID cliente del tuo account Google Ads. |
| `auth.params.loginCustomerID` | L&#39;ID cliente di accesso che corrisponde al tuo account Google Ads Manager. |
| `auth.params.developerToken` | Token sviluppatore dell’account Google Ads. |
| `auth.params.refreshToken` | Il token di aggiornamento dell’account Google Ads. |
| `auth.params.clientID` | ID client dell’account Google Ads. |
| `auth.params.clientSecret` | Il segreto client dell’account Google Ads. |
| `connectionSpec.id` | L’ID della specifica di connessione di Google Ads: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione di base Google Ads utilizzando [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati pubblicitari su Platform utilizzando [!DNL Flow Service] API](../../collect/advertising.md)
