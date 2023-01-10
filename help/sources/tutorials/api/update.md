---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;aggiornare account
solution: Experience Platform
title: Aggiornare gli account utilizzando l’API del servizio di flusso
type: Tutorial
description: Questa esercitazione descrive i passaggi per aggiornare i dettagli e le credenziali di un account utilizzando l’API del servizio di flusso.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 3%

---

# Aggiornare gli account utilizzando l’API del servizio di flusso

In alcuni casi, potrebbe essere necessario aggiornare i dettagli di una connessione sorgente esistente. [!DNL Flow Service] consente di aggiungere, modificare ed eliminare i dettagli di una connessione batch o in streaming esistente, compresi nome, descrizione e credenziali.

Questa esercitazione descrive i passaggi per aggiornare i dettagli e le credenziali di una connessione utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa esercitazione richiede una connessione esistente e un ID di connessione valido. Se non disponi di una connessione esistente, seleziona l&#39;origine scelta dalla [panoramica di origini](../../home.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Cerca dettagli di connessione

Il primo passo per aggiornare la connessione consiste nel recuperare i relativi dettagli utilizzando l’ID di connessione. Per recuperare i dettagli correnti della connessione, invia una richiesta di GET al [!DNL Flow Service] mentre fornisci l’ID di connessione della connessione che desideri aggiornare.

**Formato API**

```http
GET /connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | L&#39;unico `id` valore della connessione che si desidera recuperare. |

**Richiesta**

La seguente richiesta recupera informazioni relative alla connessione.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli correnti della connessione, incluse le relative credenziali, l&#39;identificatore univoco (`id`) e versione . Il valore di versione è necessario per aggiornare la connessione.

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

Per aggiornare il nome, la descrizione e le credenziali della tua connessione, esegui una richiesta PATCH al [!DNL Flow Service] , fornendo al tempo stesso il tuo ID connessione, la versione e le nuove informazioni che desideri utilizzare.

>[!IMPORTANT]
>
>La `If-Match` l’intestazione è necessaria quando si effettua una richiesta PATCH. Il valore di questa intestazione è la versione univoca della connessione che si desidera aggiornare.

**Formato API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | L&#39;unico `id` valore della connessione che si desidera aggiornare. |

**Richiesta**

La richiesta seguente fornisce un nuovo nome e una nuova descrizione, nonché un nuovo set di credenziali, con cui aggiornare la connessione.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare la connessione. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Percorso del parametro da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce l&#39;ID di connessione e un tag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso l&#39;ID di connessione.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai aggiornato le credenziali e le informazioni associate alla tua connessione utilizzando [!DNL Flow Service] API. Per ulteriori informazioni sull’utilizzo dei connettori sorgente, consulta la sezione [panoramica di origini](../../home.md).
