---
description: Questa pagina esemplifica la chiamata API utilizzata per creare un Adobe Experience Platform Destination SDK di configurazione delle credenziali.
title: Creare una configurazione delle credenziali
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 8%

---


# Creare una configurazione delle credenziali

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Questa pagina esemplifica la richiesta API e il payload che puoi utilizzare per creare una configurazione delle credenziali utilizzando `/authoring/credentials` Endpoint API.

## Quando utilizzare il `/credentials` Endpoint API {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, ***non*** devono utilizzare `/credentials` Endpoint API. È invece possibile configurare le informazioni di autenticazione per la destinazione tramite la `customerAuthenticationConfigurations` dei parametri `/destinations` punto finale.
> 
>Leggi [Configurazione dell’autenticazione cliente](../functionality/destination-configuration/customer-authentication.md) per informazioni dettagliate sui tipi di autenticazione supportati.

Utilizza questo endpoint API per creare una configurazione delle credenziali solo se è presente un sistema di autenticazione globale tra Adobe e la piattaforma di destinazione e [!DNL Platform] il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, devi creare una configurazione delle credenziali utilizzando `/credentials` Endpoint API.

Quando utilizzi un sistema di autenticazione globale, devi impostare `"authenticationRule":"PLATFORM_AUTHENTICATION"` in [consegna a destinazione](../functionality/destination-configuration/destination-delivery.md) configurazione, quando [creazione di una nuova configurazione di destinazione](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API con le credenziali {#get-started}

Prima di continuare, controlla la [guida introduttiva](../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Creare una configurazione delle credenziali {#create}

Puoi creare una nuova configurazione delle credenziali creando una `POST` richiesta al `/authoring/credentials` punto finale.

**Formato API**

```http
POST /authoring/credentials
```

Le richieste seguenti creano nuove configurazioni di credenziali, definite dai parametri forniti nel payload.

Seleziona ciascuna scheda qui sotto per visualizzare il payload corrispondente.

>[!BEGINTABS]

>[!TAB Base]

**Creare una configurazione delle credenziali di base**

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parametro | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `url` | Stringa | URL del provider di autorizzazioni |
| `username` | Stringa | Nome utente di accesso alla configurazione delle credenziali |
| `password` | Stringa | Password di accesso alla configurazione delle credenziali |

{style="table-layout:auto"}

+++

+++Risposta

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali appena create.

+++

>[!TAB Amazon S3]

**Crea un [!DNL Amazon S3] configurazione delle credenziali**

+++**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| Parametro | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `accessId` | Stringa | [!DNL Amazon S3] ID accesso |
| `secretKey` | Stringa | [!DNL Amazon S3] chiave segreta |

{style="table-layout:auto"}

+++

+++Risposta

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali appena create.

+++

>[!TAB SSH]

**Creare una configurazione delle credenziali SSH**

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| Parametro | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `username` | Stringa | Nome utente di accesso alla configurazione delle credenziali |
| `sshKey` | Stringa | Chiave SSH per SFTP con autenticazione SSH |

{style="table-layout:auto"}

+++

+++Risposta

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali appena create.

+++

>[!TAB Archiviazione Data Lake di Azure]

**Crea un [!DNL Azure Data Lake Storage] configurazione delle credenziali**

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| Parametro | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `url` | Stringa | URL del provider di autorizzazioni |
| `tenant` | Stringa | tenant di archiviazione Data Lake |
| `servicePrincipalId` | Stringa | ID principale del servizio Azure per Azure Data Lake Storage |
| `servicePrincipalKey` | Stringa | Chiave principale del servizio Azure per Azure Data Lake Storage |

{style="table-layout:auto"}

+++

+++Risposta

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali appena create.

+++

>[!TAB Archiviazione BLOB di Azure]

**Crea un [!DNL Azure Blob Storage] configurazione delle credenziali**

+++Richiesta

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| Parametro | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `connectionString` | Stringa | [!DNL Azure Blob Storage] stringa di connessione |

{style="table-layout:auto"}

+++

+++Risposta

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali appena create.

+++

>[!ENDTABS]

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora si sa quando utilizzare l&#39;endpoint delle credenziali e come impostare una configurazione delle credenziali utilizzando `/authoring/credentials` Lettura endpoint API [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire dove si adatta questo passaggio al processo di configurazione della destinazione.
