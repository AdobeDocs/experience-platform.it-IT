---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creazione di una connessione di base di Experienci Platform  tramite l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---


# Creazione di una connessione di base [!DNL Experience Platform] di set di dati tramite l&#39; [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Per collegare i dati da un&#39;origine di terze parti a [!DNL Platform], è innanzitutto necessario stabilire una connessione alla base di dati.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per guidarvi nei passaggi necessari per creare una connessione di base per i dataset.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

* [Sistema](../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Schema Guida](../../../xdm/api/getting-started.md)per lo sviluppatore del Registro di sistema: Include informazioni importanti che è necessario conoscere per eseguire correttamente le chiamate all&#39;API del Registro di sistema dello schema. Ciò include il vostro `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all’intestazione Accetta e ai suoi possibili valori).
* [Servizio](../../../catalog/home.md)catalogo: Catalogo è il sistema di registrazione per la posizione dei dati e la linea all&#39;interno [!DNL Experience Platform].
* [Caricamento](../../../ingestion/batch-ingestion/overview.md)batch: L&#39;API di assimilazione batch consente di assimilare i dati  Experience Platform come file batch.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a Data Lake tramite l&#39; [!DNL Flow Service] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Cercare le specifiche di connessione

Il primo passaggio per la creazione di una connessione di base di dataset consiste nel recuperare una serie di specifiche di connessione dall&#39;interno [!DNL Flow Service].

**Formato API**

Ogni origine disponibile dispone di un proprio set di specifiche di connessione per descrivere le proprietà del connettore, ad esempio i requisiti di autenticazione. È possibile ricercare le specifiche di connessione per una connessione di base di dataset eseguendo una richiesta di GET e utilizzando i parametri di query.

L&#39;invio di una richiesta di GET senza parametri di query restituirà le specifiche di connessione per tutte le origini disponibili. È possibile includere la query `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` per ottenere informazioni per la connessione di base del dataset.

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**Richiesta**

La richiesta seguente recupera le specifiche di connessione per una connessione di base di dataset.

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

## Creazione di una connessione di base di dataset

Una connessione di base specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione alla base di dati, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

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

Una risposta corretta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per creare una connessione di destinazione e acquisire i dati da un connettore di origine di terze parti.

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione di base di dati tramite l&#39; [!DNL Flow Service] API e hai ottenuto il valore ID univoco della connessione. È possibile utilizzare questa connessione di base per creare una connessione di destinazione. Le seguenti esercitazioni descrivono i passaggi necessari per creare una connessione di destinazione, a seconda della categoria di connettore di origine utilizzata:

* [Archiviazione cloud](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [Successo cliente](./collect/customer-success.md)
* [Database](./collect/database-nosql.md)