---
description: Questa pagina esemplifica la chiamata API utilizzata per creare un Adobe Experience Platform Destination SDK di configurazione delle credenziali.
title: Creare una configurazione delle credenziali
exl-id: 9844c9c5-d2dc-4d4b-ae93-759bf23b87fa
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 6%

---

# Creare una configurazione delle credenziali

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per creare una configurazione delle credenziali utilizzando l&#39;endpoint API `/authoring/credentials`.

## Quando utilizzare l&#39;endpoint API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, ***non*** deve utilizzare l&#39;endpoint API `/credentials`. È invece possibile configurare le informazioni di autenticazione per la destinazione tramite i parametri `customerAuthenticationConfigurations` dell&#39;endpoint `/destinations`.
> 
>Leggi [Configurazione autenticazione cliente](../functionality/destination-configuration/customer-authentication.md) per informazioni dettagliate sui tipi di autenticazione supportati.

Utilizzare questo endpoint API per creare una configurazione di credenziali solo se è presente un sistema di autenticazione globale tra Adobe e la piattaforma di destinazione e il cliente [!DNL Platform] non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, è necessario creare una configurazione delle credenziali utilizzando l&#39;endpoint API `/credentials`.

Quando si utilizza un sistema di autenticazione globale, è necessario impostare `"authenticationRule":"PLATFORM_AUTHENTICATION"` nella configurazione [consegna di destinazione](../functionality/destination-configuration/destination-delivery.md), durante la [creazione di una nuova configurazione di destinazione](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API per le credenziali {#get-started}

Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Creare una configurazione di credenziali {#create}

È possibile creare una nuova configurazione delle credenziali effettuando una richiesta `POST` all&#39;endpoint `/authoring/credentials`.

**Formato API**

```http
POST /authoring/credentials
```

Le seguenti richieste creano nuove configurazioni di credenziali, definite dai parametri forniti nel payload.

Seleziona ciascuna scheda di seguito per visualizzare il payload corrispondente.

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
| `url` | Stringa | URL del provider di autorizzazione |
| `username` | Stringa | Nome utente di accesso alla configurazione credenziali |
| `password` | Stringa | Password di accesso alla configurazione delle credenziali |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della nuova configurazione delle credenziali creata.

+++

>[!TAB Amazon S3]

**Crea una configurazione delle credenziali [!DNL Amazon S3]**

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
| `accessId` | Stringa | ID di accesso [!DNL Amazon S3] |
| `secretKey` | Stringa | Chiave segreta [!DNL Amazon S3] |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della nuova configurazione delle credenziali creata.

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
| `username` | Stringa | Nome utente di accesso alla configurazione credenziali |
| `sshKey` | Stringa | Chiave SSH per SFTP con autenticazione SSH |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della nuova configurazione delle credenziali creata.

+++

>[!TAB Archiviazione Azure Data Lake]

**Crea una configurazione delle credenziali [!DNL Azure Data Lake Storage]**

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
| `url` | Stringa | URL del provider di autorizzazione |
| `tenant` | Stringa | Tenant archiviazione Azure Data Lake |
| `servicePrincipalId` | Stringa | ID entità servizio Azure per l’archiviazione del data lake di Azure |
| `servicePrincipalKey` | Stringa | Chiave principale del servizio Azure per l’archiviazione del data lake di Azure |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della nuova configurazione delle credenziali creata.

+++

>[!TAB Archiviazione BLOB di Azure]

**Crea una configurazione delle credenziali [!DNL Azure Blob Storage]**

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della nuova configurazione delle credenziali creata.

+++

>[!ENDTABS]

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, sai quando utilizzare l&#39;endpoint delle credenziali e come impostare una configurazione delle credenziali utilizzando l&#39;endpoint API `/authoring/credentials`. Leggi [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della destinazione.
