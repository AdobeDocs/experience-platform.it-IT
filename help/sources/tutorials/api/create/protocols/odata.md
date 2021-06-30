---
keywords: Experience Platform;home;argomenti popolari;OData generico;dati generici
solution: Experience Platform
title: Creare una connessione di base OData generica utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare OData generico a Adobe Experience Platform utilizzando l’API del servizio di flusso.
exl-id: 45b302cb-1a43-4fab-a8a2-cb4e1ee129f9
source-git-commit: 3dd7266451eada02a2342bbba5f3cf6c327529d6
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# Creare una connessione di base [!DNL Generic OData] utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>Il connettore [!DNL Generic OData] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Generic OData] utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Generic OData] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Generic OData], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | URL principale del servizio [!DNL Generic OData]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL Generic Generic OData] è: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`. |

Per ulteriori informazioni su come iniziare, consulta [this [!DNL Generic OData] document](https://www.odata.org/getting-started/basic-tutorial/).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Generic OData] come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per [!DNL Generic OData]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Protocols",
        "description": "A test connection for a Protocols source",
        "auth": {
            "specName": "Anonymous Authentication",
        "params": {
            "url" :  "{URL}"
            }
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.url` | Host del server [!DNL Generic OData]. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Generic OData]: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`. |

**Risposta**

Una risposta corretta restituisce la nuova connessione appena creata, incluso l&#39;identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
    "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL OData] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi usare questo ID nell&#39;esercitazione successiva per imparare a [esplorare le applicazioni a protocolli utilizzando l&#39;API del servizio di flusso](../../explore/protocols.md).
