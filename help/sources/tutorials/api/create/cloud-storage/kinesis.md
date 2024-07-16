---
title: Creare una connessione Amazon Kinesis Source utilizzando l’API del servizio Flusso
description: Scopri come collegare Adobe Experience Platform a un’origine Amazon Kinesis utilizzando l’API del servizio Flusso.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 4%

---

# Creare una connessione di origine [!DNL Amazon Kinesis] utilizzando l&#39;API del servizio Flusso

>[!IMPORTANT]
>
>L&#39;origine [!DNL Amazon Kinesis] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial illustra i passaggi necessari per connettere ad Experience Platform [!DNL Amazon Kinesis] (di seguito &quot;[!DNL Kinesis]&quot;) utilizzando l&#39;API [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettere correttamente [!DNL Kinesis] a Platform utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi al tuo account [!DNL Amazon Kinesis], devi fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | L&#39;ID della chiave di accesso è la metà della coppia di chiavi di accesso utilizzata per autenticare l&#39;account [!DNL Kinesis] in Platform. |
| `secretKey` | La chiave di accesso segreta è l&#39;altra metà della coppia di chiavi di accesso utilizzata per autenticare l&#39;account [!DNL Kinesis] in Platform. |
| `region` | Area geografica del tuo account [!DNL Kinesis]. Per ulteriori informazioni sulle aree geografiche, consulta la guida sull&#39;[aggiunta di indirizzi IP all&#39;elenco consentiti](../../../../ip-address-allow-list.md). |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Per ulteriori informazioni sulle chiavi di accesso [!DNL Kinesis] e su come generarle, consultare questa [[!DNL AWS] guida sulla gestione delle chiavi di accesso per gli utenti IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Il primo passaggio nella creazione di una connessione di origine consiste nell&#39;autenticare l&#39;origine [!DNL Kinesis] e generare un ID connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare elementi specifici da acquisire, incluse informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Kinesis] come parte dei parametri della richiesta.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.accessKeyId` | ID della chiave di accesso per l&#39;account [!DNL Kinesis]. |
| `auth.params.secretKey` | Chiave di accesso segreta per l&#39;account [!DNL Kinesis]. |
| `auth.params.region` | Area geografica del tuo account [!DNL Kinesis]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Creare una connessione sorgente {#source}

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali origine dati, formato dati e ID della connessione di origine necessari per creare un flusso di dati. Un&#39;istanza della connessione di origine è specifica di un tenant e di un&#39;organizzazione.

Per creare una connessione di origine, effettuare una richiesta POST all&#39;endpoint `/sourceConnections` dell&#39;API [!DNL Flow Service].

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto può essere utilizzato per cercare informazioni sulla connessione sorgente. |
| `description` | Valore facoltativo che è possibile fornire per includere ulteriori informazioni sulla connessione di origine. |
| `baseConnectionId` | ID della connessione di base dell&#39;origine [!DNL Kinesis] generato nel passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione fissa per [!DNL Kinesis]. ID: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Formato dei dati [!DNL Kinesis] che si desidera acquisire. Attualmente, l&#39;unico formato di dati supportato è `json`. |
| `params.stream` | Nome del flusso di dati da cui estrarre i record. |
| `params.dataType` | Questo parametro definisce il tipo di dati che viene acquisito. I tipi di dati supportati sono: `raw` e `xdm`. |
| `params.reset` | Questo parametro definisce la modalità di lettura dei dati. Utilizza `latest` per iniziare a leggere dai dati più recenti e `earliest` per iniziare a leggere dai primi dati disponibili nel flusso. |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di origine appena creata. Questo ID è richiesto nell’esercitazione successiva per creare un flusso di dati.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione sorgente [!DNL Kinesis] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di origine nella prossima esercitazione per [creare un flusso di dati in streaming utilizzando l&#39; [!DNL Flow Service] API](../../collect/streaming.md).
