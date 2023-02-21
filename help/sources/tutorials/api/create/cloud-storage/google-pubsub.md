---
title: Creare una connessione Google PubSub Source utilizzando l’API del servizio di flusso
description: Scopri come collegare Adobe Experience Platform a un account Google PubSub utilizzando l’API del servizio di flusso.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 2b72d384e8edd91c662364dfac31ce4edff79172
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 1%

---

# Crea un [!DNL Google PubSub] Connessione sorgente tramite l’API del servizio di flusso

Questa esercitazione descrive i passaggi per la connessione [!DNL Google PubSub] (in appresso denominato &quot;[!DNL PubSub]&quot;) ad Experience Platform, utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente [!DNL PubSub] su Platform utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi a [!DNL PubSub], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `projectId` | ID progetto necessario per l&#39;autenticazione [!DNL PubSub]. |
| `credentials` | Credenziale o chiave necessaria per l&#39;autenticazione [!DNL PubSub]. |
| `topicId` | L&#39;ID per [!DNL PubSub] risorsa che rappresenta un feed di messaggi. È necessario specificare un ID argomento se si desidera fornire l&#39;accesso a un flusso specifico di dati nel [!DNL Google PubSub] sorgente. |
| `subscriptionId` | L&#39;ID del tuo [!DNL PubSub] abbonamento. In [!DNL PubSub], gli abbonamenti ti consentono di ricevere i messaggi, abbonandoti all’argomento in cui i messaggi sono stati pubblicati. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di destinazione di origine. La [!DNL PubSub] ID della specifica di connessione: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Per ulteriori informazioni su questi valori, consulta [[!DNL PubSub] autenticazione](https://cloud.google.com/pubsub/docs/authentication) documento. Per utilizzare l&#39;autenticazione basata sull&#39;account del servizio, consulta [[!DNL PubSub] guida alla creazione di account di servizio](https://cloud.google.com/docs/authentication/production#create_service_account) per i passaggi su come generare le credenziali.

>[!TIP]
>
>Se utilizzi l’autenticazione basata sull’account del servizio, assicurati di aver concesso un accesso utente sufficiente all’account del servizio e che non vi siano spazi bianchi aggiuntivi nel JSON durante la copia e l’incolla delle credenziali.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Il primo passaggio nella creazione di una connessione sorgente è quello di autenticare il [!DNL PubSub] e genera un ID di connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL PubSub] credenziali di autenticazione come parte dei parametri della richiesta.

Durante questo passaggio, puoi definire i dati a cui il tuo account ha accesso fornendo un ID argomento. Solo le sottoscrizioni associate a tale ID argomento saranno accessibili.

>[!NOTE]
>
>I Principali (ruoli) assegnati a un progetto pubsub vengono ereditati in tutti gli argomenti e le sottoscrizioni creati all&#39;interno di un [!DNL PubSub] progetto. Se desideri aggiungere un&#39;entità (ruolo) per avere accesso a un argomento specifico, è necessario aggiungere tale entità (ruolo) anche alla sottoscrizione corrispondente dell&#39;argomento. Per ulteriori informazioni, consulta la sezione [[!DNL PubSub] documentazione sul controllo degli accessi](https://cloud.google.com/pubsub/docs/access-control).

**Formato API**

```http
POST /connections
```

**Richiesta**

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
          "specName": "Google PubSub authentication credentials",
          "params": {
              "projectId": "acme-project",
              "credentials": "{CREDENTIALS}",
              "topicId": "acmeProjectAPI",
              "subscriptionId": "acme-project-api-new"
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
| `auth.params.projectId` | ID progetto necessario per l&#39;autenticazione [!DNL PubSub]. |
| `auth.params.credentials` | Credenziale o chiave necessaria per l&#39;autenticazione [!DNL PubSub]. |
| `auth.params.topicId` | ID argomento del [!DNL PubSub] origine a cui si desidera fornire l&#39;accesso. |
| `auth.params.subscriptionId` | ID dell’abbonamento rispetto al [!DNL PubSub] argomento. |
| `connectionSpec.id` | La [!DNL PubSub] ID delle specifiche di connessione: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID di connessione di base è necessario nel passaggio successivo per creare una connessione di origine.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Creazione di una connessione sorgente {#source}

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali l’origine dati, il formato dati e un ID di connessione di origine necessari per creare un flusso di dati. Un&#39;istanza di connessione di origine è specifica per un tenant e un&#39;organizzazione.

Per creare una connessione di origine, invia una richiesta POST al `/sourceConnections` punto finale [!DNL Flow Service] API.

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
          "topicId": "acme-project",
          "subscriptionId": "{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione sorgente. |
| `description` | Valore facoltativo che è possibile fornire per includere ulteriori informazioni sulla connessione sorgente. |
| `baseConnectionId` | L&#39;ID di connessione di base del [!DNL PubSub] origine generata nel passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione fissa per [!DNL PubSub]. Questo ID è: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Il formato del [!DNL PubSub] dati da acquisire. Attualmente, l’unico formato di dati supportato è `json`. |
| `params.topicId` | Nome o ID del [!DNL PubSub] argomento. In [!DNL PubSub], un argomento è una risorsa denominata che rappresenta un feed di messaggi. |
| `params.subscriptionId` | L’ID della sottoscrizione che corrisponde a un dato argomento. In [!DNL PubSub], le sottoscrizioni consentono di leggere i messaggi da un argomento. È possibile assegnare uno o più abbonamenti a un singolo argomento. |
| `params.dataType` | Questo parametro definisce il tipo di dati da acquisire. I tipi di dati supportati includono: `raw` e `xdm`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Questo ID è necessario nell’esercitazione successiva per creare un flusso di dati.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL PubSub] connessione di origine tramite [!DNL Flow Service] API. Puoi usare questo ID di connessione sorgente nell’esercitazione successiva per [creare un flusso di dati in streaming utilizzando [!DNL Flow Service] API](../../collect/streaming.md).
