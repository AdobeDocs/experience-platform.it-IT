---
description: Questa pagina esemplifica la chiamata API utilizzata per recuperare i dettagli di una richiesta di pubblicazione di destinazione tramite Adobe Experience Platform Destination SDK.
title: Recuperare una richiesta di pubblicazione di destinazione
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 3%

---


# Recuperare una richiesta di pubblicazione di destinazione

>[!IMPORTANT]
>
>Devi utilizzare questo endpoint API solo se invii una destinazione prodotta (pubblica), che dovrà essere utilizzata da altri clienti Experience Platform. Se crei una destinazione privata per uso personale, non è necessario inviare formalmente la destinazione utilizzando l’API di pubblicazione.

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Dopo aver configurato e testato la destinazione, puoi inviarla ad Adobe per la revisione e la pubblicazione. Letto [Invia per la revisione una destinazione creata in Destination SDK](../guides/submit-destination.md) per tutte le altre operazioni da eseguire nell&#39;ambito del processo di invio della destinazione.

Utilizza l’endpoint API per la pubblicazione delle destinazioni per inviare una richiesta di pubblicazione quando:

* In qualità di partner di Destination SDK, desideri rendere la tua destinazione prodotta disponibile in tutte le organizzazioni di Experienci Platform per tutti i clienti di Experienci Platform da utilizzare;
* Fai *qualsiasi aggiornamento* alle configurazioni. Gli aggiornamenti della configurazione vengono rispecchiati nella destinazione solo dopo l’invio di una nuova richiesta di pubblicazione, approvata dal team di Experienci Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API di pubblicazione di destinazione {#get-started}

Prima di continuare, controlla [guida introduttiva](../getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Elencare richieste di pubblicazione di destinazione {#retrieve-list}

Per recuperare un elenco di tutte le destinazioni inviate per la pubblicazione per la tua organizzazione IMS, devi effettuare una richiesta GET al `/authoring/destinations/publish` endpoint.

**Formato API**

Utilizza il seguente formato API per recuperare tutte le richieste di pubblicazione per il tuo account.

```http
GET /authoring/destinations/publish
```

Utilizza il seguente formato API per recuperare una richiesta di pubblicazione specifica, definita da `{DESTINATION_ID}` parametro.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Richiesta**

Le due richieste seguenti recuperano tutte le richieste di pubblicazione per l’organizzazione IMS o una richiesta di pubblicazione specifica, a seconda che venga passata o meno la `DESTINATION_ID` nella richiesta.

Seleziona ciascuna scheda di seguito per visualizzare il payload corrispondente.

>[!BEGINTABS]

>[!TAB Recupera tutte le richieste di pubblicazione]

+++Richiesta

La richiesta seguente recupererà l’elenco delle richieste di pubblicazione inviate, in base a [!DNL IMS Org ID] e la configurazione della sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Risposta

La risposta che segue restituisce lo stato HTTP 200 con un elenco di tutte le destinazioni inviate per la pubblicazione a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Uno `configId` corrisponde alla richiesta di pubblicazione per una destinazione.

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

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `destinationId` | Stringa | ID di destinazione della configurazione di destinazione inviata per la pubblicazione. |
| `publishDetailsList.configId` | Stringa | ID univoco della richiesta di pubblicazione di destinazione per la destinazione inviata. |
| `publishDetailsList.allowedOrgs` | Stringa | Restituisce le organizzazioni di Experience Platform per le quali è disponibile la destinazione. <br> <ul><li> Per `"destinationType": "PUBLIC"`, questo parametro restituisce `"*"`, il che significa che la destinazione è disponibile per tutte le organizzazioni Experience Platform.</li><li> Per `"destinationType": "DEV"`, questo parametro restituisce l’ID organizzazione dell’organizzazione utilizzata per l’authoring e il test della destinazione.</li></ul> |
| `publishDetailsList.status` | Stringa | Lo stato della richiesta di pubblicazione di destinazione. I valori possibili sono `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinazioni con il valore `PUBLISHED` sono live e possono essere utilizzate dai clienti Experience Platform. |
| `publishDetailsList.destinationType` | Stringa | Il tipo di destinazione. I valori possono essere `DEV` e `PUBLIC`. `DEV` corrisponde alla destinazione nell’organizzazione Experience Platform. `PUBLIC` corrisponde alla destinazione inviata per la pubblicazione. Considera queste due opzioni in termini Git, dove `DEV` rappresenta il ramo di authoring locale e il `PUBLIC` version rappresenta il ramo principale remoto. |
| `publishDetailsList.publishedDate` | Stringa | La data in cui la destinazione è stata inviata per la pubblicazione, in tempo reale. |

{style="table-layout:auto"}

+++

>[!TAB Recuperare una richiesta di pubblicazione specifica]

+++Richiesta

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID della destinazione per la quale desideri recuperare lo stato di pubblicazione. |

+++

+++Risposta

Se ha superato un `DESTINATION_ID` nella chiamata API, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sulla richiesta Publish di destinazione specificata.

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

+++

>[!ENDTABS]

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.