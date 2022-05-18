---
keywords: Experience Platform;home;argomenti popolari;preparazione dati;preparazione dati;streaming;upsert;streaming upsert
title: Inviare Aggiornamenti Parziali Alle Righe Al Servizio Profilo Utilizzando Data Prep
description: Questo documento fornisce informazioni su come inviare aggiornamenti parziali delle righe al Servizio profili utilizzando Data Prep.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: 67049cf220379bfa5b64f530f26045ea21077be0
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# Invia aggiornamenti parziali a [!DNL Profile Service] utilizzo [!DNL Data Prep]

Streaming degli upsers in [!DNL Data Prep] consente di inviare aggiornamenti parziali delle righe a [!DNL Profile Service] durante la creazione e la creazione di nuovi collegamenti di identità con una singola richiesta API.

Gli inserzionisti in streaming possono conservare il formato dei dati mentre li traducono in [!DNL Profile Service] Richieste PATCH durante l’acquisizione. In base agli input forniti, [!DNL Data Prep] consente di inviare un singolo payload API e di tradurre i dati in entrambi [!DNL Profile Service] PATCH e [!DNL Identity Service] CREARE richieste.

Questo documento fornisce informazioni su come eseguire lo streaming degli upsers in [!DNL Data Prep].

## Introduzione

