---
title: Creare una connessione Google PubSub Source utilizzando l’API del servizio Flusso
description: Scopri come collegare Adobe Experience Platform a un account Google PubSub utilizzando l’API del servizio Flow.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: fcac805e151d6142886eb8e05da0eb1babad2f69
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 2%

---

# Crea una connessione Source [!DNL Google PubSub] utilizzando l&#39;API del servizio Flusso

>[!IMPORTANT]
>
>L&#39;origine [!DNL Google PubSub] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial illustra i passaggi necessari per connettere ad Experience Platform [!DNL Google PubSub] (di seguito &quot;[!DNL PubSub]&quot;) utilizzando l&#39;API [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettere correttamente [!DNL PubSub] a Platform utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Per connettere l&#39;account [!DNL PubSub] a [!DNL Flow Service], è necessario fornire i valori per le proprietà di connessione descritte di seguito. Per ulteriori informazioni sull&#39;autenticazione e sulla configurazione dei prerequisiti, leggere la [[!DNL PubSub source] panoramica](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).

>[!BEGINTABS]

>[!TAB Autenticazione basata su progetto]

| Credenziali | Descrizione |
| --- | --- |
| `projectId` | ID progetto richiesto per autenticare [!DNL PubSub]. |
| `credentials` | Credenziali necessarie per autenticare [!DNL PubSub]. Assicurati di inserire il file JSON completo dopo aver rimosso gli spazi vuoti dalle credenziali. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di destinazione di origine. ID della specifica di connessione [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB Autenticazione basata su argomenti e sottoscrizioni]

| Credenziali | Descrizione |
| --- | --- |
| `credentials` | Credenziali necessarie per autenticare [!DNL PubSub]. Assicurati di inserire il file JSON completo dopo aver rimosso gli spazi vuoti dalle credenziali. |
| `topicName` | Nome della risorsa che rappresenta un feed di messaggi. È necessario specificare un nome di argomento se si desidera fornire l&#39;accesso a un flusso di dati specifico nell&#39;origine [!DNL PubSub]. Il formato del nome argomento è: `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | Nome dell&#39;abbonamento [!DNL PubSub]. In [!DNL PubSub], gli abbonamenti consentono di ricevere messaggi, sottoscrivendo l&#39;argomento in cui i messaggi sono stati pubblicati. **Nota**: è possibile utilizzare una singola sottoscrizione [!DNL PubSub] per un solo flusso di dati. Per creare più flussi di dati, devi disporre di più abbonamenti. Formato del nome della sottoscrizione: `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di destinazione di origine. ID della specifica di connessione [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

Per ulteriori informazioni su questi valori, leggere questo documento di [[!DNL PubSub] autenticazione](https://cloud.google.com/pubsub/docs/authentication). Per utilizzare l&#39;autenticazione basata su account di servizio, leggere questa [[!DNL PubSub] guida sulla creazione di account di servizio](https://cloud.google.com/docs/authentication/production#create_service_account) per i passaggi relativi alla generazione delle credenziali.

>[!TIP]
>
>Se utilizzi l’autenticazione basata sull’account del servizio, assicurati di aver concesso un accesso utente sufficiente all’account del servizio e di non inserire spazi vuoti aggiuntivi nel JSON quando copi e incolla le credenziali.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

>[!TIP]
>
>Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Google PubSub]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Il primo passaggio nella creazione di una connessione di origine consiste nell&#39;autenticare l&#39;origine [!DNL PubSub] e generare un ID connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare elementi specifici da acquisire, incluse informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL PubSub] come parte dei parametri della richiesta.

L&#39;origine [!DNL PubSub] consente di specificare il tipo di accesso da consentire durante l&#39;autenticazione. È possibile impostare l&#39;account in modo che disponga dell&#39;accesso root o limitare l&#39;accesso a un particolare argomento [!DNL PubSub] e a una sottoscrizione specifica.

