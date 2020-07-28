---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Kinesis Amazon  utilizzando l'API di servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 11431ffcfc2204931fe3e863bfadc7878a40b49c
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 2%

---


# Creazione di un [!DNL Amazon Kinesis] connettore tramite l&#39;API del servizio di flusso

>[!NOTE]
>Il [!DNL Amazon Kineses] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per illustrare i passaggi necessari per connettersi [!DNL Experience Platform] a un [!DNL Amazon Kinesis] account.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrete conoscere per collegarvi correttamente a un [!DNL Amazon Kinesis] account utilizzando l&#39; [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] connettersi all&#39; [!DNL Amazon Kinesis] account, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | ID chiave di accesso per il tuo [!DNL Kinesis] account. |
| `secretKey` | La chiave di accesso segreta per il tuo [!DNL Kinesis] account. |
| `region` |  | Regione per il tuo [!DNL Kinesis] account. |
| `connectionSpec.id` | ID specifica [!DNL Kinesis] connessione: `86043421-563b-46ec-8e6c-e23184711bf6` |

Per ulteriori informazioni su questi valori, consultare [questo documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)Kinesis.

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

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per [!DNL Amazon Kinesis] account, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

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
        "auth": {
            "specName": "Basic Authentication for Kinesis",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretKey": "secretKey"
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
| `auth.params.accessKeyId` | ID chiave di accesso per il tuo [!DNL Kinesis] account. |
| `auth.params.secretKey` | La chiave di accesso segreta per il tuo [!DNL Kinesis] account. |
| `auth.params.region` | Regione per il tuo [!DNL Kinesis] account. |
| `connectionSpec.id` | ID specifica [!DNL Kinesis] connessione: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati di archiviazione cloud nell&#39;esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, avete creato una [!DNL Amazon Kinesis] connessione utilizzando le API e un ID univoco è stato ottenuto come parte del corpo della risposta. Puoi utilizzare questo ID connessione per [esplorare gli storage cloud utilizzando l&#39;API](../../explore/cloud-storage.md)del servizio di flusso.