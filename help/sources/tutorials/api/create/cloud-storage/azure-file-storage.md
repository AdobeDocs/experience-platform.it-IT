---
keywords: Experience Platform;home;argomenti comuni;Azure;Azure File Storage;Azure file storage
solution: Experience Platform
title: Creare una connessione di base per l’archiviazione dei file di Azure utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come collegare Azure File Storage a Adobe Experience Platform utilizzando l’API del servizio Flusso.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Creare un [!DNL Azure File Storage] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Azure File Storage] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Azure File Storage] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Azure File Storage], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Endpoint del [!DNL Azure File Storag]Istanza a cui si sta effettuando l&#39;accesso. |
| `userId` | L’utente con un accesso sufficiente al [!DNL Azure File Storage] endpoint. |
| `password` | La password per [!DNL Azure File Storage] istanza |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Azure File Storage] è: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

Per ulteriori informazioni su come iniziare, consulta [questo documento di Azure File Storage](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Azure File Storage] credenziali di autenticazione come parte dei parametri della richiesta.

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
| `auth.params.host` | Endpoint del [!DNL Azure File Storage] istanza a cui si sta effettuando l’accesso. |
| `auth.params.userId` | L’utente con un accesso sufficiente al [!DNL Azure File Storage] endpoint. |
| `auth.params.password` | Il [!DNL Azure File Storage] chiave di accesso. |
| `connectionSpec.id` | Il [!DNL Azure File Storage] ID specifica di connessione: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un’ [!DNL Azure File Storage] connessione tramite [!DNL Flow Service] e hanno ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nel prossimo tutorial mentre apprendi come [esplorare un’archiviazione cloud di terze parti utilizzando l’API del servizio Flow](../../explore/cloud-storage.md).
