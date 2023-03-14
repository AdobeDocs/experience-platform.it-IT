---
description: Questa pagina descrive tutte le operazioni API che è possibile eseguire utilizzando l’endpoint API "/authoring/credentials".
title: Operazioni API per endpoint credenziali
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 6%

---

# Operazioni API per endpoint credenziali {#credentials}

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Questa pagina elenca e descrive tutte le operazioni API che è possibile eseguire utilizzando `/authoring/credentials` Endpoint API

Per una descrizione delle funzionalità supportate da questo endpoint, leggi:

* [Configurazione della destinazione di streaming](destination-configuration.md) per la funzionalità che puoi configurare per le destinazioni di streaming.
* [Configurazione di destinazione basata su file](file-based-destination-configuration.md) per la funzionalità che puoi configurare per le destinazioni basate su file.

## Quando utilizzare il `/credentials` Endpoint API {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, *non* devono utilizzare `/credentials` Endpoint API È invece possibile configurare le informazioni di autenticazione per la destinazione tramite `customerAuthenticationConfigurations` parametri di `/destinations` endpoint. Letto [Configurazione dell’autenticazione](./authentication-configuration.md#when-to-use) per ulteriori informazioni.

Utilizza questo endpoint API e seleziona `PLATFORM_AUTHENTICATION` nel [configurazione di destinazione](./destination-configuration.md#destination-delivery) se è presente un sistema di autenticazione globale tra Adobe e la tua destinazione e il [!DNL Platform] Il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, è necessario creare un oggetto credenziali utilizzando `/credentials` Endpoint API

## Guida introduttiva alle operazioni API di configurazione delle credenziali {#get-started}

Prima di continuare, controlla [guida introduttiva](./getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Creare una configurazione di credenziali {#create}

Per creare una nuova configurazione delle credenziali, devi effettuare una richiesta POST al `/authoring/credentials` endpoint.

**Formato API**

```http
POST /authoring/credentials
```

**Richiesta**

La richiesta seguente crea una nuova configurazione delle credenziali, configurata dai parametri forniti nel payload. Il payload riportato di seguito include tutti i parametri accettati dal `/authoring/credentials` endpoint. Tieni presente che non è necessario aggiungere tutti i parametri alla chiamata e che il modello è personalizzabile, in base ai requisiti API.

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
| `username` | Stringa | Nome utente di accesso alla configurazione credenziali |
| `password` | Stringa | Password di accesso alla configurazione delle credenziali |
| `url` | Stringa | URL del provider di autorizzazione |
| `clientId` | Stringa | ID client delle credenziali client/applicazione |
| `clientSecret` | Stringa | Segreto client delle credenziali client/applicazione |
| `accessToken` | Stringa | Token di accesso fornito dal provider di autorizzazioni |
| `expiration` | Stringa | Time-to-live del token di accesso |
| `refreshToken` | Stringa | Aggiorna token fornito dal provider di autorizzazioni |
| `header` | Stringa | Qualsiasi intestazione necessaria per l’autorizzazione |
| `accessId` | Stringa | ID accesso Amazon S3 |
| `secretKey` | Stringa | Chiave segreta Amazon S3 |
| `sshKey` | Stringa | Chiave SSH per SFTP con autenticazione SSH |
| `tenant` | Stringa | Tenant archiviazione Azure Data Lake |
| `servicePrincipalId` | Stringa | ID entità servizio Azure per l’archiviazione del data lake di Azure |
| `servicePrincipalKey` | Stringa | Chiave principale del servizio Azure per l’archiviazione del data lake di Azure |
| `connectionString` | Stringa | Stringa di connessione archiviazione BLOB di Azure |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della nuova configurazione delle credenziali creata.

## Elencare le configurazioni delle credenziali {#retrieve-list}

Per recuperare un elenco di tutte le configurazioni di credenziali per l’organizzazione IMS, invia una richiesta GET al `/authoring/credentials` endpoint.

**Formato API**


```http
GET /authoring/credentials
```

**Richiesta**

La richiesta seguente recupererà l’elenco delle configurazioni di credenziali a cui hai accesso, in base alla configurazione di sandbox e organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La seguente risposta restituisce lo stato HTTP 200 con un elenco di configurazioni di credenziali a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Uno `instanceId` corrisponde al modello per una configurazione di credenziali. La risposta viene troncata per brevità.

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

Per aggiornare una configurazione di credenziali esistente, devi effettuare una richiesta PUT al `/authoring/credentials` e fornendo l’ID istanza della configurazione di credenziali che desideri aggiornare. Nel corpo della chiamata, fornisci la configurazione delle credenziali aggiornata.

**Formato API**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione delle credenziali che desideri aggiornare. |

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

## Recuperare una configurazione di credenziali specifica {#get}

Per recuperare informazioni dettagliate su una configurazione di credenziali specifica, effettua una richiesta GET al `/authoring/credentials` e fornendo l’ID istanza della configurazione di credenziali che desideri aggiornare.

**Formato API**

```http
GET /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione di credenziali che desideri recuperare. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sulla configurazione delle credenziali specificata.

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

## Elimina una configurazione di credenziali specifica {#delete}

È possibile eliminare la configurazione delle credenziali specificata effettuando una richiesta DELETE al `/authoring/credentials` e fornendo l’ID della configurazione di credenziali che desideri eliminare nel percorso della richiesta.

**Formato API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | Il `id` della configurazione delle credenziali che desideri eliminare. |

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai quando utilizzare l’endpoint delle credenziali e come impostare una configurazione delle credenziali utilizzando `/authoring/credentials` Endpoint API o `/authoring/destinations` endpoint. Letto [come utilizzare Destination SDK per configurare la destinazione](./configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della destinazione.
