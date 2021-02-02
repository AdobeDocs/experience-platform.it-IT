---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;anteprima;esempio
title: Anteprima profilo - API profilo cliente in tempo reale
description: Utilizzando gli endpoint API del profilo cliente in tempo reale, potete visualizzare l'anteprima dell'ultimo esempio di successo dei dati del profilo, nonché elencare la distribuzione del profilo per set di dati e per namespace di identità all'interno di Adobe Experience Platform.
topic: guide
translation-type: tm+mt
source-git-commit: fe93a3672f65168744b3a242be7f42012f323544
workflow-type: tm+mt
source-wordcount: '1551'
ht-degree: 1%

---


# Anteprima dell’endpoint di stato del campione (anteprima profilo)

Adobe Experience Platform consente di acquisire dati dei clienti da più origini per creare profili unificati solidi per i singoli clienti. Poiché i dati abilitati per il profilo cliente in tempo reale vengono trasferiti in [!DNL Platform], vengono memorizzati nell&#39;archivio dati del profilo.

Quando l’inserimento di record nell’archivio profili aumenta o diminuisce il conteggio totale dei profili di oltre il 5%, viene attivato un processo per aggiornare il conteggio. Per i flussi di lavoro dei dati in streaming, viene effettuato un controllo ogni ora per determinare se è stata raggiunta la soglia di incremento o riduzione del 5%. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio. Per l’inserimento batch, entro 15 minuti dal corretto inserimento di un batch nell’archivio profili, se viene raggiunta la soglia di incremento o riduzione del 5%, viene eseguito un processo per aggiornare il conteggio. Utilizzando l&#39;API Profile è possibile visualizzare in anteprima l&#39;ultimo processo di esempio riuscito, nonché la distribuzione del profilo di elenco per set di dati e per namespace di identità.

