---
keywords: Experience Platform;home;argomenti popolari;oracle;
title: (Beta) Creare una connessione di base Responsys Oracle utilizzando l’API del servizio di flusso
description: Scopri come collegare Adobe Experience Platform a Oracle Responsys utilizzando l’API del servizio di flusso.
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# (Beta) Crea un [!DNL Oracle Responsys] connessione di base utilizzando [!DNL Flow Service] API

>[!NOTE]
>
>La [!DNL Oracle Responsys] la sorgente è in versione beta. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo dei connettori con etichetta beta.

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Oracle Responsys] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Platform:

* [Origini](../../../../home.md): Platform consente l’acquisizione di dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Oracle Responsys] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Oracle Responsys], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| `endpoint` | L’URL dell’endpoint di autenticazione REST del tuo [!DNL Oracle Responsys] istanza. |
| `clientId` | L&#39;ID cliente del tuo [!DNL Oracle Responsys] istanza. |
| `clientSecret` | Il segreto cliente del tuo [!DNL Oracle Responsys] istanza. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. Il valore dell&#39;ID della specifica di connessione del [!DNL Oracle Responsys] la sorgente è fissa come: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

Per ulteriori informazioni sulle credenziali di autenticazione per [!DNL Oracle Responsys], vedi [[!DNL Oracle Responsys] guida all’autenticazione](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Oracle Responsys] credenziali di autenticazione come parte dei parametri della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Oracle Responsys]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `name` | Il nome del tuo [!DNL Oracle Responsys] connessione di base. È consigliabile fornire un nome descrittivo in quanto è possibile utilizzare questo valore per cercare la connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire informazioni aggiuntive sulla connessione di base. |
| `auth.specName` | Tipo di autenticazione utilizzato per la connessione. |
| `auth.params.endpoint` | L’URL dell’endpoint di autenticazione REST del tuo [!DNL Oracle Responsys] server. |
| `auth.params.clientId` | L&#39;ID cliente del tuo [!DNL Oracle Responsys] istanza. |
| `auth.params.clientSecret` | Il segreto cliente del tuo [!DNL Oracle Responsys] istanza. |
| `connectionSpec.id` | Il valore dell&#39;ID della specifica di connessione del [!DNL Oracle Responsys] la sorgente è fissa come: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Oracle Responsys] connessione di base utilizzando [!DNL Flow Service] API. Puoi usare questo ID di connessione di base nelle seguenti esercitazioni:

* [Esplorare la struttura e il contenuto delle tabelle di dati utilizzando [!DNL Flow Service] API](../../explore/tabular.md)
* [Crea un flusso di dati per trasferire i dati di automazione del marketing a Platform utilizzando [!DNL Flow Service] API](../../collect/marketing-automation.md)
