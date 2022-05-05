---
keywords: Experience Platform;home;argomenti popolari;rossa;Redshift;Amazon Redshift;amazon redshift
solution: Experience Platform
title: Creare una connessione di base Amazon Redshift utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Amazon Redshift utilizzando l’API del servizio di flusso.
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: c0d750ef61ad2e295568cccabca5c52a758997c2
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# Crea un [!DNL Amazon Redshift] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Amazon Redshift] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Amazon Redshift] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Amazon Redshift], è necessario fornire le seguenti proprietà di connessione:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| `server` | Il server associato al [!DNL Amazon Redshift] conto. |
| `username` | Il nome utente associato al tuo [!DNL Amazon Redshift] conto. |
| `password` | La password associata al [!DNL Amazon Redshift] conto. |
| `database` | La [!DNL Amazon Redshift] database a cui si accede. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Amazon Redshift] è `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Per ulteriori informazioni su come iniziare, consulta questo articolo [[!DNL Amazon Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

>[!NOTE]
>
>Standard di codifica predefinito per [!DNL Redshift] è Unicode. Questo non può essere modificato.

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Amazon Redshift] credenziali di autenticazione come parte dei parametri della richiesta.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.server` | Le [!DNL Amazon Redshift] server. |
| `auth.params.database` | Il database associato al [!DNL Amazon Redshift] conto. |
| `auth.params.password` | La password associata al [!DNL Amazon Redshift] conto. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL Amazon Redshift] conto. |
| `connectionSpec.id` | La [!DNL Amazon Redshift] ID specifica di connessione: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Amazon Redshift] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per trasferire i dati di database a Platform utilizzando [!DNL Flow Service] API](../../collect/database-nosql.md)
