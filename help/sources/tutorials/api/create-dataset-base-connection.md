---
keywords: Experience Platform;home;argomenti popolari;servizio flusso connessione set di dati;servizio flusso;connessione servizio flusso
solution: Experience Platform
title: Creare una connessione di base del set di dati Adobe Experience Platform utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come utilizzare l’API del servizio Flusso per creare una connessione di base a set di dati a Adobe Experience Platform.
exl-id: 5e829f4a-954b-4011-a003-c42c7a0d5617
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---

# Creare una connessione a una base di dati [!DNL Experience Platform] utilizzando l&#39;API [!DNL Flow Service]

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Per collegare i dati da un’origine di terze parti a [!DNL Platform], è innanzitutto necessario stabilire una connessione alla base di dati.

Questa esercitazione utilizza l’ API [!DNL Flow Service] per illustrarti i passaggi necessari per creare una connessione di base a set di dati.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../xdm/home.md) Experience Data Model (XDM): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Guida](../../../xdm/api/getting-started.md) per gli sviluppatori del Registro di schema: Include informazioni importanti da conoscere per eseguire correttamente le chiamate all’API del Registro di sistema dello schema. Questo include il tuo `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni richieste per fare richieste (con particolare attenzione all&#39;intestazione Accept e ai suoi possibili valori).
* [Servizio](../../../catalog/home.md) catalogo: Catalogo è il sistema di registrazione per la posizione dei dati e la derivazione all&#39;interno di  [!DNL Experience Platform].
* [Acquisizione](../../../ingestion/batch-ingestion/overview.md) batch: L’API di acquisizione batch ti consente di inserire dati in Experience Platform come file batch.
* [Sandbox](../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a Data Lake utilizzando l&#39;API [!DNL Flow Service].

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Cercare le specifiche di connessione

Il primo passaggio nella creazione di una connessione alla base di dati è quello di recuperare un set di specifiche di connessione dall&#39;interno di [!DNL Flow Service].

**Formato API**

Ogni sorgente disponibile dispone di un proprio set di specifiche di connessione per descrivere le proprietà del connettore, ad esempio i requisiti di autenticazione. È possibile cercare le specifiche di connessione per una connessione di base a un set di dati eseguendo una richiesta di GET e utilizzando i parametri di query.

L’invio di una richiesta di GET senza parametri di query restituirà le specifiche di connessione per tutte le origini disponibili. Puoi includere la query `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` per ottenere informazioni per la connessione di base al set di dati.

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**Richiesta**

La richiesta seguente recupera le specifiche di connessione per una connessione di base di set di dati.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce le specifiche di connessione e l&#39;identificatore univoco (`id`) necessari per creare una connessione di base.

```json
{
    "items": [
        {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "name": "{NAME}",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "targetSpec": {
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "dataSetId": {
                            "type": "string"
                        }
                    },
                    "required": [
                        "dataSetId"
                    ]
                }
            },
            "attributes": {
                "category": "{CATEGORY}"
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Creare una connessione di base di set di dati

Una connessione di base specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione base di set di dati, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

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
        "name": "Dataset Base Connection",
        "description": "Dataset Base Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| ------------- | --------------- |
| `connectionSpec.id` | Specifica di connessione `id` recuperata nel passaggio precedente. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per creare una connessione di destinazione e acquisire dati da un connettore di origine di terze parti.

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione di base di dati utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. È possibile utilizzare questa connessione di base per creare una connessione di destinazione. Le seguenti esercitazioni illustrano i passaggi necessari per creare una connessione di destinazione, a seconda della categoria di connettore di origine in uso:

* [archiviazione cloud](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [Successo del cliente](./collect/customer-success.md)
* [Database](./collect/database-nosql.md)
