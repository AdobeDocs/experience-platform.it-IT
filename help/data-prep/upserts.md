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

# Invia aggiornamenti riga parziali a [!DNL Real-Time Customer Profile] tramite [!DNL Data Prep]

>[!WARNING]
>
>L’acquisizione dei messaggi di aggiornamento entità (con operazioni JSON PATCH) in Experience Data Model (XDM) per gli aggiornamenti del profilo tramite l’ingresso DCS è stata dichiarata obsoleta. In alternativa, puoi [acquisire dati non elaborati nell&#39;ingresso DCS](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) e specificare le mappature di dati necessarie per trasformare i dati in messaggi conformi a XDM per gli aggiornamenti del profilo.

Gli upsert di streaming in [!DNL Data Prep] consentono di inviare aggiornamenti di riga parziali ai dati [!DNL Real-Time Customer Profile], creando e stabilendo nuovi collegamenti di identità con una singola richiesta API.

Con gli aggiornamenti in streaming, è possibile mantenere il formato dei dati durante la traduzione in [!DNL Real-Time Customer Profile] richieste PATCH durante l&#39;acquisizione. In base agli input forniti, [!DNL Data Prep] ti consente di inviare un singolo payload API e tradurre i dati sia alle richieste [!DNL Real-Time Customer Profile] PATCH che a quelle [!DNL Identity Service] CREATE.

>[!NOTE]
>
>Per sfruttare le funzionalità di upsert, è consigliabile disattivare le configurazioni compatibili con XDM durante l&#39;acquisizione dei dati e mappare nuovamente il payload in ingresso utilizzando [Data Prep Mapper](./ui/mapping.md).

In questo documento vengono fornite informazioni su come eseguire lo streaming degli upsert in [!DNL Data Prep].

## Introduzione

Questa panoramica richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): Ottieni una migliore visualizzazione dei singoli clienti e del loro comportamento collegando le identità tra dispositivi e sistemi.
* [Profilo cliente in tempo reale](../profile/home.md): fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Origini](../sources/home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.

## Usa gli aggiornamenti in streaming in [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Le seguenti sorgenti supportano l’utilizzo di aggiornamenti in streaming:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Flussi di lavoro di alto livello per l&#39;upsert dello streaming

Gli upsert di streaming in [!DNL Data Prep] funzionano come segue:

* È innanzitutto necessario creare e abilitare un set di dati per l&#39;utilizzo di [!DNL Profile]. Per ulteriori informazioni, consulta la guida su [abilitazione di un set di dati per [!DNL Profile]](../catalog/datasets/enable-for-profile.md).
* Se le nuove identità devono essere collegate, è necessario creare anche un set di dati aggiuntivo **con lo stesso schema** del set di dati [!DNL Profile].
* Una volta preparati i set di dati, è necessario creare un flusso di dati per mappare la richiesta in ingresso al set di dati [!DNL Profile];
* Successivamente, devi aggiornare la richiesta in ingresso per includere le intestazioni necessarie. Queste intestazioni definiscono:
   * Operazione sui dati da eseguire con [!DNL Profile]: `create`, `merge` e `delete`.
   * Operazione di identità facoltativa da eseguire con [!DNL Identity Service]: `create`.

### Configurare il set di dati di identità

Se è necessario collegare nuove identità, devi creare e trasmettere un set di dati aggiuntivo nel payload in ingresso. Quando crei un set di dati di identità, devi assicurarti che siano soddisfatti i seguenti requisiti:

* Il set di dati di identità deve avere lo schema associato come set di dati [!DNL Profile]. Una mancata corrispondenza degli schemi può causare un comportamento di sistema incoerente.
* Tuttavia, è necessario assicurarsi che il set di dati di identità sia diverso dal set di dati [!DNL Profile]. Se i set di dati sono uguali, i dati verranno sovrascritti anziché aggiornati.
* Il set di dati iniziale deve essere abilitato per [!DNL Profile], ma il set di dati di identità **non deve essere abilitato** per [!DNL Profile]. In caso contrario, anche i dati verranno sovrascritti anziché aggiornati. Tuttavia, il set di dati di identità **deve essere abilitato** per [!DNL Identity Service].

#### Campi obbligatori negli schemi associati al set di dati di identità {#identity-dataset-required-fileds}

Se lo schema contiene campi obbligatori, è necessario eliminare la convalida del set di dati per consentire a [!DNL Identity Service] di ricevere solo le identità. È possibile eliminare la convalida applicando il valore `disabled` al parametro `acp_validationContext`. Vedi l’esempio seguente:

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
| `flowId` | Un ID univoco per identificare un flusso di dati. Questo ID del flusso di dati deve corrispondere alla connessione di origine creata con [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] o [!DNL HTTP API]. Questo flusso di dati deve avere anche un set di dati abilitato per [!DNL Profile] come set di dati di destinazione. **Nota**: l&#39;ID del set di dati di destinazione abilitato per [!DNL Profile] viene utilizzato anche come parametro `datasetId`. |
| `imsOrgId` | L’ID che corrisponde alla tua organizzazione. |
| `datasetId` | ID del set di dati di destinazione abilitato per [!DNL Profile] del flusso di dati. **Nota**: è lo stesso ID del set di dati di destinazione abilitato per [!DNL Profile] trovato nel flusso di dati. |
| `operations` | Questo parametro delinea le azioni che [!DNL Data Prep] intraprenderà in base alla richiesta in ingresso. |
| `operations.data` | Definisce le azioni da eseguire in [!DNL Real-Time Customer Profile]. |
| `operations.identity` | Definisce le operazioni consentite sui dati da [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Facoltativo) L’ID del set di dati di identità necessario solo se è necessario collegare nuove identità. |

#### Operazioni supportate

Le operazioni seguenti sono supportate da [!DNL Real-Time Customer Profile]:

| Operazioni | Descrizione |
| --- | --- | 
| `create` | Operazione predefinita. Viene generato un metodo di creazione di entità XDM per [!DNL Real-Time Customer Profile]. |
| `merge` | Viene generato un metodo di aggiornamento entità XDM per [!DNL Real-Time Customer Profile]. |
| `delete` | Viene generato un metodo di eliminazione dell&#39;entità XDM per [!DNL Real-Time Customer Profile] e vengono rimossi definitivamente i dati da [!DNL Profile store]. |

Le operazioni seguenti sono supportate da [!DNL Identity Service]:

| Operazioni | Descrizioni |
| --- | --- |
| `create` | L’unica operazione consentita per questo parametro. Se `create` viene passato come valore per `operations.identity`, [!DNL Data Prep] genera una richiesta di creazione di entità XDM per [!DNL Identity Service]. Se l’identità esiste già, viene ignorata. **Nota:** Se `operations.identity` è impostato su `create`, è necessario specificare anche `identityDatasetId`. Per questo ID di set di dati verrà generato il messaggio di creazione dell&#39;entità XDM generato internamente dal componente [!DNL Data Prep]. |

### Payload senza configurazione identità

Se non è necessario collegare nuove identità, è possibile omettere i parametri `identity` e `identityDatasetId` nelle operazioni. In questo modo i dati vengono inviati solo a [!DNL Real-Time Customer Profile] e il [!DNL Identity Service] viene ignorato. Per un esempio, consulta il payload seguente:

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

Per gli aggiornamenti XDM, lo schema deve essere abilitato per [!DNL Profile] e contenere un&#39;identità primaria. Puoi specificare l’identità primaria di uno schema XDM in due modi:

* Designa un campo statico come identità primaria nello schema XDM;
* Designa uno dei campi di identità come identità principale tramite il gruppo di campi della mappa di identità nello schema XDM.

### Designare un campo statico come campo di identità principale nello schema XDM

Nell&#39;esempio seguente, `state`, `homePhone.number` e altri attributi vengono inseriti con i rispettivi valori specificati in [!DNL Profile] con l&#39;identità primaria di `sampleEmail@gmail.com`. Un messaggio di aggiornamento dell&#39;entità XDM viene quindi generato dal componente di streaming [!DNL Data Prep]. [!DNL Real-Time Customer Profile] conferma quindi che il messaggio di aggiornamento XDM esegue l&#39;upsert del record del profilo.

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

In questo esempio, l&#39;intestazione contiene l&#39;attributo `operations` con le proprietà `identity` e `identityDatasetId`. Ciò consente l&#39;unione dei dati con [!DNL Real-Time Customer Profile] e la trasmissione delle identità a [!DNL Identity Service].

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

Di seguito è riportato un elenco delle limitazioni note da considerare quando si esegue l&#39;upsert dello streaming con [!DNL Data Prep]:

* Utilizzare il metodo Streaming Upserts solo per l&#39;invio di aggiornamenti di riga parziali a [!DNL Real-Time Customer Profile]. Aggiornamenti riga parziali: **non** utilizzati dal data lake.
* Il metodo degli aggiornamenti in streaming non supporta l’aggiornamento, la sostituzione e la rimozione di identità. Se non esistono, vengono create nuove identità. Pertanto, l&#39;operazione `identity` deve essere sempre impostata per la creazione. Se esiste già un’identità, l’operazione è no-op.
* Il metodo di upsert streaming attualmente non supporta [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) e [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/).

## Passaggi successivi

Dopo aver letto questo documento, sarai in grado di eseguire il flusso degli aggiornamenti a monte in [!DNL Data Prep] per inviare aggiornamenti di riga parziali ai tuoi dati di [!DNL Real-Time Customer Profile], nonché di creare e collegare identità con una singola richiesta API. Per ulteriori informazioni sulle altre funzionalità di [!DNL Data Prep], leggere la [[!DNL Data Prep] panoramica](./home.md). Per informazioni su come utilizzare i set di mappatura nell&#39;API [!DNL Data Prep], leggere la [[!DNL Data Prep] guida per gli sviluppatori](./api/overview.md).
