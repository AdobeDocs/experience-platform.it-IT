---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;reporting;report di sovrapposizione set di dati;dati profilo
title: Genera il rapporto di sovrapposizione del set di dati
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per generare il rapporto di sovrapposizione dei set di dati utilizzando l’API del profilo cliente in tempo reale.
source-git-commit: f30f87527f5e903c851a140e7cbaad1964a48803
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---


# Genera il rapporto di sovrapposizione dei set di dati

Il rapporto di sovrapposizione dei set di dati fornisce visibilità nella composizione dell’ [!DNL Profile] archivio dell’organizzazione esponendo i set di dati che contribuiscono maggiormente al pubblico indirizzabile (profili).

Oltre a fornire approfondimenti sui tuoi dati, questo rapporto può aiutarti a intraprendere azioni per ottimizzare l’utilizzo della licenza, ad esempio per impostare un limite di vita di alcuni dati.

Questa esercitazione descrive i passaggi necessari per generare il rapporto di sovrapposizione dei set di dati utilizzando l’ [!DNL Real-time Customer Profile] API e interpretare i risultati per la tua organizzazione.

## Introduzione

Per utilizzare le API di Adobe Experience Platform, devi prima completare l&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per raccogliere i valori necessari per le intestazioni richieste. Per ulteriori informazioni sulle API di Experience Platform, consulta la [guida introduttiva alle API di Platform](../../landing/api-guide.md) .

Le intestazioni richieste per tutte le chiamate API in questa esercitazione sono:

* `Authorization: Bearer {ACCESS_TOKEN}`: L&#39; `Authorization` intestazione richiede un token di accesso preceduto dalla parola  `Bearer`. È necessario generare un nuovo valore token di accesso ogni 24 ore.
* `x-api-key: {API_KEY}`: Il  `API Key` è anche noto come  `Client ID` e è un valore che deve essere generato solo una volta.
* `x-gw-ims-org-id: {IMS_ORG}`: Il  `IMS Org` è anche noto come  `Organization ID` e deve essere generato solo una volta.

Dopo aver completato l’esercitazione sull’autenticazione e aver raccolto i valori per le intestazioni richieste, puoi iniziare a effettuare chiamate all’API del cliente in tempo reale.

## Genera report di sovrapposizione set di dati utilizzando la riga di comando

Se hai familiarità con l’utilizzo della riga di comando, puoi utilizzare la seguente richiesta cURL per generare il rapporto di sovrapposizione del set di dati eseguendo una richiesta GET a `/previewsamplestatus/report/dataset/overlap`.

**Richiesta**

La richiesta seguente utilizza il parametro `date` per restituire il report più recente per la data specificata.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se alla data sono stati eseguiti più rapporti, viene restituito il rapporto più recente per tale data. Se un report non esiste per la data specificata, viene restituito un errore di stato HTTP 404 (Non trovato). Se non viene specificata alcuna data, viene restituito il rapporto più recente. Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

**Risposta**

Una richiesta corretta restituisce lo stato HTTP 200 (OK) e il rapporto di sovrapposizione del set di dati. Il rapporto include un oggetto `data` contenente elenchi di set di dati separati da virgole e il rispettivo conteggio dei profili. Per informazioni dettagliate su come leggere il rapporto, consulta la sezione sull’ [interpretazione dei dati del rapporto di sovrapposizione dei set di dati](#interpret-the-report) più avanti in questa esercitazione.

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

### Genera report di sovrapposizione set di dati utilizzando Postman

Postman è una piattaforma collaborativa per lo sviluppo delle API ed è utile per visualizzare le chiamate API. Può essere scaricato gratuitamente dal sito web [Postman](https://www.postman.com) e fornisce un&#39;interfaccia utente facile da usare per eseguire le chiamate API. Le seguenti schermate utilizzano l’interfaccia Postman .

**Richiesta**

Per richiedere il report di sovrapposizione dei set di dati utilizzando Postman, completa i seguenti passaggi:

* Utilizzando il menu a discesa , seleziona GET come tipo di richiesta.
* Immetti le intestazioni richieste nella colonna `KEY` :
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Immetti i valori generati durante l&#39;autenticazione nella colonna `VALUE` , sostituendo le parentesi graffe (`{{ }}`) ed eventuali contenuti tra parentesi graffe.
* Immetti il percorso della richiesta con o senza il parametro opzionale `date`:
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   oppure
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se alla data sono stati eseguiti più rapporti, viene restituito il rapporto più recente per tale data. Se un report non esiste per la data specificata, viene restituito un errore di stato HTTP 404 (Non trovato). Se non viene specificata alcuna data, viene restituito il rapporto più recente. <br/>Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

Al termine del tipo di richiesta, delle intestazioni, dei valori e del percorso, seleziona **Invia** per inviare la richiesta API e generare il rapporto.

![](../images/dataset-overlap-report/postman-request.png)

**Risposta**

Una richiesta corretta restituisce lo stato HTTP 200 (OK) e il rapporto di sovrapposizione del set di dati. Il rapporto include un oggetto `data` contenente elenchi di set di dati separati da virgole e il rispettivo conteggio dei profili. Per informazioni dettagliate su come leggere il rapporto, consulta la sezione sull’ [interpretazione dei dati del rapporto di sovrapposizione dei set di dati](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## Interpreta i dati del rapporto di sovrapposizione del set di dati {#interpret-the-report}

Il rapporto di sovrapposizione dei set di dati generato fornisce una marca temporale che mostra la data e l’ora del rapporto e un oggetto dati che include combinazioni univoche di ID dei set di dati come elenchi separati da virgole. Le sezioni seguenti forniscono informazioni aggiuntive relative ai componenti del rapporto.

### Timestamp rapporto

La `reportTimestamp` corrisponde alla data fornita nella richiesta API o, se non è stata fornita alcuna data, alla marca temporale del rapporto più recente.

### Elenco degli ID dei set di dati

L&#39;oggetto `data` include combinazioni univoche di ID di set di dati come elenchi separati da virgole con il rispettivo conteggio di profilo per quella combinazione di set di dati.

>[!NOTE]
>
>La somma di tutti i conteggi di profilo associati a ciascuna riga del rapporto di sovrapposizione dei set di dati deve corrispondere al numero totale di profili nell’organizzazione.

Per interpretare i risultati del rapporto, considera l’esempio seguente:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Questo rapporto fornisce le seguenti informazioni:
* Esistono 123 profili composti da dati provenienti dai seguenti set di dati: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Esistono 454.412 profili composti da dati provenienti da questi due set di dati: `5d92921872831c163452edc8` e `5eb2cdc6fa3f9a18a7592a98`.
* Esistono 107 profili costituiti solo da dati del set di dati `5eeda0032af7bb19162172a7`.
* L’organizzazione dispone di un totale di 454.642 profili.

## Passaggi successivi

Dopo aver completato questa esercitazione, ora puoi generare il rapporto di sovrapposizione dei set di dati utilizzando l’API Profilo cliente in tempo reale. Per ulteriori informazioni sull’utilizzo dei dati di profilo sia nell’API che nell’interfaccia utente di Experience Platform, consulta la [documentazione della panoramica del profilo](../home.md).