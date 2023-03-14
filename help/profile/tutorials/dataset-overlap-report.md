---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;rapporto;rapporto di sovrapposizione set di dati;dati profilo
title: Generare il rapporto di sovrapposizione del set di dati
type: Tutorial
description: Questa esercitazione illustra i passaggi necessari per generare il rapporto di sovrapposizione dei set di dati utilizzando l’API Profilo cliente in tempo reale.
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---

# Generare il rapporto di sovrapposizione del set di dati

Il rapporto di sovrapposizione del set di dati fornisce visibilità sulla composizione del [!DNL Profile] archiviare esponendo i set di dati che contribuiscono maggiormente al pubblico indirizzabile (profili).

Oltre a fornire informazioni approfondite sui dati, questo rapporto può aiutarti a intraprendere azioni per ottimizzare l’utilizzo della licenza, ad esempio impostare un limite alla durata di alcuni dati.

Questa esercitazione illustra i passaggi necessari per generare il rapporto di sovrapposizione dei set di dati utilizzando [!DNL Real-Time Customer Profile] e interpretare i risultati per la tua organizzazione.

## Introduzione

Per utilizzare le API di Adobe Experience Platform, devi prima completare la sezione [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per raccogliere i valori necessari per le intestazioni richieste. Per ulteriori informazioni sulle API di Experience Platform, consulta [guida introduttiva alle API di Platform](../../landing/api-guide.md).

Le intestazioni richieste per tutte le chiamate API in questa esercitazione sono:

* `Authorization: Bearer {ACCESS_TOKEN}`: Il `Authorization` l’intestazione richiede un token di accesso preceduto dalla parola `Bearer`. È necessario generare un nuovo valore del token di accesso ogni 24 ore.
* `x-api-key: {API_KEY}`: Il `API Key` è anche noto come `Client ID` e è un valore che deve essere generato una sola volta.
* `x-gw-ims-org-id: {ORG_ID}`: Il `IMS Org` è anche noto come `Organization ID` e deve essere generato una sola volta.

Dopo aver completato il tutorial di autenticazione e raccolto i valori per le intestazioni richieste, sei pronto per iniziare a effettuare chiamate all’API cliente in tempo reale.

## Genera report di sovrapposizione set di dati utilizzando la riga di comando

Se hai familiarità con l’utilizzo della riga di comando, puoi utilizzare la seguente richiesta cURL per generare il rapporto di sovrapposizione dei set di dati eseguendo una richiesta GET a `/previewsamplestatus/report/dataset/overlap`.

**Richiesta**

La richiesta seguente utilizza `date` per restituire il rapporto più recente per la data specificata.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se in tale data sono stati eseguiti più rapporti, viene restituito il rapporto più recente per tale data. Se non esiste un rapporto per la data specificata, viene restituito un errore di stato HTTP 404 (Non trovato). Se non viene specificata alcuna data, viene restituito il rapporto più recente. Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

**Risposta**

In caso di esito positivo, la richiesta restituisce lo stato HTTP 200 (OK) e il rapporto di sovrapposizione dei set di dati. Il rapporto include `data` oggetto, contenente elenchi separati da virgole di set di dati e il rispettivo conteggio dei profili. Per informazioni dettagliate su come leggere il rapporto, consulta la sezione su [interpretazione dei dati del rapporto di sovrapposizione del set di dati](#interpret-the-report) più avanti in questa esercitazione.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### Genera report di sovrapposizione set di dati tramite Postman

Postman è una piattaforma collaborativa per lo sviluppo API ed è utile per visualizzare le chiamate API. Può essere scaricato gratuitamente dal [Sito Web Postman](https://www.postman.com) e fornisce un’interfaccia utente di facile utilizzo per l’esecuzione delle chiamate API. Le schermate seguenti utilizzano l’interfaccia di Postman.

**Richiesta**

La procedura seguente illustra come richiedere il rapporto di sovrapposizione dei set di dati utilizzando Postman:

* Dal menu a discesa, seleziona GET come tipo di richiesta.
* Inserisci le intestazioni richieste in `KEY` colonna:
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Immetti i valori generati durante l’autenticazione in `VALUE` , sostituendo le parentesi graffe (`{{ }}`) e qualsiasi contenuto tra parentesi graffe.
* Immetti il percorso della richiesta con o senza l’ `date` parametro:
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   oppure
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se in tale data sono stati eseguiti più rapporti, viene restituito il rapporto più recente per tale data. Se non esiste un rapporto per la data specificata, viene restituito un errore di stato HTTP 404 (Non trovato). Se non viene specificata alcuna data, viene restituito il rapporto più recente. <br/>Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

Una volta completato il tipo di richiesta, le intestazioni, i valori e il percorso, seleziona **Invia** per inviare la richiesta API e generare il rapporto.

![](../images/dataset-overlap-report/postman-request.png)

**Risposta**

In caso di esito positivo, la richiesta restituisce lo stato HTTP 200 (OK) e il rapporto di sovrapposizione dei set di dati. Il rapporto include `data` oggetto, contenente elenchi separati da virgole di set di dati e il rispettivo conteggio dei profili. Per informazioni dettagliate su come leggere il rapporto, consulta la sezione su [interpretazione dei dati del rapporto di sovrapposizione del set di dati](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## Interpretare i dati del rapporto di sovrapposizione del set di dati {#interpret-the-report}

Il rapporto di sovrapposizione dei set di dati generato fornisce una marca temporale che mostra la data e l’ora del rapporto e un oggetto dati che include combinazioni univoche di ID di set di dati come elenchi separati da virgole. Le sezioni seguenti forniscono informazioni aggiuntive relative ai componenti del rapporto.

### Timestamp del rapporto

Il `reportTimestamp` corrisponde alla data fornita nella richiesta API o, se non è stata fornita alcuna data, alla marca temporale del rapporto più recente.

### Elenco degli ID dei set di dati

Il `data` L’oggetto include combinazioni univoche di ID set di dati come elenchi separati da virgole con il rispettivo conteggio dei profili per tale combinazione di set di dati.

>[!NOTE]
>
>La somma di tutti i conteggi di profili associati a ogni riga del rapporto di sovrapposizione dei set di dati deve corrispondere al numero totale di profili nell’organizzazione.

Per interpretare i risultati del rapporto, considera l’esempio seguente:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Questo rapporto fornisce le seguenti informazioni:

* Sono disponibili 123 profili composti da dati provenienti dai seguenti set di dati: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Esistono 454.412 profili composti da dati provenienti da questi due set di dati: `5d92921872831c163452edc8` e `5eb2cdc6fa3f9a18a7592a98`.
* Esistono 107 profili composti solo da dati del set di dati `5eeda0032af7bb19162172a7`.
* Nell’organizzazione sono presenti in totale 454.642 profili.

## Passaggi successivi

Dopo aver completato questa esercitazione, ora puoi generare il rapporto di sovrapposizione dei set di dati utilizzando l’API Profilo cliente in tempo reale. Per ulteriori informazioni sull’utilizzo dei dati del profilo sia nell’API che nell’interfaccia utente di Experience Platform, leggi [Documentazione panoramica profilo](../home.md).
