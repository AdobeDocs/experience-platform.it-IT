---
title: Creare una connessione sorgente PubSub di Google utilizzando l’API del servizio Flusso
description: Scopri come collegare Adobe Experience Platform a un account Google PubSub utilizzando l’API del servizio Flow.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 1%

---

# Creare un [!DNL Google PubSub] Connessione sorgente tramite l’API del servizio Flusso

>[!IMPORTANT]
>
>Il [!DNL Google PubSub] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial illustra i passaggi necessari per la connessione [!DNL Google PubSub] (in seguito denominati &quot;[!DNL PubSub]&quot;) per l&#39;Experience Platform, utilizzando [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente [!DNL PubSub] alla piattaforma utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi a [!DNL PubSub], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `projectId` | ID progetto richiesto per l’autenticazione [!DNL PubSub]. |
| `credentials` | Credenziali o chiave necessarie per l&#39;autenticazione [!DNL PubSub]. |
| `topicName` | Nome della risorsa che rappresenta un feed di messaggi. È necessario specificare un nome di argomento se si desidera fornire l&#39;accesso a un flusso di dati specifico nel [!DNL PubSub] sorgente. Il formato del nome dell&#39;argomento è: `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | Il nome del tuo [!DNL PubSub] abbonamento. In entrata [!DNL PubSub], gli abbonamenti ti consentono di ricevere messaggi, abbonandoti all’argomento in cui i messaggi sono stati pubblicati in. **Nota**: un singolo [!DNL PubSub] l’abbonamento può essere utilizzato per un solo flusso di dati. Per creare più flussi di dati, devi disporre di più abbonamenti. Il formato del nome dell’abbonamento è: `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di destinazione di origine. Il [!DNL PubSub] ID specifica di connessione: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Per ulteriori informazioni su questi valori, vedere [[!DNL PubSub] autenticazione](https://cloud.google.com/pubsub/docs/authentication) documento. Per utilizzare l&#39;autenticazione basata sull&#39;account del servizio, vedere [[!DNL PubSub] guida alla creazione di account di servizio](https://cloud.google.com/docs/authentication/production#create_service_account) per i passaggi su come generare le credenziali.

>[!TIP]
>
>Se utilizzi l’autenticazione basata sull’account del servizio, assicurati di aver concesso un accesso utente sufficiente all’account del servizio e di non inserire spazi vuoti aggiuntivi nel JSON quando copi e incolla le credenziali.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Il primo passaggio nella creazione di una connessione sorgente consiste nell’autenticare [!DNL PubSub] e generare un ID di connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare elementi specifici da acquisire, incluse informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL PubSub] credenziali di autenticazione come parte dei parametri della richiesta.

Il [!DNL PubSub] origine consente di specificare il tipo di accesso da consentire durante l&#39;autenticazione. Puoi impostare l’account in modo che abbia accesso root o limitare l’accesso a un particolare [!DNL PubSub] argomento e abbonamento.

>[!NOTE]
>
>Entità principale (ruoli) assegnata a un [!DNL PubSub] vengono ereditati in tutti gli argomenti e le sottoscrizioni creati all&#39;interno di un [!DNL PubSub] progetto. Se si desidera che un&#39;entità principale (ruolo) abbia accesso a un argomento specifico, è necessario aggiungere tale entità principale (ruolo) anche alla sottoscrizione corrispondente dell&#39;argomento. Per ulteriori informazioni, leggere [[!DNL PubSub] documentazione sul controllo degli accessi](<https://cloud.google.com/pubsub/docs/access-control>).

**Formato API**

```http
POST /connections
```

**Richiesta**

>[!BEGINTABS]

>[!TAB Autenticazione basata su progetto]

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
| `auth.params.projectId` | ID progetto richiesto per l’autenticazione [!DNL PubSub]. |
| `auth.params.credentials` | Credenziali o chiave necessarie per l&#39;autenticazione [!DNL PubSub]. |
| `connectionSpec.id` | Il [!DNL PubSub] ID specifica di connessione: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB Autenticazione basata su argomenti e sottoscrizioni]

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
| `auth.params.credentials` | Credenziali o chiave necessarie per l&#39;autenticazione [!DNL PubSub]. |
| `auth.params.topicName` | La coppia ID progetto e ID argomento per [!DNL PubSub] origine a cui desideri fornire accesso. |
| `auth.params.subscriptionName` | La coppia ID progetto e ID abbonamento per [!DNL PubSub] origine a cui desideri fornire accesso. |
| `connectionSpec.id` | Il [!DNL PubSub] ID specifica di connessione: `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID connessione di base è richiesto nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Creare una connessione sorgente {#source}

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali origine dati, formato dati e un ID di connessione di origine necessari per creare un flusso di dati. Un&#39;istanza della connessione di origine è specifica di un tenant e di un&#39;organizzazione.

Per creare una connessione sorgente, effettua una richiesta POST al `/sourceConnections` endpoint del [!DNL Flow Service] API.

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
| `baseConnectionId` | L’ID della connessione di base [!DNL PubSub] origine generata nel passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione fissa per [!DNL PubSub]. Questo ID è: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Il formato del [!DNL PubSub] i dati che desideri acquisire. Attualmente, l’unico formato di dati supportato è `json`. |
| `params.topicName` | Il nome del tuo [!DNL PubSub] argomento. In entrata [!DNL PubSub], un argomento è una risorsa denominata che rappresenta un feed di messaggi. |
| `params.subscriptionName` | Il nome della sottoscrizione che corrisponde a un determinato argomento. In entrata [!DNL PubSub], gli abbonamenti ti consentono di leggere i messaggi da un argomento. È possibile assegnare una o più sottoscrizioni a un singolo argomento. |
| `params.dataType` | Questo parametro definisce il tipo di dati che viene acquisito. I tipi di dati supportati includono: `raw` e `xdm`. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’identificatore univoco (`id`) della connessione sorgente appena creata. Questo ID è richiesto nell’esercitazione successiva per creare un flusso di dati.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL PubSub] connessione sorgente tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione sorgente nell’esercitazione successiva per [creare un flusso di dati in streaming utilizzando [!DNL Flow Service] API](../../collect/streaming.md).
