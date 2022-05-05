---
keywords: Experience Platform;home;argomenti popolari;veeva crm;Veeva CRM;Veeva;
solution: Experience Platform
title: Creare una connessione di base Veeva CRM utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Veeva CRM utilizzando l’API del servizio di flusso.
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---

# Crea un [!DNL Veeva CRM] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Veeva CRM] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Veeva CRM] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Veeva CRM], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `environmentUrl` | L’URL della [!DNL Veeva CRM] istanza. |
| `username` | Il valore del nome utente del tuo [!DNL Veeva CRM] conto. |
| `password` | Il valore della password [!DNL Veeva CRM] conto. |
| `securityToken` | Token di sicurezza per il [!DNL Veeva CRM] istanza. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Veeva CRM] è: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Per ulteriori informazioni su questi valori, consulta [[!DNL Veeva CRM] documento](https://developer.veevacrm.com/api/#order-management-rest-api).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Veeva CRM] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Veeva CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --- | --- |
| `name` | Il nome del tuo [!DNL Veeva CRM] connessione di base. Puoi usare questo nome per cercare il tuo [!DNL Veeva CRM] connessione di base. |
| `description` | Una descrizione facoltativa per le [!DNL Veeva CRM] connessione di base. |
| `auth.specName` | Tipo di autenticazione utilizzato per la connessione. |
| `auth.params.environmentUrl` | L’URL della [!DNL Veeva CRM] istanza. |
| `auth.params.username` | Il valore del nome utente del tuo [!DNL Veeva CRM] conto. |
| `auth.params.password` | Il valore della password [!DNL Veeva CRM] conto. |
| `auth.params.securityToken` | Token di sicurezza per il [!DNL Veeva CRM] istanza. |
| `connectionSpec.id` | ID della specifica di connessione per [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Veeva CRM] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per portare i dati CRM in Platform utilizzando [!DNL Flow Service] API](../../collect/crm.md)
