---
keywords: Experience Platform;home;argomenti popolari;couchbase;Couchbase
solution: Experience Platform
title: Creare una connessione di base Couchbase utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Couchbase a Adobe Experience Platform utilizzando l’API del servizio di flusso.
exl-id: 625e3acf-fc27-44cf-b4e6-becf1d107ff2
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# Creare una connessione di base [!DNL Couchbase] utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>Il connettore [!DNL Couchbase] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Couchbase] utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Couchbase] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione utilizzata per connettersi all&#39;istanza [!DNL Couchbase]. Il pattern della stringa di connessione per [!DNL Couchbase] è `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Per ulteriori informazioni sull&#39;acquisizione di una stringa di connessione, vedere [questo documento Couchbase](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL Couchbase] è `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Couchbase] come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per [!DNL Couchbase]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Couchbase test connection",
        "description": "A test connection for a Couchbase source",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                    "connectionString": "Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];"
                }
        },
        "connectionSpec": {
            "id": "1fe283f6-9bec-11ea-bb37-0242ac130002",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.connectionString` | Stringa di connessione utilizzata per la connessione a un account [!DNL Couchbase]. Il pattern della stringa di connessione è: `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Couchbase]: `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "54997109-07b5-40b7-9971-0907b5a0b75a",
    "etag": "\"280168f5-0000-0200-0000-5ed72b230000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Couchbase] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID nell&#39;esercitazione successiva per scoprire come [esplorare i database utilizzando l&#39;API del servizio di flusso](../../explore/database-nosql.md).
