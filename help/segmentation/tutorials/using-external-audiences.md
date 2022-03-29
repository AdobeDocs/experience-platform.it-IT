---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Importazione e utilizzo di tipi di pubblico esterni
description: Segui questa esercitazione per scoprire come utilizzare i tipi di pubblico esterni con Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 077622e891f4c42ce283e2553d6a2983569d3584
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# Importazione e utilizzo di tipi di pubblico esterni

Adobe Experience Platform supporta la possibilità di importare tipi di pubblico esterni, che possono essere successivamente utilizzati come componenti per una nuova definizione di segmento. Questo documento fornisce un’esercitazione per configurare Experience Platform per importare e utilizzare tipi di pubblico esterni.

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei vari [!DNL Adobe Experience Platform] servizi coinvolti nella creazione di segmenti di pubblico. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Servizio di segmentazione](../home.md): Consente di creare segmenti di pubblico dai dati Profilo cliente in tempo reale.
- [Profilo cliente in tempo reale](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience. Per utilizzare al meglio la segmentazione, assicurati che i tuoi dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).
- [Set di dati](../../catalog/datasets/overview.md): Il costrutto di archiviazione e gestione per la persistenza dei dati in Experience Platform.
- [Acquisizione in streaming](../../ingestion/streaming-ingestion/overview.md): In che modo Experience Platform acquisisce e memorizza in tempo reale i dati da dispositivi lato client e lato server.

### Dati del segmento e metadati del segmento

Prima di iniziare a importare e utilizzare tipi di pubblico esterni, è importante comprendere la differenza tra i dati dei segmenti e i metadati dei segmenti.

I dati dei segmenti si riferiscono ai profili che soddisfano i criteri di qualificazione dei segmenti e quindi fanno parte del pubblico.

I metadati del segmento sono informazioni sul segmento stesso, che includono nome, descrizione, espressione (se applicabile), data di creazione, data dell’ultima modifica e un ID. L’ID collega i metadati del segmento ai singoli profili che soddisfano la qualifica del segmento e fanno parte del pubblico risultante.

| Dati del segmento | Metadati del segmento |
| ------------ | ---------------- |
| Profili che soddisfano la qualifica dei segmenti | Informazioni sul segmento stesso |

## Creare uno spazio dei nomi di identità per il pubblico esterno

Il primo passaggio per l’utilizzo di tipi di pubblico esterni consiste nella creazione di uno spazio dei nomi di identità. I namespace di identità consentono a Platform di associare la posizione di origine di un segmento.

