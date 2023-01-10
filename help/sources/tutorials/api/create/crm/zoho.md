---
keywords: Experience Platform;home;argomenti popolari;Zoho CRM;zoho crm;Zoho;zoho;zoho
solution: Experience Platform
title: Creare una connessione di base Zoho CRM utilizzando l’API del servizio di flusso
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Zoho CRM utilizzando l’API del servizio di flusso.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# Crea un [!DNL Zoho CRM] connessione di base utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Zoho CRM] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Zoho CRM] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Zoho CRM], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| `endpoint` | Il punto finale del [!DNL Zoho CRM] server a cui si sta effettuando la richiesta. |
| `accountsUrl` | L’URL dell’account viene utilizzato per generare i token di accesso e aggiornamento. L&#39;URL deve essere specifico del dominio. |
| `clientId` | L&#39;ID client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| `clientSecret` | Il segreto client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| `accessToken` | Il token di accesso autorizza l’accesso sicuro e temporaneo al tuo [!DNL Zoho CRM] conto. |
| `refreshToken` | Un token di aggiornamento è un token utilizzato per generare un nuovo token di accesso, una volta scaduto il token di accesso. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Zoho CRM] è: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Per ulteriori informazioni su queste credenziali, consulta la documentazione su [[!DNL Zoho CRM] autenticazione](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Zoho CRM] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

>[!TIP]
>
>Il dominio dell&#39;URL degli account deve corrispondere alla posizione di dominio appropriata. Di seguito sono riportati i vari domini e gli URL dei loro account corrispondenti:<ul><li>Stati Uniti: https://accounts.zoho.com</li><li>Australia: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>Cina: https://accounts.zoho.com.cn</li></ul>

La richiesta seguente crea una connessione di base per [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Zoho CRM base connection",
        "description": "Base Connection for Zoho CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "accountsUrl": "{ACCOUNTS_URL}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "929e4450-0237-4ed2-9404-b7e1e0a00309",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --- | --- |
| `name` | Il nome del tuo [!DNL Zoho CRM] connessione di base. Puoi usare questo nome per cercare il tuo [!DNL Zoho CRM] connessione di base. |
| `description` | Una descrizione facoltativa per le [!DNL Zoho CRM] connessione di base. |
| `auth.specName` | Tipo di autenticazione utilizzato per la connessione. |
| `auth.params.endpoint` | Il punto finale del [!DNL Zoho CRM] server a cui si sta effettuando la richiesta. |
| `auth.params.accountsUrl` | L’URL dell’account viene utilizzato per generare i token di accesso e aggiornamento. L&#39;URL deve essere specifico del dominio. |
| `auth.params.clientId` | L&#39;ID client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| `auth.params.clientSecret` | Il segreto client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| `auth.params.accessToken` | Il token di accesso autorizza l’accesso sicuro e temporaneo al tuo [!DNL Zoho CRM] conto. |
| `auth.params.refreshToken` | Un token di aggiornamento è un token utilizzato per generare un nuovo token di accesso, una volta scaduto il token di accesso. |
| `connectionSpec.id` | ID della specifica di connessione per [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Zoho] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Creare un flusso di dati per portare i dati CRM in Platform utilizzando [!DNL Flow Service] API](../../collect/crm.md)