>[!NOTE]
>
>Le entità (ruoli) assegnate a un progetto [!DNL PubSub] vengono ereditate in tutti gli argomenti e le sottoscrizioni creati all&#39;interno di un progetto [!DNL PubSub]. Se si desidera che un&#39;entità principale (ruolo) abbia accesso a un argomento specifico, è necessario aggiungere anche tale entità principale (ruolo) alla sottoscrizione corrispondente dell&#39;argomento. Per ulteriori informazioni, leggere la [[!DNL PubSub] documentazione sul controllo degli accessi](<https://cloud.google.com/pubsub/docs/access-control>).

**Formato API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticazione basata su progetto]

Per creare una connessione di base con l&#39;autenticazione basata su progetto, effettuare una richiesta POST all&#39;endpoint `/connections` e fornire `projectId` e `credentials` nel corpo della richiesta.

+++Richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Project Based Authentication",
          "params": {
              "projectId": "{PROJECT_ID}",
              "credentials": "{CREDENTIALS}"
          }
      },
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.projectId` | ID progetto richiesto per autenticare [!DNL PubSub]. |
| `auth.params.credentials` | Credenziali o chiave necessarie per autenticare [!DNL PubSub]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

++++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID connessione di base è richiesto nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!TAB Autenticazione basata su argomenti e sottoscrizioni]

Per creare una connessione di base con autenticazione basata su argomento e su sottoscrizione, effettuare una richiesta POST all&#39;endpoint `/connections` e fornire `credentials`, `topicName` e `subscriptionName` nel corpo della richiesta.

+++Richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
          }
      },
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.credentials` | Credenziali o chiave necessarie per autenticare [!DNL PubSub]. |
| `auth.params.topicName` | Coppia ID progetto e ID argomento per l&#39;origine [!DNL PubSub] a cui si desidera fornire l&#39;accesso. |
| `auth.params.subscriptionName` | La coppia ID progetto e ID sottoscrizione per l&#39;origine [!DNL PubSub] a cui si desidera fornire l&#39;accesso. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID connessione di base è richiesto nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!ENDTABS]


## Creare una connessione sorgente {#source}

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali origine dati, formato dati e un ID di connessione di origine necessari per creare un flusso di dati. Un&#39;istanza della connessione di origine è specifica di un tenant e di un&#39;organizzazione.

Per creare una connessione di origine, effettuare una richiesta POST all&#39;endpoint `/sourceConnections` dell&#39;API [!DNL Flow Service].

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Google PubSub source connection",
      "description": "A source connection for Google PubSub",
      "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto può essere utilizzato per cercare informazioni sulla connessione sorgente. |
| `description` | Valore facoltativo che è possibile fornire per includere ulteriori informazioni sulla connessione di origine. |
| `baseConnectionId` | ID della connessione di base dell&#39;origine [!DNL PubSub] generato nel passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione fissa per [!DNL PubSub]. ID: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Formato dei dati [!DNL PubSub] che si desidera acquisire. Attualmente, l&#39;unico formato di dati supportato è `json`. |
| `params.topicName` | Il nome dell&#39;argomento [!DNL PubSub]. In [!DNL PubSub] un argomento è una risorsa denominata che rappresenta un feed di messaggi. |
| `params.subscriptionName` | Il nome della sottoscrizione che corrisponde a un determinato argomento. In [!DNL PubSub], gli abbonamenti consentono di leggere i messaggi da un argomento. È possibile assegnare una o più sottoscrizioni a un singolo argomento. |
| `params.dataType` | Questo parametro definisce il tipo di dati che viene acquisito. I tipi di dati supportati sono: `raw` e `xdm`. |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di origine appena creata. Questo ID è richiesto nell’esercitazione successiva per creare un flusso di dati.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione sorgente [!DNL PubSub] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di origine nella prossima esercitazione per [creare un flusso di dati in streaming utilizzando l&#39; [!DNL Flow Service] API](../../collect/streaming.md).
