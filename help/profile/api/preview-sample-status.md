---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;anteprima;esempio
title: Endpoint API di anteprima dello stato del campione (anteprima profilo)
description: Utilizzando l’endpoint di stato di esempio per l’anteprima, parte dell’API Profilo cliente in tempo reale, puoi visualizzare in anteprima l’ultimo campione di dati di profilo riusciti, nonché elencare la distribuzione dei profili per set di dati e per namespace di identità in Adobe Experience Platform.
topic-legacy: guide
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1652'
ht-degree: 1%

---

# Anteprima dell’endpoint di stato di esempio (anteprima profilo)

Adobe Experience Platform consente di acquisire dati dei clienti da più sorgenti per creare solidi profili unificati per i singoli clienti. Poiché i dati abilitati per Profilo cliente in tempo reale vengono acquisiti in [!DNL Platform], vengono memorizzati nell’archivio dati Profilo.

Quando l’acquisizione dei record nell’archivio profili aumenta o diminuisce il conteggio totale dei profili di oltre il 5%, viene attivato un processo di campionamento per aggiornare il conteggio. Il modo in cui il campione viene attivato dipende dal tipo di acquisizione utilizzato:

* Per **flussi di lavoro di dati in streaming**, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o diminuzione del 5% è stata soddisfatta. In caso affermativo, viene attivato automaticamente un processo di esempio per aggiornare il conteggio.
* Per **l&#39;acquisizione batch**, entro 15 minuti dal corretto inserimento di un batch nell&#39;archivio profili, se viene soddisfatta la soglia di aumento o diminuzione del 5%, viene eseguito un processo per aggiornare il conteggio. Utilizzando l’API di profilo puoi visualizzare in anteprima il processo di esempio più recente, oltre a elencare la distribuzione dei profili per set di dati e per namespace di identità.

Queste metriche sono disponibili anche nella sezione [!UICONTROL Profiles] dell’interfaccia utente di Experience Platform. Per informazioni su come accedere ai dati del profilo utilizzando l&#39;interfaccia utente, visita la [[!DNL Profile] guida utente](../ui/user-guide.md).

