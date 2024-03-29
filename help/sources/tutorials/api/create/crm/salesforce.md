---
keywords: Experience Platform;home;argomenti popolari;Salesforce;salesforce
solution: Experience Platform
title: Creare una connessione di base Salesforce utilizzando l’API del servizio Flow
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un account Salesforce utilizzando l’API del servizio Flusso.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 27ad8812137502d0a636345852f0cae5d01c7b23
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 4%

---

# Creare un [!DNL Salesforce] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Salesforce] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente [!DNL Platform] a un [!DNL Salesforce] account che utilizza [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi a [!DNL Salesforce], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `environmentUrl` | L’URL del [!DNL Salesforce] istanza di origine. |
| `username` | Nome utente per [!DNL Salesforce] account utente. |
| `password` | La password per [!DNL Salesforce] account utente. |
| `securityToken` | Token di sicurezza per [!DNL Salesforce] account utente. |
| `apiVersion` | Facoltativo) La versione REST API di [!DNL Salesforce] che si sta utilizzando. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, è necessario immettere il valore come `52.0` Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Salesforce] è: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Per ulteriori informazioni su come iniziare, visita [questo documento Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` e fornire il [!DNL Salesforce] credenziali di autenticazione nel corpo della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Salesforce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Connection",
      "description": "Connection for Salesforce account",
      "auth": {
          "specName": "Basic Authentication",
          "params": {****
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
| `auth.params.username` | Il nome utente associato al tuo [!DNL Salesforce] account. |
| `auth.params.password` | La password associata al tuo [!DNL Salesforce] account. |
| `auth.params.securityToken` | Il token di sicurezza associato al tuo [!DNL Salesforce] account. |
| `connectionSpec.id` | Il [!DNL Salesforce] ID specifica di connessione: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Salesforce] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati CRM in Platform utilizzando [!DNL Flow Service] API](../../collect/crm.md)
