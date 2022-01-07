---
description: Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando l'endpoint API `/authoring/destinations/publish`.
title: Operazioni dell’endpoint API Publish Destinations
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 6dd8a94e46b9bee6d1407e7ec945a722d8d7ecdb
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 5%

---

# Operazioni API dell’endpoint Publish Destinations {#publish-destination}

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando `/authoring/destinations/publish` Endpoint API.

Dopo aver configurato e verificato la destinazione, puoi inviarla ad Adobe per la revisione e la pubblicazione.

Utilizza l’endpoint API delle destinazioni di pubblicazione per inviare una richiesta di pubblicazione quando:
* In qualità di partner di Destination SDK, vuoi rendere disponibile la tua destinazione di prodotto in tutte le organizzazioni Experience Platform affinché tutti i clienti di Experience Platform possano utilizzarla;
* Vuoi rendere la destinazione personalizzata disponibile nella tua organizzazione di Experience Platform, in tutte le sandbox.

## Guida introduttiva alle operazioni API di pubblicazione della destinazione {#get-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Invia una configurazione di destinazione per la pubblicazione {#create}

Puoi inviare una configurazione di destinazione per la pubblicazione effettuando una richiesta di POST al `/authoring/destinations/publish` punto finale.

**Formato API**


```http
POST /authoring/destinations/publish
```

**Richiesta**

La seguente richiesta invia una destinazione per la pubblicazione, tra le organizzazioni configurate dai parametri forniti nel payload. Il payload seguente include tutti i parametri accettati dal `/authoring/destinations/publish` punto finale.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "xyz@AdobeOrg",
      "lmn@AdobeOrg"
   ]
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `destinationId` | Stringa | ID di destinazione della configurazione di destinazione che si sta inviando per la pubblicazione. Ottieni l&#39;ID di destinazione di una configurazione di destinazione utilizzando [riferimento API per la configurazione della destinazione](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Stringa | `ALL` oppure `LIMITED`. Specifica se la destinazione deve essere visualizzata nel catalogo per tutti i clienti Experience Platform o solo per alcune organizzazioni. <br> **Nota**: Se utilizzi `LIMITED`, la destinazione verrà pubblicata solo per l’organizzazione di Experience Platform. Se desideri pubblicare la destinazione in un sottoinsieme di organizzazioni di Experience Platform a scopo di test dei clienti, contatta il supporto Adobe. |
| `allowedOrgs` | Stringa | Se utilizzi `"destinationAccess":"LIMITED"`, specifica le organizzazioni di Experience Platform per le quali la destinazione sarà disponibile. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli della richiesta di pubblicazione della destinazione.

## Elenca richieste di pubblicazione di destinazione {#retrieve-list}

Puoi recuperare un elenco di tutte le destinazioni inviate per la pubblicazione per la tua organizzazione IMS effettuando una richiesta di GET al `/authoring/destinations/publish` punto finale.

**Formato API**


```http
GET /authoring/destinations/publish
```

**Richiesta**

La seguente richiesta recupera l’elenco delle destinazioni inviate per la pubblicazione a cui hai accesso, in base alla configurazione dell’organizzazione IMS e della sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta seguente restituisce lo stato HTTP 200 con un elenco di destinazioni inviate per la pubblicazione a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Uno `configId` corrisponde alla richiesta di pubblicazione per una destinazione.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"1630617746"
      }
   ]
}
    
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `destinationId` | Stringa | ID di destinazione della configurazione di destinazione inviata per la pubblicazione. |
| `publishDetailsList.configId` | Stringa | ID univoco della richiesta di pubblicazione della destinazione per la destinazione inviata. |
| `publishDetailsList.allowedOrgs` | Stringa | Restituisce le organizzazioni di Experienci Platform per le quali la destinazione deve essere disponibile. |
| `publishDetailsList.status` | Stringa | Lo stato della richiesta di pubblicazione della destinazione. I valori possibili sono `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. |
| `publishDetailsList.publishedDate` | Stringa | Data in cui la destinazione è stata inviata per la pubblicazione, in epoch time. |

{style=&quot;table-layout:auto&quot;}

## Aggiornare una richiesta di pubblicazione di destinazione esistente {#update}

Puoi aggiornare le organizzazioni consentite in una richiesta di pubblicazione di destinazione esistente effettuando una richiesta di PUT al `/authoring/destinations/publish` e fornisce l&#39;ID della destinazione per la quale desideri aggiornare le organizzazioni consentite. Nel corpo della chiamata , fornisci le organizzazioni consentite aggiornate.

**Formato API**


```http
PUT /authoring/destinations/publish/{DESTINATION_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID della destinazione per la quale vuoi aggiornare la richiesta di pubblicazione. |

**Richiesta**

La richiesta seguente aggiorna una richiesta di pubblicazione di destinazione esistente, configurata dai parametri forniti nel payload. Nell’esempio di chiamata riportato di seguito, stiamo aggiornando le organizzazioni consentite.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "abc@AdobeOrg",
      "def@AdobeOrg"
   ]
}
```

## Ottenere lo stato di una specifica richiesta di pubblicazione di destinazione {#get}

Puoi recuperare informazioni dettagliate su una specifica richiesta di pubblicazione di destinazione effettuando una richiesta GET al `/authoring/destinations/publish` e fornisce l&#39;ID della destinazione per la quale desideri recuperare lo stato di pubblicazione.

**Formato API**


```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID della destinazione per la quale desideri recuperare lo stato di pubblicazione. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla richiesta di pubblicazione della destinazione specificata.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"string"
      }
   ]
}
```

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come inviare una richiesta di pubblicazione per la tua destinazione. Il team Adobe Experience Platform esaminerà la tua richiesta di pubblicazione e ti risponderà entro cinque giorni lavorativi.
