---
keywords: Experience Platform;home;argomenti popolari;redshift;Redshift;Amazon Redshift;amazon redshift
solution: Experience Platform
title: Creare una connessione di base Amazon Redshift utilizzando l’API del servizio Flow
type: Tutorial
description: Scopri come collegare Adobe Experience Platform ad Amazon Redshift utilizzando l’API del servizio Flow.
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# Creare un [!DNL Amazon Redshift] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Amazon Redshift] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Amazon Redshift] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Amazon Redshift], è necessario fornire le seguenti proprietà di connessione:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| `server` | Il server associato al tuo [!DNL Amazon Redshift] account. |
| `username` | Il nome utente associato al tuo [!DNL Amazon Redshift] account. |
| `password` | La password associata al tuo [!DNL Amazon Redshift] account. |
| `database` | Il [!DNL Amazon Redshift] database a cui si sta effettuando l&#39;accesso. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Amazon Redshift] è `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Per ulteriori informazioni su come iniziare, consulta questa [[!DNL Amazon Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

>[!NOTE]
>
>Standard di codifica predefinito per [!DNL Redshift] è Unicode. Questo non può essere modificato.

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Amazon Redshift] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Amazon Redshift]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| ------------- | --------------- |
| `auth.params.server` | Il tuo [!DNL Amazon Redshift] server. |
| `auth.params.database` | Il database associato al tuo [!DNL Amazon Redshift] account. |
| `auth.params.password` | La password associata al tuo [!DNL Amazon Redshift] account. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Amazon Redshift] account. |
| `connectionSpec.id` | Il [!DNL Amazon Redshift] ID specifica di connessione: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un’ [!DNL Amazon Redshift] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati del database su Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
