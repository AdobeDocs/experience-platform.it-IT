---
keywords: Experience Platform;home;argomenti popolari;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Creare una connessione di base di Zoho CRM utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Zoho CRM utilizzando l’API del servizio Flusso.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# Creare un [!DNL Zoho CRM] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Zoho CRM] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Zoho CRM] utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Zoho CRM], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| `endpoint` | Endpoint del [!DNL Zoho CRM] server a cui si sta effettuando la richiesta. |
| `accountsUrl` | L’URL dell’account viene utilizzato per generare i token di accesso e di aggiornamento. L’URL deve essere specifico per il dominio. |
| `clientId` | L’ID client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| `clientSecret` | Il segreto client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| `accessToken` | Il token di accesso autorizza l’accesso protetto e temporaneo al tuo [!DNL Zoho CRM] account. |
| `refreshToken` | Un token di aggiornamento è un token utilizzato per generare un nuovo token di accesso, una volta scaduto il token di accesso. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Zoho CRM] è: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Per ulteriori informazioni su queste credenziali, consulta la documentazione su [[!DNL Zoho CRM] autenticazione](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Zoho CRM] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

>[!TIP]
>
>Il dominio dell’URL dell’account deve corrispondere alla posizione di dominio appropriata. Di seguito sono riportati i vari domini e gli URL dei relativi account:<ul><li>Stati Uniti: https://accounts.zoho.com</li><li>Australia: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>Cina: https://accounts.zoho.com.cn</li></ul>

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
| `name` | Il nome del tuo [!DNL Zoho CRM] connessione di base. È possibile utilizzare questo nome per cercare [!DNL Zoho CRM] connessione di base. |
| `description` | Una descrizione facoltativa per [!DNL Zoho CRM] connessione di base. |
| `auth.specName` | Tipo di autenticazione utilizzato per la connessione. |
| `auth.params.endpoint` | Endpoint del [!DNL Zoho CRM] server a cui si sta effettuando la richiesta. |
| `auth.params.accountsUrl` | L’URL dell’account viene utilizzato per generare i token di accesso e di aggiornamento. L’URL deve essere specifico per il dominio. |
| `auth.params.clientId` | L’ID client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| `auth.params.clientSecret` | Il segreto client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| `auth.params.accessToken` | Il token di accesso autorizza l’accesso protetto e temporaneo al tuo [!DNL Zoho CRM] account. |
| `auth.params.refreshToken` | Un token di aggiornamento è un token utilizzato per generare un nuovo token di accesso, una volta scaduto il token di accesso. |
| `connectionSpec.id` | ID della specifica di connessione per [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Zoho] connessione di base tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati CRM in Platform utilizzando [!DNL Flow Service] API](../../collect/crm.md)
