---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Creare una connessione di base Microsoft Dynamics utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come connettere Platform a un account Microsoft Dynamics utilizzando l’API del servizio Flusso.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 3%

---

# Creare una connessione di base [!DNL Microsoft Dynamics] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Microsoft Dynamics] (di seguito &quot;[!DNL Dynamics]&quot;) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettere correttamente Platform a un account Dynamics utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Dynamics], è necessario fornire i valori per le proprietà di connessione seguenti:

>[!BEGINTABS]

>[!TAB Autenticazione di base]

| Credenziali | Descrizione |
| --- | --- |
| `serviceUri` | L&#39;URL del servizio dell&#39;istanza [!DNL Dynamics]. |
| `username` | Il nome utente per l&#39;account utente [!DNL Dynamics]. |
| `password` | Password per l&#39;account [!DNL Dynamics]. |

>[!TAB Autenticazione Service-principal e chiave]

| Credenziali | Descrizione |
| --- | --- |
| `servicePrincipalId` | ID client dell&#39;account [!DNL Dynamics]. Questo ID è necessario quando si utilizza l’entità servizio e l’autenticazione basata su chiave. |
| `servicePrincipalKey` | Chiave segreta dell&#39;entità servizio. Questa credenziale è necessaria quando si utilizza l&#39;entità servizio e l&#39;autenticazione basata su chiave. |

>[!ENDTABS]

Per ulteriori informazioni, consulta [questo [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

>[!TIP]
>
>Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Dynamics]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Dynamics] come parte dei parametri della richiesta.

### Crea una connessione di base [!DNL Dynamics]

>[!TIP]
>
>Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Dynamics]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Il primo passaggio nella creazione di una connessione di origine consiste nell&#39;autenticare l&#39;origine [!DNL Dynamics] e generare un ID connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare elementi specifici da acquisire, incluse informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Dynamics] come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per creare una connessione di base [!DNL Dynamics] utilizzando l&#39;autenticazione di base, eseguire una richiesta POST all&#39;API [!DNL Flow Service] fornendo i valori per `serviceUri`, `username` e `password` della connessione.

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
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.serviceUri` | L&#39;URI del servizio associato all&#39;istanza [!DNL Dynamics]. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Dynamics]. |
| `auth.params.password` | La password associata al tuo account [!DNL Dynamics]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB Autenticazione basata su chiave entità servizio]

Per creare una connessione di base [!DNL Dynamics] utilizzando l&#39;autenticazione basata sulla chiave dell&#39;entità servizio, eseguire una richiesta POST all&#39;API [!DNL Flow Service] fornendo i valori per `serviceUri`, `servicePrincipalId` e `servicePrincipalKey` della connessione.

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
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.serviceUri` | L&#39;URI del servizio associato all&#39;istanza [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | ID client dell&#39;account [!DNL Dynamics]. Questo ID è necessario quando si utilizza l’entità servizio e l’autenticazione basata su chiave. |
| `auth.params.servicePrincipalKey` | Chiave segreta dell&#39;entità servizio. Questa credenziale è necessaria quando si utilizza l&#39;entità servizio e l&#39;autenticazione basata su chiave. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare il sistema CRM nel passaggio successivo.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]


## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Microsoft Dynamics] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati CRM in Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/crm.md)
