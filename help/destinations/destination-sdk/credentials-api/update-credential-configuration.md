---
description: Questa pagina esemplifica la chiamata API utilizzata per aggiornare una configurazione di credenziali esistente tramite il Adobe Experience Platform Destination SDK.
title: Aggiornare una configurazione delle credenziali
exl-id: ebff370c-9189-48df-871f-ed0e1cd535c8
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 5%

---

# Aggiornare una configurazione delle credenziali

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Questa pagina esemplifica la richiesta API e il payload che è possibile utilizzare per aggiornare una configurazione di credenziali esistente, utilizzando l&#39;endpoint API `/authoring/credentials`.

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

## Aggiornare una configurazione delle credenziali {#update}

È possibile aggiornare una configurazione delle credenziali [existing](create-credential-configuration.md) effettuando una richiesta `PUT` all&#39;endpoint `/authoring/credentials` con il payload aggiornato.

Per ottenere una configurazione delle credenziali esistente e i corrispondenti `{INSTANCE_ID}`, vedere l&#39;articolo relativo al [recupero di una configurazione delle credenziali](retrieve-credential-configuration.md).

**Formato API**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione delle credenziali che si desidera aggiornare. Per ottenere una configurazione delle credenziali esistente e i relativi `{INSTANCE_ID}`, vedere [Recuperare una configurazione delle credenziali](retrieve-credential-configuration.md). |

Le seguenti richieste aggiornano le configurazioni delle credenziali esistenti, definite dai parametri forniti nel payload.

Seleziona ciascuna scheda di seguito per visualizzare il payload corrispondente.

>[!BEGINTABS]

>[!TAB Base]

**Aggiornare una configurazione delle credenziali di base**

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali aggiornata.

+++

>[!TAB Amazon S3]

**Aggiorna una configurazione delle credenziali [!DNL Amazon S3]**

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali aggiornata.

+++

>[!TAB SSH]

**Aggiorna una configurazione delle credenziali [!DNL SSH]**

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `sshKey` | Stringa | Chiave [!DNL SSH] per [!DNL SFTP] con autenticazione [!DNL SSH] |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali aggiornata.

+++

>[!TAB Archiviazione Azure Data Lake]

**Aggiorna una configurazione delle credenziali [!DNL Azure Data Lake Storage]**

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `servicePrincipalId` | Stringa | ID [!DNL Azure Service Principal] per [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | Stringa | [!DNL Azure Service Principal Key] per [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali aggiornata.

+++

>[!TAB Archiviazione BLOB di Azure]

**Aggiorna una configurazione delle credenziali [!DNL Azure Blob]**

+++Richiesta

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali aggiornata.

+++

>[!ENDTABS]

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come aggiornare una configurazione di credenziali utilizzando l&#39;endpoint API `/authoring/credentials`. Leggi [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della destinazione.
