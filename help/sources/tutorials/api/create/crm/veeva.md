---
keywords: Experience Platform;home;argomenti popolari;veeva crm;Veeva CRM;Veeva;
solution: Experience Platform
title: Creare una connessione di base a Veeva CRM utilizzando l’API del servizio di flusso
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Veeva CRM utilizzando l’API del servizio Flusso.
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 5%

---

# Creare una connessione di base [!DNL Veeva CRM] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Veeva CRM] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Guida introduttuva

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Veeva CRM] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Veeva CRM], è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `environmentUrl` | URL dell&#39;istanza [!DNL Veeva CRM]. |
| `username` | Il valore del nome utente dell&#39;account [!DNL Veeva CRM]. |
| `password` | Il valore della password dell&#39;account [!DNL Veeva CRM]. |
| `securityToken` | Token di sicurezza per l&#39;istanza [!DNL Veeva CRM]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Per ulteriori informazioni su questi valori, fare riferimento a questo [[!DNL Veeva CRM] documento](https://developer.veevacrm.com/doc/Content/rest-api.htm).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Veeva CRM] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Veeva CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --- | --- |
| `name` | Nome della connessione di base [!DNL Veeva CRM]. È possibile utilizzare questo nome per cercare la connessione di base [!DNL Veeva CRM]. |
| `description` | Descrizione facoltativa della connessione di base [!DNL Veeva CRM]. |
| `auth.specName` | Tipo di autenticazione utilizzato per la connessione. |
| `auth.params.environmentUrl` | URL dell&#39;istanza [!DNL Veeva CRM]. |
| `auth.params.username` | Il valore del nome utente dell&#39;account [!DNL Veeva CRM]. |
| `auth.params.password` | Il valore della password dell&#39;account [!DNL Veeva CRM]. |
| `auth.params.securityToken` | Token di sicurezza per l&#39;istanza [!DNL Veeva CRM]. |
| `connectionSpec.id` | ID della specifica di connessione per [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Veeva CRM] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati CRM in Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/crm.md)