Queste metriche sono disponibili anche nella sezione [!UICONTROL Profiles] dell&#39;interfaccia utente del Experience Platform . Per informazioni su come accedere ai dati del profilo utilizzando l&#39;interfaccia utente, visitare la [[!DNL Profile] guida utente](../ui/user-guide.md).

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39; [[!DNL Real-time Customer Profile] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Prima di continuare, consultare la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per eseguire correttamente chiamate a qualsiasi API [!DNL Experience Platform].

## Frammenti di profilo e profili uniti

Questa guida fa riferimento sia ai &quot;frammenti di profilo&quot; che ai &quot;profili uniti&quot;. È importante comprendere la differenza tra questi termini prima di procedere.

Ciascun profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare una singola vista del cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, l&#39;organizzazione avrà più frammenti di profilo correlati a tale singolo cliente che saranno visualizzati in più set di dati. Quando questi frammenti vengono assimilati in Piattaforma, vengono uniti (in base ai criteri di unione) per creare un unico profilo per il cliente. Pertanto, è probabile che il numero totale di frammenti di profilo sia sempre superiore al numero totale di profili uniti, in quanto ogni profilo è composto da più frammenti.

## Visualizza stato ultimo campione {#view-last-sample-status}

È possibile eseguire una richiesta di GET all&#39;endpoint `/previewsamplestatus` per visualizzare i dettagli dell&#39;ultimo processo di esempio eseguito correttamente per l&#39;organizzazione IMS. Ciò include il numero totale di profili nell&#39;esempio, nonché la metrica del conteggio dei profili, o il numero totale di profili di cui dispone l&#39;organizzazione all&#39;interno  Experience Platform. Il conteggio dei profili viene generato dopo l&#39;unione dei frammenti di profilo per creare un unico profilo per ciascun cliente. In altre parole, l&#39;organizzazione potrebbe avere più frammenti di profilo correlati a un singolo cliente che interagisce con il proprio marchio tra canali diversi, ma tali frammenti sarebbero uniti (in base al criterio di unione predefinito) e restituirebbero un conteggio di profilo pari a &quot;1&quot; perché tutti correlati allo stesso individuo.

Il conteggio dei profili include anche profili con attributi (dati di record) e profili contenenti solo dati di serie temporali (eventi), come  profili Adobe Analytics. Il processo di esempio viene aggiornato regolarmente durante l’assimilazione dei dati del profilo, al fine di fornire un numero totale aggiornato di profili all’interno della piattaforma.

**Formato API**

```http
GET /previewsamplestatus
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include i dettagli dell&#39;ultimo processo di esempio riuscito eseguito per l&#39;organizzazione IMS.

>[!NOTE]
>
>In questo esempio, `numRowsToRead` e `totalRows` sono uguali tra loro. A seconda del numero di profili di cui dispone la vostra organizzazione nel  Experience Platform, questo potrebbe essere il caso. Tuttavia, in genere questi due numeri sono diversi, con `numRowsToRead` il numero più piccolo, perché rappresenta il campione come un sottoinsieme del numero totale di profili (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "cosmosDocCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| Proprietà | Descrizione |
|---|---|
| `numRowsToRead` | Il numero totale di profili uniti nell&#39;esempio. |
| `sampleJobRunning` | Valore booleano che restituisce `true` quando è in corso un processo di esempio. Fornisce la trasparenza della latenza che si verifica da quando un file batch viene caricato quando viene effettivamente aggiunto all&#39;archivio dei profili. |
| `cosmosDocCount` | Totale del numero di documenti in Cosmo. |
| `totalFragmentCount` | Numero totale di frammenti di profilo nell&#39;archivio profili. |
| `lastSuccessfulBatchTimestamp` | Timestamp ultimo caricamento batch riuscito. |
| `streamingDriven` | *Questo campo è stato dichiarato obsoleto e non contiene alcun significato per la risposta.* |
| `totalRows` | Numero totale di profili uniti nella piattaforma Experience, noti anche come &#39;profilo count&#39;. |
| `lastBatchId` | ID assimilazione ultimo batch. |
| `status` | Stato dell’ultimo campione. |
| `samplingRatio` | Rapporto tra i profili uniti campionati (`numRowsToRead`) e i profili uniti totali (`totalRows`), espressi in percentuale in formato decimale. |
| `mergeStrategy` | Strategia di unione utilizzata nel campione. |
| `lastSampledTimestamp` | Timestamp ultimo esempio riuscito. |

## Distribuzione dei profili di elenco per set di dati

Per visualizzare la distribuzione dei profili per set di dati, puoi eseguire una richiesta di GET all&#39;endpoint `/previewsamplestatus/report/dataset`.

**Formato API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se alla data sono stati eseguiti più rapporti, verrà restituito il rapporto più recente per quella data. Se non esiste un rapporto per la data specificata, verrà restituito un errore 404. Se non viene specificata alcuna data, verrà restituito il rapporto più recente. Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

**Richiesta**

La richiesta seguente utilizza il parametro `date` per restituire il report più recente per la data specificata.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include un array `data` contenente un elenco di oggetti dataset. La risposta mostrata è stata troncata per mostrare tre set di dati.

>[!NOTE]
>
>Se esistevano più rapporti per la data, verrà restituita solo l&#39;ultima. Se per la data specificata non esisteva un report dataset, viene restituito lo stato HTTP 404 (non trovato).

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Proprietà | Descrizione |
|---|---|
| `sampleCount` | Il numero totale di profili uniti campionati con questo ID set di dati. |
| `samplePercentage` | Il valore `sampleCount` come percentuale del numero totale di profili uniti campionati (il valore `numRowsToRead` come restituito nell&#39; [ultimo stato del campione](#view-last-sample-status)), espresso in formato decimale. |
| `fullIDsCount` | Numero totale di profili uniti con questo ID set di dati. |
| `fullIDsPercentage` | Il valore `fullIDsCount` come percentuale del numero totale di profili uniti (il valore `totalRows` restituito nell&#39; [ultimo stato del campione](#view-last-sample-status)), espresso in formato decimale. |
| `name` | Nome del set di dati, come fornito durante la creazione del set di dati. |
| `description` | Descrizione del dataset, come fornito durante la creazione del dataset. |
| `value` | ID del set di dati. |
| `streamingIngestionEnabled` | Indica se il set di dati è abilitato per l’assimilazione in streaming. |
| `createdUser` | L&#39;ID utente dell&#39;utente che ha creato il set di dati. |
| `reportTimestamp` | Il timestamp del report. Se durante la richiesta è stato fornito un parametro `date`, il rapporto restituito è relativo alla data specificata. Se non viene fornito alcun parametro `date`, viene restituito il rapporto più recente. |



## Distribuzione dei profili di elenco per namespace

Potete eseguire una richiesta di GET all&#39;endpoint `/previewsamplestatus/report/namespace` per visualizzare la suddivisione per namespace identità in tutti i profili uniti nell&#39;archivio dei profili. Gli spazi dei nomi delle identità sono un componente importante di Adobe Experience Platform Identity Service che funge da indicatori del contesto a cui si riferiscono i dati dei clienti. Per ulteriori informazioni, visitare la [panoramica dello spazio nomi identità](../../identity-service/namespaces.md).

>[!NOTE]
>
>Il numero totale di profili per namespace (aggiungendo insieme i valori mostrati per ogni namespace) sarà sempre superiore alla metrica del conteggio dei profili, perché un profilo potrebbe essere associato a più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più spazi dei nomi.

**Formato API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se alla data sono stati eseguiti più rapporti, verrà restituito il rapporto più recente per quella data. Se non esiste un rapporto per la data specificata, verrà restituito un errore 404. Se non viene specificata alcuna data, verrà restituito il rapporto più recente. Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

**Richiesta**

La richiesta seguente non specifica un parametro `date` e pertanto restituisce il report più recente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include un array `data`, con singoli oggetti che contengono i dettagli per ogni namespace. La risposta mostrata è stata troncata per mostrare quattro spazi dei nomi.

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Proprietà | Descrizione |
|---|---|
| `sampleCount` | Il numero totale di profili uniti campionati nello spazio dei nomi. |
| `samplePercentage` | La `sampleCount` come percentuale dei profili uniti campionati (il valore `numRowsToRead` come restituito nell&#39; [ultimo stato del campione](#view-last-sample-status)), espresso in formato decimale. |
| `reportTimestamp` | Il timestamp del report. Se durante la richiesta è stato fornito un parametro `date`, il rapporto restituito è relativo alla data specificata. Se non viene fornito alcun parametro `date`, viene restituito il rapporto più recente. |
| `fullIDsFragmentCount` | Numero totale di frammenti di profilo nello spazio dei nomi. |
| `fullIDsCount` | Il numero totale di profili uniti nello spazio dei nomi. |
| `fullIDsPercentage` | La `fullIDsCount` come percentuale del totale dei profili uniti (il valore `totalRows` come restituito nell&#39; [ultimo stato del campione](#view-last-sample-status)), espresso in formato decimale. |
| `code` | `code` per lo spazio dei nomi. Questo si può trovare quando si utilizzano gli spazi dei nomi utilizzando l&#39; [API del servizio identità Adobe Experience Platform](../../identity-service/api/list-namespaces.md) ed è anche denominato [!UICONTROL Identity symbol] nell&#39;interfaccia utente del Experience Platform . Per ulteriori informazioni, visitare la [panoramica dello spazio nomi identità](../../identity-service/namespaces.md). |
| `value` | Il valore `id` dello spazio dei nomi. Questo è possibile quando si utilizzano gli spazi dei nomi mediante l&#39;API [Servizio identità](../../identity-service/api/list-namespaces.md). |

## Passaggi successivi

Potete inoltre utilizzare stime e anteprime simili per visualizzare le informazioni a livello di riepilogo relative alle definizioni dei segmenti, in modo da garantire l&#39;isolamento dell&#39;audience prevista. Per trovare i passaggi dettagliati per l&#39;utilizzo delle anteprime e delle stime dei segmenti utilizzando l&#39;API [!DNL Adobe Experience Platform Segmentation Service], visita la [guida alle anteprime e alle endpoint delle stime](../../segmentation/api/previews-and-estimates.md), parte della [!DNL Segmentation] Guida per gli sviluppatori di API.

