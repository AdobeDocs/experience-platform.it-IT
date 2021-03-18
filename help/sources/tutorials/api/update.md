---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;aggiornare account
solution: Experience Platform
title: Aggiornare gli account utilizzando l’API del servizio di flusso
topic: ' - Panoramica'
type: Tutorial
description: Questa esercitazione descrive i passaggi per aggiornare i dettagli e le credenziali di un account utilizzando l’API del servizio di flusso.
translation-type: tm+mt
source-git-commit: 37be5f5ffa4640d7d4442a24cc257069237f15cb
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---


# Aggiornare gli account utilizzando l’API del servizio di flusso

In alcuni casi, potrebbe essere necessario aggiornare i dettagli di una connessione sorgente esistente. [!DNL Flow Service] consente di aggiungere, modificare ed eliminare i dettagli di una connessione batch o in streaming esistente, compresi nome, descrizione e credenziali.

Questa esercitazione descrive i passaggi per aggiornare i dettagli e le credenziali di una connessione utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Questa esercitazione richiede una connessione esistente e un ID di connessione valido. Se non disponi di una connessione esistente, seleziona l&#39;origine scelta dalla [panoramica origini](../../home.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per aggiornare correttamente una connessione utilizzando l’ API [!DNL Flow Service] .

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in Experience Platform, incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Cerca dettagli di connessione

Il primo passo per aggiornare la connessione consiste nel recuperare i relativi dettagli utilizzando l’ID di connessione. Per recuperare i dettagli correnti della connessione, invia una richiesta GET all’ [!DNL Flow Service] API fornendo l’ID di connessione della connessione che desideri aggiornare.

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

Una risposta corretta restituisce i dettagli correnti della connessione, incluse le relative credenziali, l&#39;identificatore univoco (`id`) e la versione. Il valore di versione è necessario per aggiornare la connessione.

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

Per aggiornare il nome, la descrizione e le credenziali della connessione, esegui una richiesta PATCH all’ API [!DNL Flow Service] fornendo al contempo l’ID, la versione e le nuove informazioni da utilizzare.

>[!IMPORTANT]
>
>L’intestazione `If-Match` è necessaria quando si effettua una richiesta PATCH. Il valore di questa intestazione è la versione univoca della connessione che si desidera aggiornare.

**Formato API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valore `id` univoco per la connessione che si desidera aggiornare. |

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
| `op` | Chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare la connessione. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce l&#39;ID di connessione e un tag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET all’ [!DNL Flow Service] API, fornendo al contempo l’ID di connessione.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai aggiornato le credenziali e le informazioni associate alla tua connessione utilizzando l’ API [!DNL Flow Service] . Per ulteriori informazioni sull&#39;utilizzo dei connettori sorgente, consulta la [panoramica delle sorgenti](../../home.md).
