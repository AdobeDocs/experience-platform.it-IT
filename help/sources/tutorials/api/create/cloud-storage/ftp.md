---
keywords: Experience Platform;home;argomenti popolari; protocollo di trasferimento dei file; protocollo di trasferimento file
solution: Experience Platform
title: Creare una connessione di base FTP utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un server FTP (File Transfer Protocol) utilizzando l’API del servizio di flusso.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---

# Creare una connessione di base FTP utilizzando [!DNL Flow Service] API

>[!NOTE]
>
>Il connettore FTP è in versione beta. Le funzioni e la documentazione sono soggette a modifiche. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo dei connettori con etichetta beta.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL FTP] (File Transfer Protocol) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a un [!DNL FTP] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi a [!DNL FTP], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al tuo [!DNL FTP] server. |
| `username` | Il nome utente con accesso al tuo [!DNL FTP] server. |
| `password` | La password [!DNL FTP] server. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL FTP] è: `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL FTP] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL FTP]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.host` | Il nome host del server FTP. |
| `auth.params.username` | Nome utente associato al server FTP. |
| `auth.params.password` | Password associata al server FTP. |
| `connectionSpec.id` | ID delle specifiche di connessione del server FTP: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione creata. Questo ID è necessario per esplorare il server FTP nella prossima esercitazione.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione FTP utilizzando [!DNL Flow Service] e hanno ottenuto il valore ID univoco della connessione. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l’API del servizio di flusso](../../explore/cloud-storage.md).
