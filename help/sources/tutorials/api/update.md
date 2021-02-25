---
keywords: ' Experience Platform;home;argomenti popolari;servizio di flusso;connessioni di aggiornamento'
solution: Experience Platform
title: Aggiornamento delle connessioni tramite l'API del servizio di flusso
topic: ' - Panoramica'
type: Tutorial
description: Questa esercitazione descrive i passaggi per aggiornare i dettagli e le credenziali di una connessione utilizzando l'API del servizio di flusso.
translation-type: tm+mt
source-git-commit: 5187647dfcf82a476bc776bf2b606db228ca70a4
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---


# Aggiornare le connessioni tramite l&#39;API del servizio di flusso

In alcuni casi, potrebbe essere necessario aggiornare i dettagli di una connessione di origine esistente. [!DNL Flow Service] consente di aggiungere, modificare ed eliminare dettagli di una connessione batch o in streaming esistente, inclusi nome, descrizione e credenziali.

Questa esercitazione descrive i passaggi per aggiornare i dettagli e le credenziali di una connessione utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Questa esercitazione richiede una connessione esistente e un ID di connessione valido. Se non si dispone di una connessione esistente, selezionare l&#39;origine di scelta tra le [origini overview](../../home.md) e seguire i passaggi descritti prima di eseguire l&#39;esercitazione.

Questa esercitazione richiede inoltre di conoscere i seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md):  Experience Platform consente l&#39;acquisizione di dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Piattaforma.
* [Sandbox](../../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per aggiornare correttamente una connessione utilizzando l&#39;API [!DNL Flow Service].

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi del Experience Platform .

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a1/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API di Experience Platform, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in  Experience Platform, incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* `Content-Type: application/json`

## Cercare i dettagli di connessione

Il primo passo per aggiornare la connessione è recuperare i dettagli utilizzando l&#39;ID di connessione. Per recuperare i dettagli correnti della connessione, effettuate una richiesta di GET all&#39;API [!DNL Flow Service] fornendo l&#39;ID connessione della connessione che desiderate aggiornare.

**Formato API**

```http
GET /connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valore `id` univoco per la connessione che si desidera recuperare. |

**Richiesta**

La seguente richiesta recupera informazioni relative alla connessione.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli correnti della connessione, incluse le relative credenziali, l&#39;identificatore univoco (`id`) e la versione. Il valore della versione è richiesto per aggiornare la connessione.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## Aggiorna connessione

Per aggiornare il nome, la descrizione e le credenziali della connessione, eseguite una richiesta PATCH all&#39;API [!DNL Flow Service] fornendo al contempo l&#39;ID connessione, la versione e le nuove informazioni che desiderate utilizzare.

>[!IMPORTANT]
>
>L&#39;intestazione `If-Match` è necessaria quando si effettua una richiesta di PATCH. Il valore di questa intestazione è la versione univoca della connessione che si desidera aggiornare.

**Formato API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valore `id` univoco per la connessione da aggiornare. |

**Richiesta**

La richiesta seguente fornisce un nuovo nome e una nuova descrizione, nonché un nuovo set di credenziali, con cui aggiornare la connessione.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `op` | Chiamata di operazione utilizzata per definire l&#39;azione necessaria per aggiornare la connessione. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce l’ID connessione e un tag aggiornato. È possibile verificare l&#39;aggiornamento eseguendo una richiesta di GET all&#39;API [!DNL Flow Service], fornendo al contempo l&#39;ID di connessione.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai aggiornato le credenziali e le informazioni associate alla tua connessione utilizzando l&#39;API [!DNL Flow Service]. Per ulteriori informazioni sull&#39;utilizzo dei connettori di origine, vedere la [panoramica delle sorgenti](../../home.md).
