---
description: Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando l'endpoint API `/authoring/destinations/publish`.
title: Operazioni dell’endpoint API Publish Destinations
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 702a5b7154724faa9f5e6847b462e0ae90475571
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 5%

---

# Operazioni API dell’endpoint Publish Destinations {#publish-destination}

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando `/authoring/destinations/publish` Endpoint API.

Dopo aver configurato e verificato la destinazione, puoi inviarla ad Adobe per la revisione e la pubblicazione. Leggi [Invia per la revisione di una destinazione creata in Destination SDK](./submit-destination.md) per tutti gli altri passaggi è necessario eseguire questa operazione come parte del processo di invio della destinazione.

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
   "destinationAccess":"ALL"
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `destinationId` | Stringa | ID di destinazione della configurazione di destinazione che si sta inviando per la pubblicazione. Ottieni l&#39;ID di destinazione di una configurazione di destinazione utilizzando [riferimento API per la configurazione della destinazione](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Stringa | Utilizzo `ALL` affinché la destinazione venga visualizzata nel catalogo per tutti i clienti di Experience Platform. |

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
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `destinationId` | Stringa | ID di destinazione della configurazione di destinazione inviata per la pubblicazione. |
| `publishDetailsList.configId` | Stringa | ID univoco della richiesta di pubblicazione della destinazione per la destinazione inviata. |
| `publishDetailsList.allowedOrgs` | Stringa | Restituisce le organizzazioni di Experience Platform per le quali la destinazione è disponibile. <br> <ul><li> Per `"destinationType": "PUBLIC"`, questo parametro restituisce `"*"`, il che significa che la destinazione è disponibile per tutte le organizzazioni di Experience Platform.</li><li> Per `"destinationType": "DEV"`, questo parametro restituisce l&#39;ID organizzazione dell&#39;organizzazione utilizzato per creare e testare la destinazione.</li></ul> |
| `publishDetailsList.status` | Stringa | Lo stato della richiesta di pubblicazione della destinazione. I valori possibili sono `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinazioni con il valore `PUBLISHED` sono live e possono essere utilizzate dai clienti Experience Platform. |
| `publishDetailsList.destinationType` | Stringa | Tipo di destinazione. I valori possono essere `DEV` e `PUBLIC`. `DEV` corrisponde alla destinazione nell’organizzazione Experience Platform. `PUBLIC` corrisponde alla destinazione inviata per la pubblicazione. Pensa a queste due opzioni in termini Git, dove `DEV` rappresenta il ramo di authoring locale e il `PUBLIC` version rappresenta il ramo principale remoto. |
| `publishDetailsList.publishedDate` | Stringa | Data in cui la destinazione è stata inviata per la pubblicazione, in epoch time. |

{style=&quot;table-layout:auto&quot;}

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
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come inviare una richiesta di pubblicazione per la tua destinazione. Il team Adobe Experience Platform esaminerà la tua richiesta di pubblicazione e ti risponderà entro cinque giorni lavorativi.
