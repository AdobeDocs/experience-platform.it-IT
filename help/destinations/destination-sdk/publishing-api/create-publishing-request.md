---
description: Scopri come formattare una chiamata API per inviare una richiesta di pubblicazione di destinazione tramite Adobe Experience Platform Destination SDK.
title: Creare una richiesta di pubblicazione di destinazione
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# Creare una richiesta di pubblicazione di destinazione

>[!IMPORTANT]
>
>Devi utilizzare questo endpoint API solo se invii una destinazione prodotta (pubblica), che dovrà essere utilizzata da altri clienti Experienci Platform. Se crei una destinazione privata per uso personale, non è necessario inviare formalmente la destinazione utilizzando l’API di pubblicazione.

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

## Invia una configurazione di destinazione per la pubblicazione {#create}

Per inviare una configurazione di destinazione per la pubblicazione, devi effettuare una richiesta POST al `/authoring/destinations/publish` endpoint.

**Formato API**

```http
POST /authoring/destinations/publish
```

+++Richiesta

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
| `destinationId` | Stringa | ID di destinazione della configurazione di destinazione che si sta inviando per la pubblicazione. Ottieni l’ID di destinazione di una configurazione di destinazione utilizzando [recuperare una configurazione di destinazione](../authoring-api/destination-configuration/retrieve-destination-configuration.md) Chiamata API. |
| `destinationAccess` | Stringa | Utilizzare `ALL` affinché la tua destinazione venga visualizzata nel catalogo per tutti i clienti di Experienci Platform. |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con i dettagli della richiesta di pubblicazione di destinazione.

+++

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come inviare una richiesta di pubblicazione per la tua destinazione. Il team Adobe Experience Platform esaminerà la richiesta di pubblicazione e ti contatterà entro cinque giorni lavorativi.
