---
title: Creare un Oracle di connessione Eloqua Base utilizzando l’API del servizio Flow
description: Scopri come collegare Adobe Experience Platform ad Oracle Eloqua utilizzando l’API del servizio Flow.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 1%

---

# Creare una connessione di base [!DNL Oracle Eloqua] utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Oracle Eloqua] diventerà obsoleta alla fine di maggio 2025. È possibile utilizzare [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) al posto dell&#39;origine [!DNL Oracle Eloqua].

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Oracle Eloqua] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Guida introduttuva

Questa guida richiede una buona conoscenza dei seguenti componenti di Platform:

* [Origini](../../../../home.md): Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che suddividono una singola istanza [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Oracle Eloqua] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Oracle Eloqua], è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| --- | --- |
| `endpoint` | Endpoint di [!DNL Oracle Eloqua]. |
| `username` | Il nome utente dell&#39;account [!DNL Oracle Eloqua]. Il nome utente deve essere formattato come `siteName + \\ + username`, dove `siteName` è il nome società utilizzato per accedere a [!DNL Oracle Eloqua] e `username` è il nome utente. Ad esempio, il nome utente di accesso può essere: `adobe\\emily`. |
| `password` | La password corrispondente al nome utente [!DNL Oracle Eloqua]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. Il valore per l&#39;ID della specifica di connessione dell&#39;origine [!DNL Oracle Eloqua] è fisso come: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Per ulteriori informazioni sulle credenziali di autenticazione per [!DNL Oracle Eloqua], vedere la [[!DNL Oracle Eloqua] guida sull&#39;autenticazione](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Oracle Eloqua] come parte dei parametri della richiesta.

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
| `name` | Nome della connessione di base [!DNL Oracle Eloqua]. È consigliabile fornire un nome descrittivo, in quanto è possibile utilizzare questo valore per cercare la connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire informazioni aggiuntive sulla connessione di base. |
| `auth.specName` | Tipo di autenticazione utilizzato per la connessione. |
| `auth.params.endpoint` | Endpoint del server [!DNL Oracle Eloqua]. |
| `auth.params.username` | Credenziali concatenate che includono il nome del sito e il nome utente corrispondenti all&#39;account [!DNL Oracle Eloqua]. |
| `auth.params.password` | Password corrispondente all&#39;account [!DNL Oracle Eloqua]. |
| `connectionSpec.id` | Il valore per l&#39;ID della specifica di connessione dell&#39;origine [!DNL Oracle Eloqua] è fisso come: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Oracle Eloqua] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati di automazione marketing su Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
