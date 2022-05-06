---
description: Questa pagina descrive tutte le operazioni API che è possibile eseguire utilizzando l'endpoint API `/authoring/credentials`.
title: Operazioni API per l’endpoint delle credenziali
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 6%

---

# Operazioni API per l’endpoint delle credenziali {#credentials}

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando `/authoring/credentials` Endpoint API.

Per una descrizione delle funzionalità supportate da questo endpoint, leggere:

* [Configurazione della destinazione di streaming](destination-configuration.md) per la funzionalità che puoi configurare per le destinazioni di streaming.
* [Configurazione della destinazione basata su file](file-based-destination-configuration.md) per la funzionalità che puoi configurare per le destinazioni basate su file.

## Quando utilizzare il `/credentials` Endpoint API {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, *non* devono utilizzare `/credentials` Endpoint API. È invece possibile configurare le informazioni di autenticazione per la destinazione tramite la `customerAuthenticationConfigurations` dei parametri `/destinations` punto finale. Leggi [Configurazione dell’autenticazione](./authentication-configuration.md#when-to-use) per ulteriori informazioni.

Utilizza questo endpoint API e seleziona `PLATFORM_AUTHENTICATION` in [configurazione di destinazione](./destination-configuration.md#destination-delivery) se esiste un sistema di autenticazione globale tra l’Adobe e la destinazione e [!DNL Platform] il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando `/credentials` Endpoint API.

## Guida introduttiva alle operazioni API di configurazione delle credenziali {#get-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Creare una configurazione delle credenziali {#create}

È possibile creare una nuova configurazione delle credenziali effettuando una richiesta di POST al `/authoring/credentials` punto finale.

**Formato API**

```http
POST /authoring/credentials
```

**Richiesta**

La richiesta seguente crea una nuova configurazione di credenziali, configurata dai parametri forniti nel payload. Il payload seguente include tutti i parametri accettati dal `/authoring/credentials` punto finale. Non è necessario aggiungere tutti i parametri alla chiamata e il modello è personalizzabile, in base ai requisiti API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "oauth2UserAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "username":"string",
      "password":"string",
      "header":"string"
   },
   "oauth2ClientAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "header":"string",
      "developerToken":"string"
   },
   "oauth2AccessTokenAuthentication":{
      "accessToken":"string",
      "expiration":"string",
      "username":"string",
      "userId":"string",
      "url":"string",
      "header":"string"
   },
   "oauth2RefreshTokenAuthentication":{
      "refreshToken":"string",
      "expiration":"string",
      "clientId":"string",
      "clientSecret":"string",
      "url":"string",
      "header":"string"
   },
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   },
   "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   },
   "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   },
   "azureConnectionStringAuthentication":{
      "connectionString":"string"
   },
   "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parametro | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `username` | Stringa | Nome utente di accesso alla configurazione delle credenziali |
| `password` | Stringa | Password di accesso alla configurazione delle credenziali |
| `url` | Stringa | URL del provider di autorizzazioni |
| `clientId` | Stringa | ID client delle credenziali client/applicazione |
| `clientSecret` | Stringa | Segreto client delle credenziali client/applicazione |
| `accessToken` | Stringa | Token di accesso fornito dal provider di autorizzazioni |
| `expiration` | Stringa | Time-to-live per il token di accesso |
| `refreshToken` | Stringa | Token di aggiornamento fornito dal provider di autorizzazioni |
| `header` | Stringa | Qualsiasi intestazione necessaria per l&#39;autorizzazione |
| `accessId` | Stringa | ID accesso Amazon S3 |
| `secretKey` | Stringa | Chiave segreta Amazon S3 |
| `sshKey` | Stringa | Chiave SSH per SFTP con autenticazione SSH |
| `tenant` | Stringa | tenant di archiviazione Data Lake |
| `servicePrincipalId` | Stringa | ID principale del servizio Azure per Azure Data Lake Storage |
| `servicePrincipalKey` | Stringa | Chiave principale del servizio Azure per Azure Data Lake Storage |
| `connectionString` | Stringa | Stringa di connessione archiviazione BLOB di Azure |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali appena create.

## Configurazioni delle credenziali elenco {#retrieve-list}

Puoi recuperare un elenco di tutte le configurazioni di credenziali per la tua organizzazione IMS effettuando una richiesta di GET al `/authoring/credentials` punto finale.

**Formato API**


```http
GET /authoring/credentials
```

**Richiesta**

La seguente richiesta recupererà l’elenco delle configurazioni di credenziali a cui hai accesso, in base alla configurazione dell’organizzazione IMS e della sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta seguente restituisce lo stato HTTP 200 con un elenco di configurazioni di credenziali a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Uno `instanceId` corrisponde al modello per una configurazione di credenziali. La risposta viene troncata per brevità.

```json
{
   "items":[
      {
         "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
         "createdDate":"2021-06-07T06:41:48.641943Z",
         "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
         "type":"OAUTH2_USER_CREDENTIAL",
         "name":"yourdestination",
         "oauth2UserAuthentication":{
            "url":"ABCD",
            "clientId":"ABCDEFGHIJKL",
            "clientSecret":"clientsecret",
            "username":"username",
            "password":"password",
            "header":"header"
         }
      }
   ]
}
    
```

## Aggiornare una configurazione di credenziali esistente {#update}

È possibile aggiornare una configurazione di credenziali esistente effettuando una richiesta di PUT al `/authoring/credentials` e fornisce l&#39;ID istanza della configurazione delle credenziali che desideri aggiornare. Nel corpo della chiamata , fornisci la configurazione delle credenziali aggiornate.

**Formato API**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione delle credenziali da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna una configurazione di credenziali esistente, configurata dai parametri forniti nel payload.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```

## Recupera una configurazione di credenziali specifica {#get}

È possibile recuperare informazioni dettagliate su una configurazione di credenziali specifica effettuando una richiesta di GET al `/authoring/credentials` e fornisce l&#39;ID istanza della configurazione delle credenziali che desideri aggiornare.

**Formato API**

```http
GET /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione delle credenziali da recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla configurazione delle credenziali specificate.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```

## Eliminare una configurazione di credenziali specifica {#delete}

È possibile eliminare la configurazione delle credenziali specificata effettuando una richiesta di DELETE al `/authoring/credentials` e fornendo l&#39;ID della configurazione delle credenziali che desideri eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | La `id` della configurazione delle credenziali da eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora si sa quando utilizzare l&#39;endpoint delle credenziali e come impostare una configurazione delle credenziali utilizzando `/authoring/credentials` endpoint API o `/authoring/destinations` punto finale. Leggi [come utilizzare Destination SDK per configurare la destinazione](./configure-destination-instructions.md) per capire dove si adatta questo passaggio al processo di configurazione della destinazione.
