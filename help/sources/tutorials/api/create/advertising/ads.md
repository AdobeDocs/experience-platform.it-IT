---
keywords: Experience Platform;home;argomenti popolari;annunci Google;annunci Google;annunci Google;annunci Google;annunci
title: Creare una connessione di base Google Ads utilizzando l’API del servizio di flusso
description: Scopri come collegare Adobe Experience Platform ad Google Ads utilizzando l’API del servizio di flusso.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---

# Creare una connessione di base Google Ads utilizzando [!DNL Flow Service] API

>[!NOTE]
>
>L&#39;origine Google Ads è in versione beta. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per Google Ads utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Experience Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi con successo a Google Ads utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con Google Ads, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientCustomerId` | L’ID cliente client è il numero di account che corrisponde all’account client Google Ads che desideri gestire con l’API Google Ads. Questo ID segue il modello di `123-456-7890`. |
| `developerToken` | Il token sviluppatore ti consente di accedere all’API Google Ads. Puoi usare lo stesso token sviluppatore per effettuare richieste per tutti i tuoi account Google Ads. Recupera il token sviluppatore tramite [accesso al tuo account manager](https://ads.google.com/home/tools/manager-accounts/) e quindi passare alla [!DNL API Center] pagina. |
| `refreshToken` | Il token di aggiornamento fa parte di [!DNL OAuth2] autenticazione. Questo token ti consente di rigenerare i token di accesso dopo la scadenza. |
| `clientId` | L&#39;ID client viene utilizzato in tandem con il segreto client come parte di [!DNL OAuth2] autenticazione. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto del tuo account identificando l&#39;applicazione in Google. |
| `clientSecret` | Il segreto client viene utilizzato in parallelo con l’ID client come parte di [!DNL OAuth2] autenticazione. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto del tuo account identificando l&#39;applicazione in Google. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per Google Ads è: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Leggi il documento di panoramica API per [ulteriori informazioni su come iniziare a utilizzare Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` endpoint durante la fornitura delle credenziali di autenticazione di Google Ads come parte dei parametri di richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per Google Ads:

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
| `auth.params.clientCustomerID` | ID cliente del tuo account Google Ads. |
| `auth.params.developerToken` | Il token sviluppatore del tuo account Google Ads. |
| `auth.params.refreshToken` | Il token di aggiornamento del tuo account Google Ads. |
| `auth.params.clientID` | L&#39;ID client del tuo account Google Ads. |
| `auth.params.clientSecret` | Il segreto client del tuo account Google Ads. |
| `connectionSpec.id` | ID delle specifiche di connessione di Google Ads: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione base Google Ads utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per portare i dati pubblicitari su Platform utilizzando [!DNL Flow Service] API](../../collect/advertising.md)
