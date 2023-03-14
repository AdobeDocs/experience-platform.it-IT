---
description: Questa pagina elenca e descrive tutte le operazioni API che è possibile eseguire utilizzando l’endpoint API "/authoring/destinations/publish".
title: Operazioni endpoint API per la pubblicazione delle destinazioni
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 1fb0fde2054528679235268ae96e3b7e78de80ef
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 4%

---

# Operazioni API per l’endpoint &quot;Destinations&quot; di pubblicazione {#publish-destination}

>[!IMPORTANT]
>
>Devi utilizzare questo endpoint API solo se invii una destinazione prodotta (pubblica), che dovrà essere utilizzata da altri clienti Experience Platform. Se crei una destinazione privata per uso personale, non è necessario inviare formalmente la destinazione utilizzando l’API di pubblicazione.

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Questa pagina elenca e descrive tutte le operazioni API che è possibile eseguire utilizzando `/authoring/destinations/publish` Endpoint API

Dopo aver configurato e testato la destinazione, puoi inviarla ad Adobe per la revisione e la pubblicazione. Letto [Invia per la revisione una destinazione creata in Destination SDK](./submit-destination.md) per tutte le altre operazioni da eseguire nell&#39;ambito del processo di invio della destinazione.

Utilizza l’endpoint API per la pubblicazione delle destinazioni per inviare una richiesta di pubblicazione quando:

* In qualità di partner di Destination SDK, desideri rendere la tua destinazione prodotta disponibile in tutte le organizzazioni di Experienci Platform per tutti i clienti di Experienci Platform da utilizzare;
* Fai *qualsiasi aggiornamento* alle configurazioni. Gli aggiornamenti della configurazione vengono rispecchiati nella destinazione solo dopo l’invio di una nuova richiesta di pubblicazione, approvata dal team di Experienci Platform.

<!-- * You want to make your custom destination available in your own Experience Platform organization, across all sandboxes. -->

## Guida introduttiva alle operazioni API di pubblicazione di destinazione {#get-started}

Prima di continuare, controlla [guida introduttiva](./getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Invia una configurazione di destinazione per la pubblicazione {#create}

Per inviare una configurazione di destinazione per la pubblicazione, devi effettuare una richiesta POST al `/authoring/destinations/publish` endpoint.

**Formato API**

```http
POST /authoring/destinations/publish
```

**Richiesta**

La richiesta seguente invia una destinazione per la pubblicazione, tra le organizzazioni configurate dai parametri forniti nel payload. Il payload riportato di seguito include tutti i parametri accettati dal `/authoring/destinations/publish` endpoint.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `destinationId` | Stringa | ID di destinazione della configurazione di destinazione che si sta inviando per la pubblicazione. Ottieni l’ID di destinazione di una configurazione di destinazione utilizzando [riferimento API per la configurazione di destinazione](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Stringa | Utilizzare `ALL` affinché la tua destinazione venga visualizzata nel catalogo per tutti i clienti di Experience Platform. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con i dettagli della richiesta di pubblicazione di destinazione.

## Elencare richieste di pubblicazione di destinazione {#retrieve-list}

Per recuperare un elenco di tutte le destinazioni inviate per la pubblicazione per la tua organizzazione IMS, devi effettuare una richiesta GET al `/authoring/destinations/publish` endpoint.

**Formato API**

```http
GET /authoring/destinations/publish
```

**Richiesta**

La richiesta seguente recupera l’elenco delle destinazioni inviate per la pubblicazione a cui hai accesso, in base alla configurazione di sandbox e organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La seguente risposta restituisce lo stato HTTP 200 con un elenco di destinazioni inviate per la pubblicazione a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Uno `configId` corrisponde alla richiesta di pubblicazione per una destinazione.

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
| `publishDetailsList.configId` | Stringa | ID univoco della richiesta di pubblicazione di destinazione per la destinazione inviata. |
| `publishDetailsList.allowedOrgs` | Stringa | Restituisce le organizzazioni di Experience Platform per le quali è disponibile la destinazione. <br> <ul><li> Per `"destinationType": "PUBLIC"`, questo parametro restituisce `"*"`, il che significa che la destinazione è disponibile per tutte le organizzazioni Experience Platform.</li><li> Per `"destinationType": "DEV"`, questo parametro restituisce l’ID organizzazione dell’organizzazione utilizzata per l’authoring e il test della destinazione.</li></ul> |
| `publishDetailsList.status` | Stringa | Lo stato della richiesta di pubblicazione di destinazione. I valori possibili sono `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinazioni con il valore `PUBLISHED` sono live e possono essere utilizzate dai clienti Experience Platform. |
| `publishDetailsList.destinationType` | Stringa | Il tipo di destinazione. I valori possono essere `DEV` e `PUBLIC`. `DEV` corrisponde alla destinazione nell’organizzazione Experience Platform. `PUBLIC` corrisponde alla destinazione inviata per la pubblicazione. Considera queste due opzioni in termini Git, dove `DEV` rappresenta il ramo di authoring locale e il `PUBLIC` version rappresenta il ramo principale remoto. |
| `publishDetailsList.publishedDate` | Stringa | La data in cui la destinazione è stata inviata per la pubblicazione, in tempo reale. |

{style="table-layout:auto"}

## Ottenere lo stato di una richiesta di pubblicazione di destinazione specifica {#get}

Per recuperare informazioni dettagliate su una specifica richiesta di pubblicazione di destinazione, effettua una richiesta GET al `/authoring/destinations/publish` e fornendo l’ID della destinazione per la quale desideri recuperare lo stato di pubblicazione.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sulla richiesta di pubblicazione di destinazione specificata.

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

Dopo aver letto questo documento, ora sai come inviare una richiesta di pubblicazione per la tua destinazione. Il team Adobe Experience Platform esaminerà la richiesta di pubblicazione e ti contatterà entro cinque giorni lavorativi.
