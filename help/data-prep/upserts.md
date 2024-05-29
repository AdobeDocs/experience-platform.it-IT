---
keywords: Experience Platform;home;argomenti popolari;preparazione dati;preparazione dati;streaming;upsert;streaming upsert
title: Inviare Aggiornamenti Parziali Delle Righe A Real-Time Customer Profile Tramite La Preparazione Dei Dati
description: Scopri come inviare aggiornamenti parziali delle righe a Real-Time Customer Profile utilizzando la preparazione dati.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 0%

---

# Invia aggiornamenti riga parziali a [!DNL Real-Time Customer Profile] utilizzo [!DNL Data Prep]

>[!WARNING]
>
>L’acquisizione dei messaggi di aggiornamento entità (con operazioni JSON PATCH) in Experience Data Model (XDM) per gli aggiornamenti del profilo tramite l’ingresso DCS è stata dichiarata obsoleta. In alternativa, puoi: [Inserire dati non elaborati nell&#39;ingresso DCS](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) e specifica le mappature di dati necessarie per trasformare i dati in messaggi conformi a XDM per gli aggiornamenti del profilo.

Upsert in streaming [!DNL Data Prep] consente di inviare aggiornamenti di riga parziali a [!DNL Real-Time Customer Profile] e allo stesso tempo creare e stabilire nuovi collegamenti di identità con una singola richiesta API.

Gli aggiornamenti in streaming consentono di mantenere il formato dei dati durante la traduzione [!DNL Real-Time Customer Profile] Richieste PATCH durante l’acquisizione. In base agli input forniti, [!DNL Data Prep] consente di inviare un singolo payload API e tradurre i dati in entrambi [!DNL Real-Time Customer Profile] PATCH e [!DNL Identity Service] Creare le richieste.

>[!NOTE]
>
>Per sfruttare le funzionalità di upsert, è consigliabile disattivare le configurazioni compatibili con XDM durante l’acquisizione dei dati e mappare nuovamente il payload in ingresso utilizzando [Mapper preparazione dati](./ui/mapping.md).

Questo documento fornisce informazioni su come eseguire lo streaming degli upsert in [!DNL Data Prep].

## Introduzione

Questa panoramica richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): ottieni una visione migliore dei singoli clienti e del loro comportamento collegando le identità tra dispositivi e sistemi.
* [Profilo cliente in tempo reale](../profile/home.md): fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Sorgenti](../sources/home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.

## Utilizzare gli aggiornamenti in streaming in [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Le seguenti sorgenti supportano l’utilizzo di aggiornamenti in streaming:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Flussi di lavoro di alto livello per l&#39;upsert dello streaming

Upsert in streaming [!DNL Data Prep] funziona come segue:

* Devi innanzitutto creare e abilitare un set di dati per [!DNL Profile] consumo. Consulta la guida su [abilitazione di un set di dati per [!DNL Profile]](../catalog/datasets/enable-for-profile.md) per ulteriori informazioni.
* Se devi collegare nuove identità, devi anche creare un set di dati aggiuntivo **con lo stesso schema** come [!DNL Profile] set di dati.
* Una volta preparati i set di dati, devi creare un flusso di dati per mappare la richiesta in ingresso su [!DNL Profile] serie di dati;
* Successivamente, devi aggiornare la richiesta in ingresso per includere le intestazioni necessarie. Queste intestazioni definiscono:
   * L’operazione sui dati da eseguire con [!DNL Profile]: `create`, `merge`, e `delete`.
   * Operazione di identità facoltativa da eseguire con [!DNL Identity Service]: `create`.

### Configurare il set di dati di identità

Se è necessario collegare nuove identità, devi creare e trasmettere un set di dati aggiuntivo nel payload in ingresso. Quando crei un set di dati di identità, devi assicurarti che siano soddisfatti i seguenti requisiti:

* Il set di dati di identità deve avere lo schema associato come [!DNL Profile] set di dati. Una mancata corrispondenza degli schemi può causare un comportamento di sistema incoerente.
* Tuttavia, devi assicurarti che il set di dati di identità sia diverso da [!DNL Profile] set di dati. Se i set di dati sono uguali, i dati verranno sovrascritti anziché aggiornati.
* Mentre il set di dati iniziale deve essere abilitato per [!DNL Profile], il set di dati di identità **non deve essere abilitato** per [!DNL Profile]. In caso contrario, anche i dati verranno sovrascritti anziché aggiornati. Tuttavia, il set di dati di identità **deve essere abilitato** per [!DNL Identity Service].

#### Campi obbligatori negli schemi associati al set di dati di identità {#identity-dataset-required-fileds}

Se lo schema contiene campi obbligatori, la convalida del set di dati deve essere eliminata per abilitare [!DNL Identity Service] per ricevere solo le identità. È possibile sopprimere la convalida applicando la `disabled` valore per `acp_validationContext` parametro. Vedi l’esempio seguente:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags": {
        "acp_validationContext": [
            "disabled"
        ],
        "unifiedProfile": [
            "enabled:false"
        ],
        "unifiedIdentity": [
            "enabled:true"
        ]
    }
}'
```

>[!TIP]
>
>Non è necessario eseguire alcuna configurazione aggiuntiva se lo schema associato al set di dati di identità non dispone di campi obbligatori.

## Struttura del payload in ingresso

Di seguito è riportato un esempio di struttura di payload in ingresso che stabilisce nuovi collegamenti di identità.

### Payload con configurazione identità

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| Parametro | Descrizione |
| --- | --- |
| `flowId` | Un ID univoco per identificare un flusso di dati. Questo ID del flusso di dati deve corrispondere alla connessione sorgente creata con [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], o [!DNL HTTP API]. Questo flusso di dati deve avere anche [!DNL Profile]set di dati abilitato come set di dati di destinazione. **Nota**: ID del [!DNL Profile]Il set di dati di destinazione abilitato viene utilizzato anche come `datasetId` parametro. |
| `imsOrgId` | L’ID che corrisponde alla tua organizzazione. |
| `datasetId` | ID del [!DNL Profile]set di dati di destinazione del flusso di dati abilitato. **Nota**: questo è lo stesso ID del [!DNL Profile]ID del set di dati di destinazione abilitato trovato nel flusso di dati. |
| `operations` | Questo parametro delinea le azioni che [!DNL Data Prep] utilizzerà in base alla richiesta in ingresso. |
| `operations.data` | Definisce le azioni da eseguire in [!DNL Real-Time Customer Profile]. |
| `operations.identity` | Definisce le operazioni consentite sui dati da [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Facoltativo) L’ID del set di dati di identità necessario solo se è necessario collegare nuove identità. |

#### Operazioni supportate

Le seguenti operazioni sono supportate da [!DNL Real-Time Customer Profile]:

| Operazioni | Descrizione |
| --- | --- | 
| `create` | Operazione predefinita. Questo genera un metodo di creazione di entità XDM per [!DNL Real-Time Customer Profile]. |
| `merge` | Viene generato un metodo di aggiornamento dell’entità XDM per [!DNL Real-Time Customer Profile]. |
| `delete` | Viene generato un metodo di eliminazione dell’entità XDM per [!DNL Real-Time Customer Profile] e rimuove definitivamente i dati dal [!DNL Profile store]. |

Le seguenti operazioni sono supportate da [!DNL Identity Service]:

| Operazioni | Descrizioni |
| --- | --- |
| `create` | L’unica operazione consentita per questo parametro. Se `create` viene passato come valore per `operations.identity`, quindi [!DNL Data Prep] genera una richiesta di creazione di entità XDM per [!DNL Identity Service]. Se l’identità esiste già, viene ignorata. **Nota:** Se `operations.identity` è impostato su `create`, quindi `identityDatasetId` è necessario specificare anche. L’entità XDM crea un messaggio generato internamente da [!DNL Data Prep] per questo id set di dati verrà generato un componente. |

### Payload senza configurazione identità

Se non è necessario collegare nuove identità, puoi omettere `identity` e `identityDatasetId` parametri nelle operazioni. In questo modo i dati vengono inviati solo a [!DNL Real-Time Customer Profile] e salta la [!DNL Identity Service]. Per un esempio, consulta il payload seguente:

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## Passaggio dinamico delle identità primarie

Per gli aggiornamenti XDM, lo schema deve essere abilitato per [!DNL Profile] e contengono un’identità primaria. Puoi specificare l’identità primaria di uno schema XDM in due modi:

* Designa un campo statico come identità primaria nello schema XDM;
* Designa uno dei campi di identità come identità principale tramite il gruppo di campi della mappa di identità nello schema XDM.

### Designare un campo statico come campo di identità principale nello schema XDM

Nell’esempio seguente, `state`, `homePhone.number` e gli altri attributi vengono inseriti con i rispettivi valori specificati nel [!DNL Profile] con l’identità primaria di `sampleEmail@gmail.com`. Il messaggio di aggiornamento di un’entità XDM viene quindi generato dal flusso [!DNL Data Prep] componente. [!DNL Real-Time Customer Profile] quindi conferma che il messaggio di aggiornamento XDM esegue l’upsert del record del profilo.

>[!NOTE]
>
>In questo esempio, le identità non verranno collegate tra loro poiché non sono definite operazioni per l’identità.

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### Designa uno dei campi di identità come identità principale tramite il gruppo di campi della mappa di identità nello schema XDM

In questo esempio, l’intestazione contiene `operations` attributo con `identity` e `identityDatasetId` proprietà. Questo consente di unire i dati con [!DNL Real-Time Customer Profile] e anche per le identità da trasmettere a [!DNL Identity Service].

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## Limitazioni note e considerazioni chiave

Di seguito è riportato un elenco delle limitazioni note da considerare quando si esegue lo streaming degli aggiornamenti con [!DNL Data Prep]:

* Il metodo di streaming upserts deve essere utilizzato solo quando si inviano aggiornamenti parziali delle righe a [!DNL Real-Time Customer Profile]. Gli aggiornamenti parziali delle righe sono **non** consumato dal data lake.
* Il metodo degli aggiornamenti in streaming non supporta l’aggiornamento, la sostituzione e la rimozione di identità. Se non esistono, vengono create nuove identità. Da qui la `identity` L&#39;operazione deve essere sempre impostata su create. Se esiste già un’identità, l’operazione è no-op.
* Il metodo di streaming upserts attualmente non supporta [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) e [SDK di Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/documentation/).

## Passaggi successivi

Una volta letto questo documento, sarai in grado di eseguire lo streaming degli upsert in [!DNL Data Prep] per inviare aggiornamenti di riga parziali al [!DNL Real-Time Customer Profile] e di creare e collegare le identità con una singola richiesta API. Per ulteriori informazioni su altri [!DNL Data Prep] , leggi le [[!DNL Data Prep] panoramica](./home.md). Per informazioni su come utilizzare i set di mappatura all&#39;interno di [!DNL Data Prep] API, leggi le [[!DNL Data Prep] guida per sviluppatori](./api/overview.md).
