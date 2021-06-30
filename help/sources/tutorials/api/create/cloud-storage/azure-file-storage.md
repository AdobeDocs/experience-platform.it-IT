---
keywords: Experience Platform;home;argomenti popolari;Azure;Azure File Storage;Azure file storage
solution: Experience Platform
title: Creare una connessione di base di archiviazione file di Azure utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Azure File Storage a Adobe Experience Platform utilizzando l’API del servizio di flusso.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Creare una connessione di base [!DNL Azure File Storage] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Azure File Storage] utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Azure File Storage] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Azure File Storage], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Endpoint dell&#39;istanza [!DNL Azure File Storag]e a cui si accede. |
| `userId` | L’utente con accesso sufficiente all’endpoint [!DNL Azure File Storage]. |
| `password` | La password per la tua istanza [!DNL Azure File Storage] |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL Azure File Storage] è: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

Per ulteriori informazioni su come iniziare, consulta [questo documento Azure File Storage](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Azure File Storage] come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per [!DNL Azure File Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.host` | Endpoint dell&#39;istanza [!DNL Azure File Storage] a cui si accede. |
| `auth.params.userId` | L’utente con accesso sufficiente all’endpoint [!DNL Azure File Storage]. |
| `auth.params.password` | Chiave di accesso [!DNL Azure File Storage]. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Azure File Storage]: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Azure File Storage] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nell&#39;esercitazione successiva per scoprire come [esplorare un&#39;archiviazione cloud di terze parti utilizzando l&#39;API del servizio di flusso](../../explore/cloud-storage.md).
