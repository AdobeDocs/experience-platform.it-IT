---
description: Questa pagina descrive tutte le operazioni API che è possibile eseguire utilizzando l'endpoint API `/authoring/credentials`.
title: Operazioni API per l’endpoint delle credenziali
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 5%

---

# Operazioni API per l’endpoint delle credenziali {#credentials}

>[!IMPORTANT]
>
>**Endpoint** API:  `platform.adobe.io/data/core/activation/authoring/credentials`

In questa pagina sono elencate e descritte tutte le operazioni API che puoi eseguire utilizzando l’endpoint API `/authoring/credentials`.

## Quando utilizzare l’endpoint API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, *non* non è necessario utilizzare l’endpoint API `/credentials`. Puoi invece configurare le informazioni di autenticazione per la destinazione tramite i parametri `customerAuthenticationConfigurations` dell’ endpoint `/destinations` . Leggi [Configurazione credenziali](./credentials-configuration.md) per ulteriori informazioni.

Utilizza questo endpoint API e seleziona `PLATFORM_AUTHENTICATION` nella [configurazione di destinazione](./destination-configuration.md#destination-delivery) se è presente un sistema di autenticazione globale tra Adobe e la destinazione e il cliente [!DNL Platform] non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando l&#39;endpoint API `/credentials`.

<!--

Commenting out the example configurations

## Example configurations

**Example configuration for a Basic authentication credential configuration with username and password**

```json
{
  "type": "BASIC",
  "name": "YOUR_DESTINATION_NAME",
  "basicAuthentication": {
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "password": "YOUR_DESTINATION_SERVER_PASSWORD"
  }
}

```

**Example configuration for an OAuth2 credential configuration**

```json

{
  "oauth2AccessTokenAuthentication": {
    "accessToken": "YOUR_DESTINATION_SERVER_ACCESS_TOKEN",
    "expiration": "YOUR_TOKEN_TIME_TO_LIVE",
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "userId": "YOUR_DESTINATION_USER_ID",
    "url": "AUTHORIZATION_PROVIDER_URL",
    "header": "YOUR_AUTHORIZATION_HEADER"
  }
}

```

The sections below list out the necessary parameters for each authentication type. Let us know which authentication type your server uses and provide us with the relevant information for your server type.

## Basic authentication

|Parameter | Type | Description|
|---------|----------|------|
|`username` | String | credentials configuration login username |
|`password` | String | credentials configuration login password |



// commenting out this part as these types of authentication methods are not supported in phase one

### S3 authentication

|Parameter | Type | Description|
|---------|----------|------|
|accessId | String | credentials configuration S3 credential Access key ID |
|secretKey | String | credentials configuration S3 credential Secret key |

### SSH 

|Parameter | Type | Description|
|---------|----------|------|
|username | String | credentials configuration SSH username |
|SSHKey | String | credentials configuration SSH key |



## OAuth1

|Parameter | Type | Description|
|---------|----------|------|
|`apiKey` | String | A value used by the Destinations Service to identify itself to the Service Provider. |
|`apiSecret` | String | Secret used by the Destinations Service to establish ownership of the API key to the Service Provider. |
|`acccessToken` | String | A value used by the Destinations Service to gain access to the Protected Resources on behalf of the User |
|`tokenSecret` | String | A secret used by the Destinations Service to establish ownership of an access token. |

## OAuth2 user credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username` | String | The user's username to log on to your platform. |
|`password` | String | The user's password to log on to your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 client credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username`| String | URL of authorization provider |
|`password` | String | Any header required for authorization |

## OAuth2 access token

|Parameter | Type | Description|
|---------|----------|------|
|`accessToken` | String | Access token provided by the authorization provider |
|`expiration` | String | The time-to-live for the access token |
|`username` | String | The user's username to log on to your platform. |
|`userId` | String | The user's ID with your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 refresh token

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`refreshToken` | String | Refresh token provided by the authorization provider |
|`url` | String | URL of authorization provider |
|`expiration` | String | The time-to-live for the refresh token |
|`header` | String | Any header required for authorization |

-->

## Guida introduttiva alle operazioni API di configurazione delle credenziali {#get-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Creare una configurazione delle credenziali {#create}

È possibile creare una nuova configurazione delle credenziali effettuando una richiesta di POST all&#39;endpoint `/authoring/credentials`.

**Formato API**


```http
POST /authoring/credentials
```

**Richiesta**

La richiesta seguente crea una nuova configurazione di credenziali, configurata dai parametri forniti nel payload. Il payload seguente include tutti i parametri accettati dall’endpoint `/authoring/credentials`. Non è necessario aggiungere tutti i parametri alla chiamata e il modello è personalizzabile, in base ai requisiti API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
   }
}
```

| Parametro | Tipo | Descrizione |
| -------- | ----------- | ----------- |
| `username` | Stringa | nome utente di accesso alla configurazione delle credenziali |
| `password` | Stringa | password di accesso alla configurazione delle credenziali |
| `url` | Stringa | URL del provider di autorizzazioni |
| `clientId` | Stringa | ID client delle credenziali client/applicazione |
| `clientSecret` | Stringa | Segreto client delle credenziali client/applicazione |
| `accessToken` | Stringa | Token di accesso fornito dal provider di autorizzazioni |
| `expiration` | Stringa | Time-to-live per il token di accesso |
| `refreshToken` | Stringa | Token di aggiornamento fornito dal provider di autorizzazioni |
| `header` | Stringa | Qualsiasi intestazione necessaria per l&#39;autorizzazione |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali appena create.

## Configurazioni delle credenziali elenco {#retrieve-list}

È possibile recuperare un elenco di tutte le configurazioni di credenziali per l’organizzazione IMS effettuando una richiesta di GET all’endpoint `/authoring/credentials`.

**Formato API**


```http
GET /authoring/credentials
```

**Richiesta**

La seguente richiesta recupererà l’elenco delle configurazioni di credenziali a cui hai accesso, in base alla configurazione dell’organizzazione IMS e della sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta seguente restituisce lo stato HTTP 200 con un elenco di configurazioni di credenziali a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Una `instanceId` corrisponde al modello per una configurazione di credenziali. La risposta viene troncata per brevità.

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

È possibile aggiornare una configurazione di credenziali esistente effettuando una richiesta di PUT all&#39;endpoint `/authoring/credentials` e fornendo l&#39;ID di istanza della configurazione di credenziali che si desidera aggiornare. Nel corpo della chiamata , fornisci la configurazione delle credenziali aggiornate.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

È possibile recuperare informazioni dettagliate su una configurazione di credenziali specifica effettuando una richiesta di GET all&#39;endpoint `/authoring/credentials` e fornendo l&#39;ID di istanza della configurazione di credenziali che si desidera aggiornare.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

È possibile eliminare la configurazione delle credenziali specificata effettuando una richiesta DELETE all&#39;endpoint `/authoring/credentials` e fornendo l&#39;ID della configurazione delle credenziali che si desidera eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | La `id` della configurazione delle credenziali che desideri eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

## Gestione degli errori API

Gli endpoint API SDK di destinazione seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) e [richiedi errori di intestazione](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai quando utilizzare l’endpoint delle credenziali e come impostare una configurazione delle credenziali utilizzando l’ `/authoring/credentials` endpoint API o l’ `/authoring/destinations` endpoint. Leggi [come utilizzare l&#39;SDK di destinazione per configurare la destinazione](./configure-destination-instructions.md) per capire dove si adatta questo passaggio al processo di configurazione della destinazione.
