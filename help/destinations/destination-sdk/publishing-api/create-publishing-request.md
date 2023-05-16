---
description: Scopri come formattare una chiamata API per inviare una richiesta di pubblicazione di destinazione tramite Adobe Experience Platform Destination SDK.
title: Creare una richiesta di pubblicazione di destinazione
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---


# Creare una richiesta di pubblicazione di destinazione

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

## Invia una configurazione di destinazione per la pubblicazione {#create}

Puoi inviare una configurazione di destinazione per la pubblicazione effettuando una richiesta di POST al `/authoring/destinations/publish` punto finale.

**Formato API**

```http
POST /authoring/destinations/publish
```

+++Richiesta

La seguente richiesta invia una destinazione per la pubblicazione, tra le organizzazioni configurate dai parametri forniti nel payload. Il payload seguente include tutti i parametri accettati dal `/authoring/destinations/publish` punto finale.

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
| `destinationId` | Stringa | ID di destinazione della configurazione di destinazione che si sta inviando per la pubblicazione. Ottieni l&#39;ID di destinazione di una configurazione di destinazione utilizzando [recuperare una configurazione di destinazione](../authoring-api/destination-configuration/retrieve-destination-configuration.md) Chiamata API. |
| `destinationAccess` | Stringa | Utilizzo `ALL` affinché la destinazione venga visualizzata nel catalogo per tutti i clienti di Experience Platform. |

{style="table-layout:auto"}

+++Risposta

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli della richiesta di pubblicazione della destinazione.

## Gestione degli errori API

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come inviare una richiesta di pubblicazione per la tua destinazione. Il team Adobe Experience Platform esaminerà la tua richiesta di pubblicazione e ti risponderà entro cinque giorni lavorativi.