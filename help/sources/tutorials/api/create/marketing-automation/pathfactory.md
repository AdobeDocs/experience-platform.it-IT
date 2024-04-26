---
title: Creare una connessione di base PathFactory utilizzando l'API del servizio Flow
description: Scopri come autenticare l’account PathFactory in base a Experienci Platform utilizzando l’API del servizio Flow.
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---

# Creare un [!DNL PathFactory] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Leggi questo documento per scoprire come creare una connessione di base per [!DNL PathFactory] utilizzando [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

La sezione seguente fornisce informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL PathFactory] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste {#gather-credentials}

Per accedere all’account PathFactory sulla piattaforma, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Nome utente | Il tuo [!DNL PathFactory] nome utente dell’account. Questo è essenziale per identificare l’account nel sistema. |
| Password | La password associata al tuo [!DNL PathFactory] account. Assicurati che sia protetto per evitare accessi non autorizzati. |
| Dominio | Il dominio associato al tuo [!DNL PathFactory] account. In genere si riferisce all’identificatore univoco all’interno del [!DNL PathFactory] URL. |
| Token di accesso | Un token univoco utilizzato per l’autenticazione API per garantire una comunicazione sicura tra i sistemi e [!DNL PathFactory]. |
| Endpoint API | Endpoint API specifici per l’accesso ai dati: visitatori, sessioni e visualizzazioni di pagina. Ogni endpoint corrisponde a set di dati diversi che è possibile recuperare. **Nota:** Questi sono predefiniti da [!DNL PathFactory] e sono specifici per i dati a cui intendi accedere: <ul><li>**Endpoint visitatori**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Endpoint sessioni**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Endpoint visualizzazioni pagina**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Per ulteriori informazioni su come proteggere e utilizzare le credenziali e su come ottenere e aggiornare il token di accesso, visita [[!DNL PathFactory] Centro assistenza](https://support.pathfactory.com/categories/adobe/). Questa risorsa offre guide complete sulla gestione delle credenziali e sulla garanzia di un’integrazione API efficace e sicura.

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL PathFactory] credenziali di autenticazione come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL PathFactory]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
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
| `auth.params.clientId` | L’ID client associato al tuo [!DNL PathFactory] applicazione. |
| `auth.params.clientSecret` | Il segreto client associato al tuo [!DNL PathFactory] applicazione. |
| `connectionSpec.id` | Il [!DNL PathFactory] ID specifica di connessione: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco di connessione (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL PathFactory] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati di automazione marketing su Platform utilizzando [!DNL Flow Service] API](../../collect/marketing-automation.md)
