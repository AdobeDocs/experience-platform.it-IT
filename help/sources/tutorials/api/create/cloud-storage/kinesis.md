---
keywords: Experience Platform;home;argomenti popolari;Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Creare una connessione sorgente Amazon Kinesis utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un account Kinesis Amazon utilizzando l’API del servizio di flusso.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
translation-type: tm+mt
source-git-commit: d6f1521470b8dc630060584189690545c724de6b
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 2%

---

# Creare una connessione sorgente [!DNL Amazon Kinesis] utilizzando l’API del servizio di flusso

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Questa esercitazione utilizza l’ API [!DNL Flow Service] per seguire i passaggi necessari per la connessione di [!DNL Experience Platform] a un account [!DNL Amazon Kinesis].

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a un account [!DNL Amazon Kinesis] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi all&#39;account [!DNL Amazon Kinesis], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | ID chiave di accesso per l&#39;account [!DNL Kinesis]. |
| `secretKey` | Chiave di accesso segreto per l&#39;account [!DNL Kinesis]. |
| `region` | Area dell&#39;account [!DNL Kinesis]. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

Per ulteriori informazioni su questi valori, consulta [questo documento Kinesis](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL Amazon Kinesis] in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

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
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region: "{REGION}
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
| `auth.params.region` | Area dell&#39;account [!DNL Kinesis]. Per ulteriori informazioni sulle aree geografiche, consulta il documento sull&#39; [elenco consentiti dell&#39;indirizzo IP](../../../../ip-address-allow-list.md) |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso l’identificatore univoco (`id`). Questo ID è necessario per esplorare i dati di archiviazione cloud nell’esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Amazon Kinesis] utilizzando le API e come parte del corpo della risposta è stato ottenuto un ID univoco. Puoi usare questo ID connessione per [raccogliere dati in streaming utilizzando l&#39;API del servizio di flusso](../../collect/streaming.md).