Questa panoramica richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): Ottieni una visione migliore dei singoli clienti e del loro comportamento attraverso il collegamento delle identità tra dispositivi e sistemi.
* [Profilo cliente in tempo reale](../profile/home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Origini](../sources/home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.

## Utilizzare gli upsers in streaming in [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Le seguenti sorgenti supportano l&#39;uso di upserts in streaming:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Lo streaming aumenta il flusso di lavoro di alto livello

Streaming degli upsers in [!DNL Data Prep] funziona come segue:

* È innanzitutto necessario creare e abilitare un set di dati per [!DNL Profile] consumo. Consulta la guida su [abilitazione di un set di dati per [!DNL Profile]](../catalog/datasets/enable-for-profile.md) per ulteriori informazioni;
* Se è necessario collegare nuove identità, è necessario creare anche un set di dati aggiuntivo **con lo stesso schema** come [!DNL Profile] set di dati;
* Una volta preparati i set di dati, devi creare un flusso di dati per mappare la richiesta in arrivo al [!DNL Profile] set di dati;
* Successivamente, devi aggiornare la richiesta in arrivo per includere le intestazioni necessarie. Queste intestazioni definiscono:
   * Operazione di dati con cui eseguire [!DNL Profile]: `create`, `merge`e `delete`;
   * Operazione di identità opzionale da eseguire con [!DNL Identity Service]: `create`.

### Configurare il set di dati di identità

Se è necessario collegare nuove identità, è necessario creare e trasmettere un set di dati aggiuntivo nel payload in arrivo. Quando crei un set di dati di identità, devi accertarti che siano soddisfatti i seguenti requisiti:

* Il set di dati di identità deve avere il proprio schema associato come [!DNL Profile] set di dati. Una mancata corrispondenza degli schemi può comportare un comportamento incoerente del sistema;
* Tuttavia, devi assicurarti che il set di dati di identità sia diverso dal [!DNL Profile] set di dati. Se i set di dati sono gli stessi, i dati verranno sovrascritti anziché aggiornati;
* Mentre il set di dati iniziale deve essere abilitato per [!DNL Profile], il set di dati di identità **non** è abilitato per [!DNL Profile]. In caso contrario, anche i dati verranno sovrascritti anziché aggiornati.

#### Campi obbligatori negli schemi associati al set di dati di identità {#identity-dataset-required-fileds}

Se lo schema contiene campi obbligatori, la convalida del set di dati deve essere eliminata per abilitare [!DNL Identity Service] per ricevere solo le identità. È possibile eliminare la convalida applicando il `disabled` al `acp_validationContext` parametro . Vedi l&#39;esempio seguente:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags":{
        "acp_validationContext": ["disabled"]
        }
}'
```

>[!TIP]
>
>Non è necessario eseguire alcuna configurazione aggiuntiva se lo schema associato al set di dati di identità non contiene campi obbligatori.

## Struttura del payload in entrata

Nell&#39;esempio seguente viene visualizzato un esempio di struttura del payload in entrata che stabilisce nuovi collegamenti di identità.

### Payload con configurazione dell&#39;identità

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
| `flowId` | Un ID univoco per identificare un flusso di dati. L&#39;ID del flusso di dati deve corrispondere alla connessione sorgente creata con [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]oppure [!DNL HTTP API]. Questo flusso di dati dovrebbe anche avere [!DNL Profile]Set di dati abilitato come set di dati di destinazione. **Nota**: ID del [!DNL Profile]Il set di dati di destinazione abilitato viene utilizzato anche come `datasetId` parametro . |
| `imsOrgId` | L&#39;ID che corrisponde alla tua organizzazione. |
| `datasetId` | ID del [!DNL Profile]Set di dati di destinazione abilitato del flusso di dati. **Nota**: Questo è lo stesso ID del [!DNL Profile]ID set di dati di destinazione abilitato trovato nel flusso di dati. |
| `operations` | Questo parametro delinea le azioni che [!DNL Data Prep] in base alla richiesta in arrivo. |
| `operations.data` | Definisce le azioni da eseguire in [!DNL Profile Service]. |
| `operations.identity` | Definisce le operazioni consentite sui dati da [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Facoltativo) L&#39;ID del set di dati di identità richiesto solo se è necessario collegare nuove identità. |

#### Operazioni supportate

Le seguenti operazioni sono supportate da [!DNL Profile Service]:

| Operazioni | Descrizione |
| --- | --- | 
| `create` | Operazione predefinita. Viene generato un metodo di creazione entità XDM per [!DNL Profile Service]. |
| `merge` | Viene generato un metodo di aggiornamento entità XDM per [!DNL Profile Service]. |
| `delete` | Viene generato un metodo di eliminazione delle entità XDM per [!DNL Profile Service] e rimuove definitivamente i dati dal [!DNL Profile Store]. |

Le seguenti operazioni sono supportate da [!DNL Identity Service]:

| Operazioni | Descrizioni |
| --- | --- |
| `create` | L&#39;unica operazione consentita per questo parametro. Se `create` viene passato come valore per `operations.identity`, quindi [!DNL Data Prep] genera una richiesta di creazione di entità XDM per [!DNL Identity Service]. Se l&#39;identità esiste già, l&#39;identità viene ignorata. **Nota:** Se `operations.identity` è impostato su `create`, quindi `identityDatasetId` deve essere specificato anche. L’entità XDM crea il messaggio generato internamente da [!DNL Data Prep] verrà generato per questo ID set di dati. |

### Payload senza configurazione dell&#39;identità

Se non è necessario collegare nuove identità, puoi omettere la `identity` e `identityDatasetId` nelle operazioni. In questo modo i dati vengono inviati solo a [!DNL Profile Service] e salta la [!DNL Identity Service]. Per un esempio, consulta il payload seguente:

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

## Trasmettere dinamicamente le identità primarie

Per gli aggiornamenti XDM, lo schema deve essere abilitato per [!DNL Profile] e contengono un&#39;identità primaria. È possibile specificare l&#39;identità principale di uno schema XDM in due modi:

* designare un campo statico come identità principale nello schema XDM;
* Designa uno dei campi di identità come identità principale tramite il gruppo di campi mappa identità nello schema XDM.

### Designare un campo statico come campo di identità principale nello schema XDM

Nell’esempio seguente: `state`, `homePhone.number` e altri attributi sono utilizzati con i rispettivi valori specificati nel [!DNL Profile] con l&#39;identità principale di `sampleEmail@gmail.com`. Un messaggio di aggiornamento entità XDM viene quindi generato dal flusso [!DNL Data Prep] componente. [!DNL Profile Service] quindi conferma che XDM aggiorna il messaggio per aggiornare il record del profilo.

>[!NOTE]
>
>In questo esempio, le identità non verranno collegate tra loro in quanto non sono definite operazioni per l&#39;identità.

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

### Designare uno dei campi di identità come identità principale tramite il gruppo di campi mappa identità nello schema XDM

In questo esempio, l’intestazione contiene `operations` con l&#39;attributo `identity` e `identityDatasetId` proprietà. Ciò consente l’unione dei dati con [!DNL Profile Service] e anche per le identità da trasmettere a [!DNL Identity Service].

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

Di seguito è riportato un elenco delle limitazioni note da considerare durante lo streaming degli upsers con [!DNL Data Prep]:

* Il metodo upserts in streaming deve essere utilizzato solo quando si inviano aggiornamenti di riga parziali a [!DNL Profile Service]. Gli aggiornamenti parziali delle righe sono **not** consumato da data lake.
* Il metodo upserts in streaming non supporta l’aggiornamento, la sostituzione e la rimozione delle identità. Le identità possono essere aggiunte solo utilizzando `identity: create` funzionamento.
* Il metodo upserts in streaming supporta attualmente solo attributi e oggetti con valore singolo primitivo (come numeri interi, date, marche temporali e stringhe). Il metodo upserts in streaming non supporta la sostituzione, l’aggiunta o la sovrascrittura di attributi di array e indici di array specifici.

## Passaggi successivi

Leggendo questo documento, è ora necessario comprendere come eseguire lo streaming degli upsers in [!DNL Data Prep] per inviare aggiornamenti parziali alle righe [!DNL Profile Service] , creando e collegando identità con una singola richiesta API. Per ulteriori informazioni su altri [!DNL Data Prep] funzionalità, leggere [[!DNL Data Prep] panoramica](./home.md). Per scoprire come utilizzare i set di mappatura all’interno di [!DNL Data Prep] API, leggi [[!DNL Data Prep] guida per sviluppatori](./api/overview.md).
