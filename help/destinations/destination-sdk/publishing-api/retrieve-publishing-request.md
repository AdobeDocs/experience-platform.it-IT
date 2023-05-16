---
description: Questa pagina esemplifica la chiamata API utilizzata per recuperare i dettagli su una richiesta di pubblicazione di destinazione tramite Adobe Experience Platform Destination SDK.
title: Recupera una richiesta di pubblicazione di destinazione
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 3%

---


# Recupera una richiesta di pubblicazione di destinazione

>[!IMPORTANT]
>
>È necessario utilizzare questo endpoint API solo se si invia una destinazione di prodotto (pubblico) da utilizzare per altri clienti Experience Platform. Se crei una destinazione privata per tuo uso, non devi inviare formalmente la destinazione utilizzando l’API di pubblicazione.

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Dopo aver configurato e verificato la destinazione, puoi inviarla ad Adobe per la revisione e la pubblicazione. Leggi [Invia per la revisione di una destinazione creata in Destination SDK](../guides/submit-destination.md) per tutti gli altri passaggi è necessario eseguire questa operazione come parte del processo di invio della destinazione.

Utilizza l’endpoint API delle destinazioni di pubblicazione per inviare una richiesta di pubblicazione quando:

* In qualità di partner di Destination SDK, vuoi rendere disponibile la tua destinazione di prodotto in tutte le organizzazioni Experience Platform affinché tutti i clienti di Experience Platform possano utilizzarla;
* Fai *qualsiasi aggiornamento* alle tue configurazioni. Gli aggiornamenti di configurazione si riflettono nella destinazione solo dopo aver inviato una nuova richiesta di pubblicazione, approvata dal team di Experience Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API di pubblicazione della destinazione {#get-started}

Prima di continuare, controlla la [guida introduttiva](../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Elenca richieste di pubblicazione di destinazione {#retrieve-list}

Puoi recuperare un elenco di tutte le destinazioni inviate per la pubblicazione per la tua organizzazione IMS effettuando una richiesta di GET al `/authoring/destinations/publish` punto finale.

**Formato API**

Utilizza il seguente formato API per recuperare tutte le richieste di pubblicazione per il tuo account.

```http
GET /authoring/destinations/publish
```

Utilizza il seguente formato API per recuperare una richiesta di pubblicazione specifica, definita dalla `{DESTINATION_ID}` parametro .

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Richiesta**

Le due richieste seguenti recuperano tutte le richieste di pubblicazione per la tua organizzazione IMS o una richiesta di pubblicazione specifica, a seconda che passi o meno la `DESTINATION_ID` nella richiesta.

Seleziona ciascuna scheda qui sotto per visualizzare il payload corrispondente.

>[!BEGINTABS]

>[!TAB Recupera tutte le richieste di pubblicazione]

+++Richiesta

La seguente richiesta recupererà l’elenco delle richieste di pubblicazione inviate, in base a [!DNL IMS Org ID] e la configurazione della sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Risposta

La risposta seguente restituisce lo stato HTTP 200 con un elenco di tutte le destinazioni inviate per la pubblicazione a cui hai accesso, in base all’ID organizzazione IMS e al nome della sandbox utilizzati. Uno `configId` corrisponde alla richiesta di pubblicazione per una destinazione.

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
| `publishDetailsList.configId` | Stringa | ID univoco della richiesta di pubblicazione della destinazione per la destinazione inviata. |
| `publishDetailsList.allowedOrgs` | Stringa | Restituisce le organizzazioni di Experience Platform per le quali la destinazione è disponibile. <br> <ul><li> Per `"destinationType": "PUBLIC"`, questo parametro restituisce `"*"`, il che significa che la destinazione è disponibile per tutte le organizzazioni di Experience Platform.</li><li> Per `"destinationType": "DEV"`, questo parametro restituisce l&#39;ID organizzazione dell&#39;organizzazione utilizzato per creare e testare la destinazione.</li></ul> |
| `publishDetailsList.status` | Stringa | Lo stato della richiesta di pubblicazione della destinazione. I valori possibili sono `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinazioni con il valore `PUBLISHED` sono live e possono essere utilizzate dai clienti Experience Platform. |
| `publishDetailsList.destinationType` | Stringa | Tipo di destinazione. I valori possono essere `DEV` e `PUBLIC`. `DEV` corrisponde alla destinazione nell’organizzazione Experience Platform. `PUBLIC` corrisponde alla destinazione inviata per la pubblicazione. Pensa a queste due opzioni in termini Git, dove `DEV` rappresenta il ramo di authoring locale e il `PUBLIC` version rappresenta il ramo principale remoto. |
| `publishDetailsList.publishedDate` | Stringa | Data in cui la destinazione è stata inviata per la pubblicazione, in epoch time. |

{style="table-layout:auto"}

+++

>[!TAB Recupera una richiesta di pubblicazione specifica]

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

Se hai passato un `DESTINATION_ID` nella chiamata API , la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sulla richiesta di pubblicazione della destinazione specificata.

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

{style="table-layout:auto"}

+++

>[!ENDTABS]

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.