>[!NOTE]
>
>Sono disponibili endpoint di stima e anteprima nell’API del servizio di segmentazione di Adobe Experience Platform che consentono di visualizzare informazioni di riepilogo sulle definizioni dei segmenti per assicurarsi di isolare il pubblico previsto. Per trovare i passaggi dettagliati per l’utilizzo dell’anteprima dei segmenti e degli endpoint di stima, visita la [guida alle anteprime e agli endpoint di stima](../../segmentation/api/previews-and-estimates.md), parte della guida per gli sviluppatori API [!DNL Segmentation].

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39; [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Frammenti di profilo e profili uniti

Questa guida fa riferimento sia ai &quot;frammenti di profilo&quot; che ai &quot;profili uniti&quot;. È importante comprendere la differenza tra questi termini prima di procedere.

Ogni singolo profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare una singola vista del cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi al singolo cliente che compaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti (in base al criterio di unione) per creare un unico profilo per il cliente. Pertanto, è probabile che il numero totale di frammenti di profilo sia sempre superiore al numero totale di profili uniti, in quanto ogni profilo è composto da più frammenti.

## Visualizza lo stato dell&#39;ultimo esempio {#view-last-sample-status}

Puoi eseguire una richiesta di GET all’endpoint `/previewsamplestatus` per visualizzare i dettagli dell’ultimo processo di esempio riuscito eseguito per l’organizzazione IMS. Ciò include il numero totale di profili nel campione, nonché la metrica di conteggio dei profili, o il numero totale di profili di cui la tua organizzazione dispone all’interno dell’Experience Platform. Il conteggio dei profili viene generato dopo l’unione dei frammenti di profilo per formare un singolo profilo per ogni singolo cliente. In altre parole, l’organizzazione può disporre di più frammenti di profilo relativi a un singolo cliente che interagisce con il tuo marchio su diversi canali, ma questi frammenti verranno uniti (in base al criterio di unione predefinito) e restituiranno un conteggio di &quot;1&quot; profilo perché sono tutti correlati allo stesso individuo.

Il conteggio dei profili include anche profili con attributi (dati record) e profili contenenti solo dati di serie temporali (eventi), ad esempio profili Adobe Analytics. Il processo di esempio viene aggiornato regolarmente man mano che i dati del profilo vengono acquisiti, al fine di fornire un numero totale aggiornato di profili all’interno di Platform.

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

La risposta include i dettagli dell’ultimo processo di esempio riuscito eseguito per l’organizzazione IMS.

>[!NOTE]
>
>In questo esempio di risposta, `numRowsToRead` e `totalRows` sono uguali tra loro. A seconda del numero di profili di cui dispone l’organizzazione nell’Experience Platform, ciò potrebbe accadere. Tuttavia, in genere questi due numeri sono diversi, con `numRowsToRead` come numero minore, perché rappresenta il campione come sottoinsieme del numero totale di profili (`totalRows`).

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
| `numRowsToRead` | Numero totale di profili uniti nel campione. |
| `sampleJobRunning` | Valore booleano che restituisce `true` quando è in corso un processo di esempio. Fornisce la trasparenza della latenza che si verifica dal momento in cui un file batch viene caricato al momento dell’aggiunta effettiva all’archivio profili. |
| `cosmosDocCount` | Numero totale di documenti in Cosmo. |
| `totalFragmentCount` | Numero totale di frammenti di profilo nell’archivio profili. |
| `lastSuccessfulBatchTimestamp` | Timestamp ultimo inserimento batch riuscito. |
| `streamingDriven` | *Questo campo è stato dichiarato obsoleto e non contiene alcun significato per la risposta.* |
| `totalRows` | Numero totale di profili uniti nell’Experience Platform, noto anche come &quot;conteggio dei profili&quot;. |
| `lastBatchId` | ID acquisizione ultimo batch. |
| `status` | Stato dell’ultimo campione. |
| `samplingRatio` | Rapporto tra i profili uniti campionati (`numRowsToRead`) e i profili uniti totali (`totalRows`), espresso in percentuale in formato decimale. |
| `mergeStrategy` | Strategia di unione utilizzata nel campione. |
| `lastSampledTimestamp` | Data e ora dell’ultimo esempio riuscito. |

## Elencare la distribuzione dei profili per set di dati

Per visualizzare la distribuzione dei profili per set di dati, puoi eseguire una richiesta GET all’endpoint `/previewsamplestatus/report/dataset` .

**Formato API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se alla data sono stati eseguiti più rapporti, verrà restituito il rapporto più recente per tale data. Se un report non esiste per la data specificata, verrà restituito un errore 404. Se non viene specificata alcuna data, verrà restituito il rapporto più recente. Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

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

La risposta include un array `data` contenente un elenco di oggetti set di dati. La risposta mostrata è stata troncata per mostrare tre set di dati.

>[!NOTE]
>
>Se esistono più rapporti per la data, viene restituita solo l’ultima. Se non esisteva un rapporto del set di dati per la data fornita, verrebbe restituito lo stato HTTP 404 (Non trovato).

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
| `sampleCount` | Il numero totale di profili uniti campionati con questo ID di set di dati. |
| `samplePercentage` | La `sampleCount` come percentuale del numero totale di profili uniti campionati (il valore `numRowsToRead` come restituito nel [stato dell&#39;ultimo campione](#view-last-sample-status)), espresso in formato decimale. |
| `fullIDsCount` | Il numero totale di profili uniti con questo ID di set di dati. |
| `fullIDsPercentage` | La `fullIDsCount` come percentuale del numero totale di profili uniti (il valore `totalRows` restituito nel [stato dell&#39;ultimo campione](#view-last-sample-status)), espresso in formato decimale. |
| `name` | Nome del set di dati, come fornito durante la creazione del set di dati. |
| `description` | Descrizione del set di dati, come fornito durante la creazione del set di dati. |
| `value` | ID del set di dati. |
| `streamingIngestionEnabled` | Se il set di dati è abilitato per l’acquisizione in streaming. |
| `createdUser` | ID utente dell’utente che ha creato il set di dati. |
| `reportTimestamp` | La marca temporale del rapporto. Se durante la richiesta è stato fornito un parametro `date` , il rapporto restituito è relativo alla data fornita. Se non viene fornito alcun parametro `date`, viene restituito il rapporto più recente. |

## Distribuzione del profilo di elenco in base allo spazio dei nomi

Puoi eseguire una richiesta di GET all’endpoint `/previewsamplestatus/report/namespace` per visualizzare la suddivisione per namespace di identità in tutti i profili uniti nell’archivio profili. Gli spazi dei nomi di identità sono un componente importante del servizio Adobe Experience Platform Identity che funge da indicatori del contesto a cui si riferiscono i dati dei clienti. Per ulteriori informazioni, visita la [panoramica dello spazio dei nomi identità](../../identity-service/namespaces.md).

>[!NOTE]
>
>Il numero totale di profili per namespace (aggiunta insieme dei valori mostrati per ogni namespace) sarà sempre più alto della metrica di conteggio dei profili, perché un profilo può essere associato a più namespace. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più namespace.

**Formato API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se alla data sono stati eseguiti più rapporti, verrà restituito il rapporto più recente per tale data. Se un report non esiste per la data specificata, verrà restituito un errore 404. Se non viene specificata alcuna data, verrà restituito il rapporto più recente. Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

**Richiesta**

La richiesta seguente non specifica un parametro `date` e pertanto restituisce il rapporto più recente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include un array `data` con singoli oggetti contenenti i dettagli di ogni namespace. La risposta mostrata è stata troncata per mostrare quattro namespace.

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
| `sampleCount` | Numero totale di profili uniti campionati nello spazio dei nomi. |
| `samplePercentage` | La `sampleCount` come percentuale dei profili uniti campionati (il valore `numRowsToRead` come restituito nel [stato dell&#39;ultimo campione](#view-last-sample-status)), espresso in formato decimale. |
| `reportTimestamp` | La marca temporale del rapporto. Se durante la richiesta è stato fornito un parametro `date` , il rapporto restituito è relativo alla data fornita. Se non viene fornito alcun parametro `date`, viene restituito il rapporto più recente. |
| `fullIDsFragmentCount` | Numero totale di frammenti di profilo nello spazio dei nomi. |
| `fullIDsCount` | Numero totale di profili uniti nello spazio dei nomi. |
| `fullIDsPercentage` | Il `fullIDsCount` come percentuale del totale dei profili uniti (il valore `totalRows` restituito nello stato [ultimo campione](#view-last-sample-status)), espresso in formato decimale. |
| `code` | Il `code` per lo spazio dei nomi. Questo si può trovare quando si lavora con i namespace utilizzando l’ [API del servizio Adobe Experience Platform Identity](../../identity-service/api/list-namespaces.md) ed è indicato anche come [!UICONTROL Identity symbol] nell’interfaccia utente di Experience Platform. Per ulteriori informazioni, visita la [panoramica dello spazio dei nomi identità](../../identity-service/namespaces.md). |
| `value` | Il valore `id` per lo spazio dei nomi. Questo si può trovare quando si utilizzano i namespace utilizzando l’ [API del servizio Identity](../../identity-service/api/list-namespaces.md). |

## Passaggi successivi

Ora che sai come visualizzare in anteprima i dati di esempio nell’archivio profili, puoi anche utilizzare gli endpoint stimati e visualizzati in anteprima dell’API del servizio di segmentazione per visualizzare informazioni di riepilogo relative alle definizioni dei segmenti. Queste informazioni consentono di isolare il pubblico previsto nel segmento. Per ulteriori informazioni sulle operazioni con le anteprime e le stime dei segmenti utilizzando l&#39;API di segmentazione, visita la [guida all&#39;anteprima e alla stima degli endpoint](../../segmentation/api/previews-and-estimates.md).
