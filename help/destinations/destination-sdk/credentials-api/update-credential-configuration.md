---
description: Questa pagina esemplifica la chiamata API utilizzata per aggiornare una configurazione delle credenziali esistente tramite Adobe Experience Platform Destination SDK.
title: Aggiornare una configurazione delle credenziali
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 8%

---


# Aggiornare una configurazione delle credenziali

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Questa pagina esemplifica la richiesta API e il payload che puoi utilizzare per aggiornare una configurazione delle credenziali esistente utilizzando `/authoring/credentials` Endpoint API.

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

## Aggiornare una configurazione delle credenziali {#update}

È possibile aggiornare un [esistente](create-credential-configuration.md) configurazione delle credenziali effettuando una `PUT` richiesta al `/authoring/credentials` endpoint con il payload aggiornato.

Per ottenere una configurazione delle credenziali esistente e la relativa `{INSTANCE_ID}`, consulta l’articolo [recupero di una configurazione delle credenziali](retrieve-credential-configuration.md).

**Formato API**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione delle credenziali da aggiornare. Per ottenere una configurazione delle credenziali esistente e la relativa `{INSTANCE_ID}`, vedi [Recuperare una configurazione delle credenziali](retrieve-credential-configuration.md). |

Le richieste seguenti aggiornano le configurazioni delle credenziali esistenti, definite dai parametri forniti nel payload.

Seleziona ciascuna scheda qui sotto per visualizzare il payload corrispondente.

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
| `url` | Stringa | URL del provider di autorizzazioni |
| `username` | Stringa | Nome utente di accesso alla configurazione delle credenziali |
| `password` | Stringa | Password di accesso alla configurazione delle credenziali |

{style="table-layout:auto"}

+++

+++Risposta

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali aggiornata.

+++

>[!TAB Amazon S3]

**Aggiornare un [!DNL Amazon S3] configurazione delle credenziali**

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
| `accessId` | Stringa | [!DNL Amazon S3] ID accesso |
| `secretKey` | Stringa | [!DNL Amazon S3] chiave segreta |

{style="table-layout:auto"}

+++

+++Risposta

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali aggiornata.

+++

>[!TAB SSH]

**Aggiornare un [!DNL SSH] configurazione delle credenziali**

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
| `username` | Stringa | Nome utente di accesso alla configurazione delle credenziali |
| `sshKey` | Stringa | [!DNL SSH] chiave per [!DNL SFTP] con [!DNL SSH] autenticazione |

{style="table-layout:auto"}

+++

+++Risposta

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali aggiornata.

+++

>[!TAB Archiviazione Data Lake di Azure]

**Aggiornare un [!DNL Azure Data Lake Storage] configurazione delle credenziali**

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
| `url` | Stringa | URL del provider di autorizzazioni |
| `tenant` | Stringa | tenant di archiviazione Data Lake |
| `servicePrincipalId` | Stringa | [!DNL Azure Service Principal] ID per [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | Stringa | [!DNL Azure Service Principal Key] per [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++Risposta

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali aggiornata.

+++

>[!TAB Archiviazione BLOB di Azure]

**Aggiornare un [!DNL Azure Blob] configurazione delle credenziali**

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

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali aggiornata.

+++

>[!ENDTABS]

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come aggiornare una configurazione delle credenziali utilizzando `/authoring/credentials` Endpoint API. Leggi [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire dove si adatta questo passaggio al processo di configurazione della destinazione.