Per creare uno spazio dei nomi di identità, segui le istruzioni contenute in [guida allo spazio dei nomi identità](../../identity-service/namespaces.md#manage-namespaces). Durante la creazione dello spazio dei nomi di identità, aggiungi i dettagli di origine allo spazio dei nomi di identità e contrassegnali [!UICONTROL Tipo] come **[!UICONTROL Identificatore non personale]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

>[!NOTE]
>
>Per iniziare a utilizzare namespace personalizzati con tipi di pubblico esterni, dovrai creare un ticket di supporto. Per ulteriori informazioni, contatta il tuo rappresentante Adobe.

## Creare uno schema per i metadati del segmento

Dopo aver creato uno spazio dei nomi di identità, devi creare un nuovo schema per il segmento che creerai.

Per iniziare a comporre uno schema, seleziona prima **[!UICONTROL Schemi]** sulla barra di navigazione a sinistra, seguita dalla **[!UICONTROL Creare uno schema]** nell’angolo in alto a destra dell’area di lavoro Schemi. Da qui, seleziona **[!UICONTROL Sfoglia]** per visualizzare una selezione completa dei tipi di schema disponibili.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Poiché stai creando una definizione di segmento, che è una classe predefinita, seleziona **[!UICONTROL Usa classe esistente]**. Ora, seleziona la **[!UICONTROL Definizione del segmento]** classe, seguita da **[!UICONTROL Assegna classe]**.

![](../images/tutorials/external-audiences/assign-class.png)

Dopo la creazione dello schema, dovrai specificare quale campo conterrà l’ID del segmento. Questo campo deve essere contrassegnato come identità principale e assegnato agli spazi dei nomi creati in precedenza.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Dopo la marcatura `_id` come identità principale, seleziona il titolo dello schema, seguito dall’interruttore etichettato **[!UICONTROL Profilo]**. Seleziona **[!UICONTROL Abilita]** per abilitare lo schema per [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Ora, questo schema è abilitato per Profilo, con l’identificazione principale assegnata allo spazio dei nomi dell’identità non persona creato. Di conseguenza, i metadati del segmento importati in Platform utilizzando questo schema verranno acquisiti in Profilo senza essere uniti ad altri dati di profilo relativi alle persone.

## Creare un set di dati per lo schema

Dopo aver configurato lo schema, dovrai creare un set di dati per i metadati del segmento.

Per creare un set di dati, segui le istruzioni nella sezione [guida utente del set di dati](../../catalog/datasets/user-guide.md#create). Dovresti seguire la **[!UICONTROL Creare un set di dati dallo schema]** utilizzando lo schema creato in precedenza.

![](../images/tutorials/external-audiences/select-schema.png)

Dopo aver creato il set di dati, continua a seguire le istruzioni in [guida utente del set di dati](../../catalog/datasets/user-guide.md#enable-profile) per abilitare questo set di dati per il profilo cliente in tempo reale.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configurazione e importazione di dati sul pubblico

Con il set di dati abilitato, i dati possono ora essere inviati in Platform tramite l’interfaccia utente o utilizzando le API di Experience Platform. Puoi acquisire questi dati tramite una connessione batch o in streaming.

### Inserire dati utilizzando una connessione batch

Per creare una connessione batch, è possibile seguire le istruzioni contenute nel modello generico [guida all’interfaccia utente per il caricamento locale dei file](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Per un elenco completo delle sorgenti disponibili con cui è possibile utilizzare i dati di acquisizione, consulta la sezione [panoramica di origini](../../sources/home.md).

### Inserire dati tramite una connessione in streaming

Per creare una connessione in streaming, puoi seguire le istruzioni contenute in [Esercitazione API](../../sources/tutorials/api/create/streaming/http.md) o [Esercitazione sull’interfaccia utente](../../sources/tutorials/ui/create/streaming/http.md).

Una volta creata la connessione streaming, avrai accesso all&#39;endpoint streaming univoco a cui puoi inviare i tuoi dati. Per informazioni su come inviare dati a questi endpoint, consulta la sezione [esercitazione sullo streaming dei dati di record](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Struttura dei metadati del pubblico

Dopo aver creato una connessione, ora puoi inserire i dati in Platform.

Di seguito è riportato un esempio dei metadati del payload per il pubblico esterno:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{SEGMENT_ID}",
            "description": "Sample description",
            "identityMap": {
                "{IDENTITY_NAMESPACE}": [{
                    "id": "{}"
                }]
            },
            "segmentName" : "{SEGMENT_NAME}",
            "segmentStatus": "ACTIVE",
            "version": "1.0"
        }
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `schemaRef` | Lo schema **deve** fai riferimento allo schema creato in precedenza per i metadati del segmento. |
| `datasetId` | ID set di dati **deve** fai riferimento al set di dati creato in precedenza per lo schema appena creato. |
| `xdmEntity._id` | ID **deve** fai riferimento allo stesso ID segmento utilizzato come pubblico esterno. |
| `xdmEntity.identityMap` | Questa sezione **deve** contiene l’etichetta di identità utilizzata per creare lo spazio dei nomi creato in precedenza. |
| `{IDENTITY_NAMESPACE}` | Etichetta dello spazio dei nomi di identità creato in precedenza. Ad esempio, se hai chiamato il namespace Identity &quot;externalAudience&quot;, lo utilizzerai come chiave dell’array. |
| `segmentName` | Nome del segmento per il quale desideri segmentare il pubblico esterno. |

## Creazione di segmenti utilizzando i tipi di pubblico importati

Una volta configurati i tipi di pubblico importati, possono essere utilizzati come parte del processo di segmentazione. Per trovare tipi di pubblico esterni, vai al Generatore di segmenti e seleziona **[!UICONTROL Tipi di pubblico]** nella scheda **[!UICONTROL Campi]** sezione .

![](../images/tutorials/external-audiences/external-audiences.png)

## Passaggi successivi

Ora che puoi utilizzare tipi di pubblico esterni nei segmenti, puoi utilizzare il Generatore di segmenti per creare segmenti. Per scoprire come creare i segmenti, leggi la sezione [esercitazione sulla creazione di segmenti](./create-a-segment.md).

## Appendice

Oltre a utilizzare i metadati del pubblico esterno importati e utilizzarli per creare segmenti, puoi anche importare appartenenze di segmenti esterne in Platform.

### Configurare uno schema di destinazione di appartenenza a un segmento esterno

Per iniziare a comporre uno schema, seleziona prima **[!UICONTROL Schemi]** sulla barra di navigazione a sinistra, seguita dalla **[!UICONTROL Creare uno schema]** nell’angolo in alto a destra dell’area di lavoro Schemi. Da qui, seleziona **[!UICONTROL Profilo individuale XDM]**.

![](../images/tutorials/external-audiences/create-schema-profile.png)

Una volta creato lo schema, è necessario aggiungere il gruppo di campi di appartenenza al segmento come parte dello schema. A questo scopo, seleziona [!UICONTROL Dettagli di appartenenza al segmento], seguita da [!UICONTROL Aggiungi gruppi di campi].

![](../images/tutorials/external-audiences/segment-membership-details.png)

Inoltre, assicurati che lo schema sia contrassegnato per **[!UICONTROL Profilo]**. A questo scopo, è necessario contrassegnare un campo come identità principale.

![](../images/tutorials/external-audiences/external-segment-profile.png)

### Imposta il set di dati

Dopo aver creato lo schema, dovrai creare un set di dati.

Per creare un set di dati, segui le istruzioni nella sezione [guida utente del set di dati](../../catalog/datasets/user-guide.md#create). Dovresti seguire la **[!UICONTROL Creare un set di dati dallo schema]** utilizzando lo schema creato in precedenza.

![](../images/tutorials/external-audiences/select-schema.png)

Dopo aver creato il set di dati, continua a seguire le istruzioni in [guida utente del set di dati](../../catalog/datasets/user-guide.md#enable-profile) per abilitare questo set di dati per il profilo cliente in tempo reale.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configurazione e importazione di dati di appartenenza a un pubblico esterno

Con il set di dati abilitato, i dati possono ora essere inviati in Platform tramite l’interfaccia utente o utilizzando le API di Experience Platform. Puoi acquisire questi dati tramite una connessione batch o in streaming.

### Inserire dati utilizzando una connessione batch

Per creare una connessione batch, è possibile seguire le istruzioni contenute nel modello generico [guida all’interfaccia utente per il caricamento locale dei file](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Per un elenco completo delle sorgenti disponibili con cui è possibile utilizzare i dati di acquisizione, consulta la sezione [panoramica di origini](../../sources/home.md).

### Inserire dati tramite una connessione in streaming

Per creare una connessione in streaming, puoi seguire le istruzioni contenute in [Esercitazione API](../../sources/tutorials/api/create/streaming/http.md) o [Esercitazione sull’interfaccia utente](../../sources/tutorials/ui/create/streaming/http.md).

Una volta creata la connessione streaming, avrai accesso all&#39;endpoint streaming univoco a cui puoi inviare i tuoi dati. Per informazioni su come inviare dati a questi endpoint, consulta la sezione [esercitazione sullo streaming dei dati di record](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Struttura di appartenenza al segmento

Dopo aver creato una connessione, ora puoi inserire i dati in Platform.

Di seguito è riportato un esempio del payload per l’appartenenza all’audience esterna:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience Membership"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{UNIQUE_ID}",
            "description": "Sample description",
            "{TENANT_NAME}": {
                "identities": {
                    "{SCHEMA_IDENTITY}": "sample-id"
                }
            },
            "personId" : "sample-name",
            "segmentMembership": {
                "{IDENTITY_NAMESPACE}": {
                    "{EXTERNAL_IDENTITY}": {
                        "status": "realized",
                        "lastQualificationTime": "2022-03-14T:00:00:00Z"
                    }
                }
            }
        }
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `schemaRef` | Lo schema **deve** fare riferimento allo schema creato in precedenza per i dati di appartenenza al segmento. |
| `datasetId` | ID set di dati **deve** fare riferimento al set di dati creato in precedenza per lo schema di appartenenza appena creato. |
| `xdmEntity._id` | Un ID adatto utilizzato per identificare in modo univoco il record all’interno del set di dati. |
| `{TENANT_NAME}.identities` | Questa sezione viene utilizzata per collegare il gruppo di campi delle identità personalizzate con gli utenti precedentemente importati. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | Etichetta dello spazio dei nomi di identità personalizzato creato in precedenza. Ad esempio, se hai chiamato il namespace Identity &quot;externalAudience&quot;, lo utilizzerai come chiave dell’array. |