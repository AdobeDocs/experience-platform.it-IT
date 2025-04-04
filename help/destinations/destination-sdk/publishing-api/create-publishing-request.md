---
description: Scopri come formattare una chiamata API per inviare una richiesta di pubblicazione di destinazione tramite Adobe Experience Platform Destination SDK.
title: Creare una richiesta di pubblicazione di destinazione
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# Creare una richiesta di pubblicazione di destinazione

>[!IMPORTANT]
>
>Devi utilizzare questo endpoint API solo se invii una destinazione prodotta (pubblica), per essere utilizzata da altri clienti Experience Platform. Se crei una destinazione privata per uso personale, non è necessario inviare formalmente la destinazione utilizzando l’API di pubblicazione.

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Dopo aver configurato e testato la destinazione, puoi inviarla ad Adobe per la revisione e la pubblicazione. Leggi [Invia per rivedere una destinazione creata in Destination SDK](../guides/submit-destination.md) per tutti gli altri passaggi da eseguire durante il processo di invio della destinazione.

Utilizza l’endpoint API per la pubblicazione delle destinazioni per inviare una richiesta di pubblicazione quando:

* In qualità di partner Destination SDK, desideri rendere la tua destinazione prodotta disponibile in tutte le organizzazioni Experience Platform per tutti i clienti Experience Platform da utilizzare;
* Hai apportato *qualsiasi aggiornamento* alle tue configurazioni. Gli aggiornamenti della configurazione vengono rispecchiati nella destinazione solo dopo l’invio di una nuova richiesta di pubblicazione, approvata dal team di Experience Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API di pubblicazione di destinazione {#get-started}

Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Invia una configurazione di destinazione per la pubblicazione {#create}

È possibile inviare una configurazione di destinazione per la pubblicazione effettuando una richiesta POST all&#39;endpoint `/authoring/destinations/publish`.

**Formato API**

```http
POST /authoring/destinations/publish
```

+++Richiesta

La richiesta seguente invia una destinazione per la pubblicazione, tra le organizzazioni configurate dai parametri forniti nel payload. Il payload seguente include tutti i parametri accettati dall&#39;endpoint `/authoring/destinations/publish`.

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
| `destinationId` | Stringa | ID di destinazione della configurazione di destinazione che si sta inviando per la pubblicazione. Ottenere l&#39;ID di destinazione di una configurazione di destinazione utilizzando la chiamata API [per recuperare una configurazione di destinazione](../authoring-api/destination-configuration/retrieve-destination-configuration.md). |
| `destinationAccess` | Stringa | Utilizza `ALL` per far apparire la tua destinazione nel catalogo per tutti i clienti Experience Platform. |

{style="table-layout:auto"}

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con i dettagli della richiesta di pubblicazione di destinazione.

+++

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come inviare una richiesta di pubblicazione per la tua destinazione. Il team Adobe Experience Platform esaminerà la richiesta di pubblicazione e ti contatterà entro cinque giorni lavorativi.
