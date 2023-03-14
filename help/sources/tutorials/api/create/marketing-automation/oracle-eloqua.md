---
title: Creare un Oracle di connessione Eloqua Base utilizzando l’API del servizio Flow
description: Scopri come collegare Adobe Experience Platform ad Oracle Eloqua utilizzando l’API del servizio Flow.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Creare un [!DNL Oracle Eloqua] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Oracle Eloqua] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Platform:

* [Sorgenti](../../../../home.md): Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Oracle Eloqua] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Oracle Eloqua], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| `endpoint` | Endpoint del tuo [!DNL Oracle Eloqua]. |
| `username` | Il nome utente del [!DNL Oracle Eloqua] account. Il nome utente deve essere formattato come `siteName + \\ + username`, dove `siteName` è il nome della società a cui accedi [!DNL Oracle Eloqua] e `username` è il tuo nome utente. Ad esempio, il nome utente per l’accesso può essere: `adobe\\emily`. |
| `password` | La password corrispondente al tuo [!DNL Oracle Eloqua] nome utente. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. Il valore per l&#39;ID della specifica di connessione del [!DNL Oracle Eloqua] l&#39;origine è fissa come: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Per ulteriori informazioni sulle credenziali di autenticazione per [!DNL Oracle Eloqua], vedere [[!DNL Oracle Eloqua] guida all’autenticazione](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Oracle Eloqua] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Oracle Eloqua]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `name` | Il nome del tuo [!DNL Oracle Eloqua] connessione di base. È consigliabile fornire un nome descrittivo, in quanto è possibile utilizzare questo valore per cercare la connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire informazioni aggiuntive sulla connessione di base. |
| `auth.specName` | Tipo di autenticazione utilizzato per la connessione. |
| `auth.params.endpoint` | Endpoint del tuo [!DNL Oracle Eloqua] server. |
| `auth.params.username` | Credenziali concatenate che includono il nome del sito e il nome utente corrispondenti al [!DNL Oracle Eloqua] account. |
| `auth.params.password` | La password che corrisponde al tuo [!DNL Oracle Eloqua] account. |
| `connectionSpec.id` | Il valore per l&#39;ID della specifica di connessione del [!DNL Oracle Eloqua] l&#39;origine è fissa come: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un’ [!DNL Oracle Eloqua] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati di automazione marketing su Platform utilizzando [!DNL Flow Service] API](../../collect/marketing-automation.md)
