---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore BLOB di Azure utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 11431ffcfc2204931fe3e863bfadc7878a40b49c
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---


# Creare un [!DNL Azure Blob] connettore utilizzando l&#39; [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per guidarvi attraverso i passaggi necessari per collegarvi [!DNL Experience Platform] a un archivio [!DNL Azure Blob] (in seguito denominato &quot;Blob&quot;).

Se si preferisce utilizzare l&#39;interfaccia utente in [!DNL Experience Platform], l&#39;esercitazione [dell&#39;interfaccia utente del connettore di origine](../../../ui/create/cloud-storage/blob-s3.md) Azure Blob o  Amazon S3 fornisce istruzioni dettagliate per eseguire azioni simili.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a un archivio Blob tramite l&#39; [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] connettersi all&#39;archivio Blob, è necessario specificare i valori per la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione necessaria per accedere ai dati nell&#39;archivio Blob. Il pattern della stringa di connessione BLOB è: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per Blob è: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

Per ulteriori informazioni su come ottenere una stringa di connessione, fare riferimento a [questo documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)Azure Blob.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti al gruppo [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per account Blob, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione Blob, è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta POST. L&#39;ID della specifica di connessione per Blob è `4c10e202-c428-4796-9208-5f1f5732b1cf`.

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Blob Connection",
        "description": "Cnnection for an Azure Blob account",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.connectionString` | Stringa di connessione necessaria per accedere ai dati nell&#39;archivio Blob. Il pattern della stringa di connessione BLOB è: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione di archiviazione BLOB è: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare l&#39;archiviazione nell&#39;esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione Blob utilizzando le API e un ID univoco è stato ottenuto come parte del corpo della risposta. Potete utilizzare questo ID connessione per [esplorare gli storage cloud utilizzando l&#39;API](../../explore/cloud-storage.md) del servizio di flusso o per [assimilare i dati del parquet tramite l&#39;API](../../cloud-storage-parquet.md)del servizio di flusso.