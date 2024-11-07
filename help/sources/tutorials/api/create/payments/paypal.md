---
keywords: Experience Platform;home;argomenti popolari;connettore PayPal;paypal;Paypal
solution: Experience Platform
title: Creare una connessione di base PayPal utilizzando l'API del servizio di flusso
type: Tutorial
description: Scopri come collegare PayPal a Adobe Experience Platform utilizzando l’API del servizio Flow.
exl-id: 5e6ca7b4-5e2f-4706-a339-ac159e2e0938
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 5%

---

# Creare una connessione di base [!DNL PayPal] utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>L&#39;origine [!DNL PayPal] diventerà obsoleta alla fine di maggio 2025. È possibile utilizzare [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) al posto dell&#39;origine [!DNL PayPal].

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL PayPal] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL PayPal] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL PayPal], è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | URL dell&#39;istanza [!DNL PayPal]. (impostazione predefinita: api.sandbox.paypal.com). |
| `clientId` | L&#39;ID client associato all&#39;applicazione [!DNL PayPal]. |
| `clientSecret` | Il segreto client associato all&#39;applicazione [!DNL PayPal]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL PayPal]: `221c7626-58f6-4eec-8ee2-042b0226f03b` |

Per ulteriori informazioni su come iniziare, consulta [questo documento PayPal](https://developer.paypal.com/docs/api/overview/#get-credentials).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL PayPal] come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL PayPal]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Paypal connection",
        "description": "Paypal connection",
        "auth": {
        "specName": "Client-Id-Secret Based Authentication",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.host` | URL dell&#39;istanza [!DNL PayPal]. |
| `auth.params.clientId` | L&#39;ID client associato all&#39;istanza [!DNL PayPal]. |
| `auth.params.clientSecret` | Il segreto client associato all&#39;istanza [!DNL PayPal]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL PayPal]: `221c7626-58f6-4eec-8ee2-042b0226f03b`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso l&#39;identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell’esercitazione successiva.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL PayPal] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati dei pagamenti a Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/payments.md)
