---
keywords: Experience Platform;home;argomenti popolari;Azure;Azure File Storage;Azure file storage
solution: Experience Platform
title: Creare una connessione di base di archiviazione file di Azure utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Azure File Storage a Adobe Experience Platform utilizzando l’API del servizio di flusso.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Crea un [!DNL Azure File Storage] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Azure File Storage] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Azure File Storage] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Azure File Storage], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Il punto finale del [!DNL Azure File Storag]Istanza a cui si accede. |
| `userId` | L&#39;utente con accesso sufficiente al [!DNL Azure File Storage] punto finale. |
| `password` | La password [!DNL Azure File Storage] istanza |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Azure File Storage] è: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

Per ulteriori informazioni su come iniziare, consulta [questo documento di archiviazione file di Azure](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Azure File Storage] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Azure File Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | Il punto finale del [!DNL Azure File Storage] istanza a cui si accede. |
| `auth.params.userId` | L&#39;utente con accesso sufficiente al [!DNL Azure File Storage] punto finale. |
| `auth.params.password` | La [!DNL Azure File Storage] chiave di accesso. |
| `connectionSpec.id` | La [!DNL Azure File Storage] ID specifica di connessione: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Azure File Storage] connessione tramite [!DNL Flow Service] e hanno ottenuto il valore ID univoco della connessione. Puoi usare questo ID nell&#39;esercitazione successiva per scoprire come [esplorare un archivio cloud di terze parti utilizzando l’API del servizio di flusso](../../explore/cloud-storage.md).
