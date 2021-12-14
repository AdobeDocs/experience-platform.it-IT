---
keywords: Experience Platform;home;argomenti popolari;Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Creare una connessione sorgente Amazon Kinesis utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un’origine Amazon Kinesis utilizzando l’API del servizio di flusso.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# Crea un [!DNL Amazon Kinesis] connessione sorgente tramite l’API del servizio di flusso

Questa esercitazione descrive i passaggi per la connessione [!DNL Amazon Kinesis] (in appresso denominato &quot;[!DNL Kinesis]&quot;) ad Experience Platform, utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente l’acquisizione di dati da varie sorgenti e allo stesso tempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente [!DNL Kinesis] su Platform utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Amazon Kinesis] account, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | L&#39;ID della chiave di accesso è la metà della coppia della chiave di accesso utilizzata per autenticare il tuo [!DNL Kinesis] a Platform. |
| `secretKey` | La chiave di accesso segreta è l&#39;altra metà della coppia di chiavi di accesso utilizzata per autenticare il tuo [!DNL Kinesis] a Platform. |
| `region` | La regione per la [!DNL Kinesis] conto. Consulta la guida su [aggiunta di indirizzi IP all’elenco consentiti](../../../../ip-address-allow-list.md) per ulteriori informazioni sulle regioni. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. La [!DNL Kinesis] ID della specifica di connessione: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Per ulteriori informazioni su [!DNL Kinesis] le chiavi di accesso e le modalità di generazione, fai riferimento a questo [[!DNL AWS] guida sulla gestione delle chiavi di accesso per gli utenti IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Il primo passaggio nella creazione di una connessione sorgente è quello di autenticare il [!DNL Kinesis] e genera un ID di connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Kinesis] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.accessKeyId` | ID chiave di accesso per il tuo [!DNL Kinesis] conto. |
| `auth.params.secretKey` | Chiave di accesso segreto per il tuo [!DNL Kinesis] conto. |
| `auth.params.region` | La regione per la [!DNL Kinesis] conto. |
| `connectionSpec.id` | La [!DNL Kinesis] ID specifica di connessione: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Creazione di una connessione sorgente {#source}

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali l’origine dati, il formato dati e l’ID di connessione di origine necessari per creare un flusso di dati. Un’istanza di connessione di origine è specifica per un tenant e un’organizzazione IMS.

Per creare una connessione di origine, invia una richiesta POST al `/sourceConnections` punto finale [!DNL Flow Service] API.

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione sorgente. |
| `description` | Valore facoltativo che è possibile fornire per includere ulteriori informazioni sulla connessione sorgente. |
| `baseConnectionId` | L&#39;ID di connessione di base del [!DNL Kinesis] origine generata nel passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione fissa per [!DNL Kinesis]. Questo ID è: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Il formato del [!DNL Kinesis] dati da acquisire. Attualmente, l’unico formato di dati supportato è `json`. |
| `params.stream` | Nome del flusso di dati da cui estrarre i record. |
| `params.dataType` | Questo parametro definisce il tipo di dati da acquisire. I tipi di dati supportati includono: `raw` e `xdm`. |
| `params.reset` | Questo parametro definisce come verranno letti i dati. Utilizzo `latest` per iniziare a leggere dai dati più recenti e utilizzare `earliest` per iniziare a leggere dai primi dati disponibili nel flusso. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Questo ID è necessario nell’esercitazione successiva per creare un flusso di dati.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Kinesis] connessione di origine tramite [!DNL Flow Service] API. Puoi usare questo ID di connessione sorgente nell’esercitazione successiva per [creare un flusso di dati in streaming utilizzando [!DNL Flow Service] API](../../collect/streaming.md).
