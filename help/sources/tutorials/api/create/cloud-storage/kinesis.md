---
keywords: Experience Platform;home;argomenti popolari;Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Creare una connessione sorgente Amazon Kinesis utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un’origine Amazon Kinesis utilizzando l’API del servizio di flusso.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# Creare una connessione sorgente [!DNL Amazon Kinesis] utilizzando l’API del servizio di flusso

Questa esercitazione descrive i passaggi necessari per collegare [!DNL Amazon Kinesis] (in seguito denominato &quot;[!DNL Kinesis]&quot;) all’Experience Platform, utilizzando l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Kinesis] Platform utilizzando l’ API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi all&#39;account [!DNL Amazon Kinesis], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | L’ID della chiave di accesso è la metà della coppia di chiavi di accesso utilizzata per autenticare l’account [!DNL Kinesis] in Platform. |
| `secretKey` | La chiave di accesso segreta è l’altra metà della coppia di chiavi di accesso utilizzata per autenticare l’account [!DNL Kinesis] in Platform. |
| `region` | Area dell&#39;account [!DNL Kinesis]. Per ulteriori informazioni sulle aree geografiche, consulta la guida sull’ [aggiunta di indirizzi IP al tuo elenco consentiti](../../../../ip-address-allow-list.md) . |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID delle specifiche di connessione [!DNL Kinesis] è: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Per ulteriori informazioni sulle [!DNL Kinesis] chiavi di accesso e su come generarle, consulta questa [[!DNL AWS] guida sulla gestione delle chiavi di accesso per gli utenti IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Il primo passaggio nella creazione di una connessione sorgente è quello di autenticare la [!DNL Kinesis] sorgente e generare un ID di connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Kinesis] come parte dei parametri della richiesta.

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
| `auth.params.accessKeyId` | ID chiave di accesso per l&#39;account [!DNL Kinesis]. |
| `auth.params.secretKey` | Chiave di accesso segreto per l&#39;account [!DNL Kinesis]. |
| `auth.params.region` | Area dell&#39;account [!DNL Kinesis]. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

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

Per creare una connessione sorgente, effettua una richiesta POST all’ endpoint `/sourceConnections` dell’ API [!DNL Flow Service] .

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
| `baseConnectionId` | L&#39;ID di connessione di base dell&#39;origine [!DNL Kinesis] generato nel passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione fissa per [!DNL Kinesis]. Questo ID è : `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Il formato dei dati [!DNL Kinesis] da acquisire. Attualmente, l’unico formato di dati supportato è `json`. |
| `params.stream` | Nome del flusso di dati da cui estrarre i record. |
| `params.dataType` | Questo parametro definisce il tipo di dati da acquisire. I tipi di dati supportati includono: `raw` e `xdm`. |
| `params.reset` | Questo parametro definisce come verranno letti i dati. Utilizza `latest` per iniziare a leggere i dati più recenti e utilizza `earliest` per iniziare a leggere i primi dati disponibili nel flusso. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Questo ID è necessario nell’esercitazione successiva per creare un flusso di dati.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione sorgente [!DNL Kinesis] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID di connessione sorgente nell’esercitazione successiva per [creare un flusso di dati utilizzando l’ [!DNL Flow Service] API](../../collect/streaming.md).
