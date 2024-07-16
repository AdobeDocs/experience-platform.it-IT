---
title: Creare una connessione di base PathFactory utilizzando l'API del servizio Flow
description: Scopri come autenticare l’account PathFactory in base a Experience Platform utilizzando l’API del servizio Flow.
badge: Beta
exl-id: 2bdfe38b-d3f7-480f-87c6-0b98b9521be2
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---

# Creare una connessione di base [!DNL PathFactory] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Leggi questo documento per scoprire come creare una connessione di base per [!DNL PathFactory] utilizzando [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

La sezione seguente fornisce informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL PathFactory] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste {#gather-credentials}

Per accedere all’account PathFactory sulla piattaforma, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Nome utente | Nome utente dell&#39;account [!DNL PathFactory]. Questo è essenziale per identificare l’account nel sistema. |
| Password | La password associata al tuo account [!DNL PathFactory]. Assicurati che sia protetto per evitare accessi non autorizzati. |
| Dominio | Il dominio associato al tuo account [!DNL PathFactory]. In genere si riferisce all&#39;identificatore univoco all&#39;interno dell&#39;URL [!DNL PathFactory]. |
| Token di accesso | Token univoco utilizzato per l&#39;autenticazione API per garantire una comunicazione sicura tra i sistemi e [!DNL PathFactory]. |
| Endpoint API | Endpoint API specifici per l’accesso ai dati: visitatori, sessioni e visualizzazioni di pagina. Ogni endpoint corrisponde a set di dati diversi che è possibile recuperare. **Nota:** questi sono predefiniti da [!DNL PathFactory] e sono specifici per i dati a cui intendi accedere: <ul><li>**Endpoint visitatori**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Endpoint sessioni**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Endpoint visualizzazioni pagina**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Per ulteriori informazioni su come proteggere e utilizzare le credenziali, nonché su come ottenere e aggiornare il token di accesso, visitare il [[!DNL PathFactory] Centro assistenza](https://support.pathfactory.com/categories/adobe/). Questa risorsa offre guide complete sulla gestione delle credenziali e sulla garanzia di un’integrazione API efficace e sicura.

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL PathFactory] come parte del corpo della richiesta.

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
| `auth.params.clientId` | L&#39;ID client associato all&#39;applicazione [!DNL PathFactory]. |
| `auth.params.clientSecret` | Il segreto client associato all&#39;applicazione [!DNL PathFactory]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL PathFactory]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso l&#39;identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL PathFactory] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati di automazione marketing su Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
