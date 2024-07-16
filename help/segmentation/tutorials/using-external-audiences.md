---
solution: Experience Platform
title: Importazione e utilizzo di tipi di pubblico esterni
description: Segui questo tutorial per scoprire come utilizzare i tipi di pubblico esterni con Adobe Experience Platform.
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
hide: true
hidefromtoc: true
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 0%

---

# Importazione e utilizzo di tipi di pubblico esterni

>[!IMPORTANT]
>
>Questa documentazione contiene informazioni provenienti da una versione precedente della documentazione di Audiences e, di conseguenza, è obsoleta.

Adobe Experience Platform supporta la possibilità di importare tipi di pubblico esterni, che possono essere successivamente utilizzati come componenti per un nuovo pubblico. Questo documento fornisce un tutorial per configurare Experience Platform per importare e utilizzare tipi di pubblico esterni.

## Introduzione

Questo tutorial richiede una buona conoscenza dei vari servizi [!DNL Adobe Experience Platform] coinvolti nella creazione di tipi di pubblico. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [Servizio di segmentazione](../home.md): consente di creare tipi di pubblico dai dati del profilo cliente in tempo reale.
- [Profilo cliente in tempo reale](../../profile/home.md): fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [Experience Data Model (XDM)](../../xdm/home.md): framework standardizzato in base al quale Platform organizza i dati sull&#39;esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alle [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).
- [Set di dati](../../catalog/datasets/overview.md): il costrutto di archiviazione e gestione per la persistenza dei dati in Experience Platform.
- [Acquisizione in streaming](../../ingestion/streaming-ingestion/overview.md): in che modo Experience Platform acquisisce e memorizza in tempo reale i dati da dispositivi lato client e lato server.

### Tipi di pubblico e definizioni dei segmenti

Prima di iniziare a importare e utilizzare tipi di pubblico esterni, è importante comprendere la differenza tra i tipi di pubblico e le definizioni dei segmenti.

I tipi di pubblico si riferiscono al gruppo di profili a cui stai tentando di filtrare. Quando utilizzi le definizioni dei segmenti, puoi creare un pubblico creando una definizione di segmento che filtra i profili al sottoinsieme che soddisfa i criteri di qualificazione dei segmenti.

Le definizioni dei segmenti includono informazioni quali il nome, la descrizione, l’espressione (se applicabile), la data di creazione, la data dell’ultima modifica e un ID. L’ID collega i metadati del segmento ai singoli profili che soddisfano la qualifica del segmento e che fanno parte del pubblico risultante.

| Tipi di pubblico | Definizione del segmento |
| --------- | ---------------- |
| Il gruppo di profili che stai tentando di trovare. Quando si utilizzano le definizioni dei segmenti, ciò significa che sarà il gruppo di profili che soddisfa la qualifica del segmento. | Il gruppo di regole utilizzato per segmentare il pubblico che stai cercando. |

## Creare uno spazio dei nomi delle identità per il pubblico esterno

Il primo passaggio per utilizzare tipi di pubblico esterni consiste nella creazione di uno spazio dei nomi delle identità. Gli spazi dei nomi di identità consentono a Platform di associarsi da dove proviene un pubblico.

Per creare uno spazio dei nomi di identità, segui le istruzioni riportate nella [guida dello spazio dei nomi di identità](../../identity-service/features/namespaces.md#manage-namespaces). Durante la creazione del namespace Identity, aggiungi i dettagli di origine allo spazio dei nomi Identity e contrassegna il relativo [!UICONTROL Tipo] come **[!UICONTROL Identificatore non persone]**.

![L&#39;identificatore non persona è evidenziato nella finestra modale Crea spazio dei nomi identità.](../images/tutorials/external-audiences/identity-namespace-info.png)

## Creare uno schema per i metadati del segmento

Dopo aver creato uno spazio dei nomi delle identità, devi creare un nuovo schema per il segmento che creerai.

Per iniziare a comporre uno schema, seleziona innanzitutto **[!UICONTROL Schemi]** sulla barra di navigazione a sinistra, quindi **[!UICONTROL Crea schema]** nell&#39;angolo superiore destro dell&#39;area di lavoro Schemi. Da qui, seleziona **[!UICONTROL Sfoglia]** per visualizzare una selezione completa dei tipi di schema disponibili.

![Sono evidenziati sia Crea schema che Sfoglia.](../images/tutorials/external-audiences/create-schema-browse.png)

Poiché si sta creando una definizione di segmento, che è una classe predefinita, selezionare **[!UICONTROL Usa classe esistente]**. Selezionare la classe **[!UICONTROL Definizione segmento]**, seguita da **[!UICONTROL Assegna classe]**.

![La classe di definizione del segmento è evidenziata.](../images/tutorials/external-audiences/assign-class.png)

Ora che lo schema è stato creato, dovrai specificare quale campo conterrà l’ID del segmento. Questo campo deve essere contrassegnato come identità primaria e assegnato agli spazi dei nomi creati in precedenza.

![Le caselle di controllo per contrassegnare il campo selezionato come identità primaria sono evidenziate nell&#39;Editor schema.](../images/tutorials/external-audiences/mark-primary-identifier.png)

Dopo aver contrassegnato il campo `_id` come identità principale, seleziona il titolo dello schema, seguito dall&#39;interruttore **[!UICONTROL Profilo]**. Selezionare **[!UICONTROL Abilita]** per abilitare lo schema per [!DNL Real-Time Customer Profile].

![L&#39;attivazione dello schema per il profilo è evidenziata nell&#39;Editor schema.](../images/tutorials/external-audiences/schema-profile.png)

Ora questo schema è abilitato per il profilo, con l’identificazione principale assegnata allo spazio dei nomi dell’identità non persona creato. Di conseguenza, i metadati del segmento importati in Platform utilizzando questo schema verranno acquisiti in Profile senza essere uniti ad altri dati di profilo relativi alle persone.

## Creare un set di dati per lo schema

Dopo aver configurato lo schema, dovrai creare un set di dati per i metadati del segmento.

Per creare un set di dati, seguire le istruzioni riportate nella [guida utente del set di dati](../../catalog/datasets/user-guide.md#create). Segui l&#39;opzione **[!UICONTROL Crea set di dati dallo schema]** utilizzando lo schema creato in precedenza.

![Lo schema su cui desideri basare il set di dati è evidenziato.](../images/tutorials/external-audiences/select-schema.png)

Dopo aver creato il set di dati, continua a seguire le istruzioni riportate nella [guida utente del set di dati](../../catalog/datasets/user-guide.md#enable-profile) per abilitare questo set di dati per Real-Time Customer Profile.

![L&#39;interruttore per abilitare lo schema per il profilo è evidenziato nella pagina dell&#39;attività del set di dati.](../images/tutorials/external-audiences/dataset-profile.png)

## Impostare e importare i dati sul pubblico

Con il set di dati abilitato, ora i dati possono essere inviati a Platform tramite l’interfaccia utente o utilizzando le API Experience Platform. Puoi acquisire questi dati tramite una connessione in batch o in streaming.

### Acquisire dati utilizzando una connessione batch

Per creare una connessione batch, segui le istruzioni riportate nella generica [guida dell&#39;interfaccia utente di caricamento file locale](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Per un elenco completo delle origini disponibili con cui è possibile utilizzare i dati di acquisizione, leggere la [panoramica delle origini](../../sources/home.md).

### Acquisire dati utilizzando una connessione in streaming

Per creare una connessione in streaming, puoi seguire le istruzioni contenute nell&#39;[esercitazione API](../../sources/tutorials/api/create/streaming/http.md) o nell&#39;[esercitazione interfaccia utente](../../sources/tutorials/ui/create/streaming/http.md).

Dopo aver creato la connessione in streaming, potrai accedere all’endpoint di streaming univoco a cui inviare i dati. Per informazioni su come inviare dati a questi endpoint, leggi l&#39;[esercitazione sullo streaming dei dati dei record](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![L&#39;endpoint di streaming per la connessione di streaming è evidenziato nella pagina dei dettagli di origine.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Struttura dei metadati del pubblico

Dopo aver creato una connessione, ora puoi acquisire i dati in Platform.

Di seguito è riportato un esempio dei metadati del payload del pubblico esterno:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
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
| `schemaRef` | Lo schema **must** fa riferimento allo schema creato in precedenza per i metadati del segmento. |
| `datasetId` | L&#39;ID del set di dati **deve** fare riferimento al set di dati creato in precedenza per lo schema appena creato. |
| `xdmEntity._id` | L&#39;ID **deve** fare riferimento allo stesso ID segmento utilizzato come pubblico esterno. |
| `xdmEntity.identityMap` | Questa sezione **deve** contenere l&#39;etichetta di identità utilizzata durante la creazione dello spazio dei nomi creato in precedenza. |
| `{IDENTITY_NAMESPACE}` | Questa è l’etichetta dello spazio dei nomi dell’identità creato in precedenza. Quindi, per esempio, se hai chiamato il tuo spazio dei nomi di identità &quot;externalAudience&quot;, lo utilizzerai come chiave dell’array. |
| `segmentName` | Il nome del segmento in base al quale vuoi segmentare il pubblico esterno. |

## Creazione di segmenti utilizzando tipi di pubblico importati

Una volta configurati, i tipi di pubblico importati possono essere utilizzati come parte del processo di segmentazione. Per trovare tipi di pubblico esterni, vai al Generatore di segmenti e seleziona la scheda **[!UICONTROL Tipi di pubblico]** nella sezione **[!UICONTROL Campi]**.

![Il selettore dei tipi di pubblico esterni nel Generatore di segmenti è evidenziato.](../images/tutorials/external-audiences/external-audiences.png)

## Passaggi successivi

Ora che puoi utilizzare i tipi di pubblico esterni nei segmenti, puoi utilizzare il Generatore di segmenti per creare i segmenti. Per informazioni su come creare i segmenti, leggi l&#39;[esercitazione sulla creazione dei segmenti](./create-a-segment.md).

## Appendice

Oltre a utilizzare i metadati di pubblico esterno importati e a utilizzarli per la creazione di segmenti, puoi anche importare le appartenenze a segmenti esterni in Platform.

### Configurare uno schema di destinazione di iscrizione a un segmento esterno

Per iniziare a comporre uno schema, seleziona innanzitutto **[!UICONTROL Schemi]** sulla barra di navigazione a sinistra, quindi **[!UICONTROL Crea schema]** nell&#39;angolo superiore destro dell&#39;area di lavoro Schemi. Da qui, seleziona **[!UICONTROL Profilo individuale XDM]**.

![L&#39;area Profilo individuale XDM è evidenziata.](../images/tutorials/external-audiences/create-schema-profile.png)

Ora che lo schema è stato creato, è necessario aggiungere il gruppo di campi di iscrizione al segmento come parte dello schema. A tale scopo, selezionare [!UICONTROL Dettagli appartenenza al segmento], seguito da [!UICONTROL Aggiungi gruppi di campi].

![Il gruppo di campi Dettagli appartenenza al segmento è evidenziato.](../images/tutorials/external-audiences/segment-membership-details.png)

Inoltre, verificare che lo schema sia contrassegnato per **[!UICONTROL Profilo]**. A questo scopo, devi contrassegnare un campo come identità primaria.

![L&#39;attivazione dello schema per il profilo è evidenziata nell&#39;Editor schema.](../images/tutorials/external-audiences/external-segment-profile.png)

### Impostare il set di dati

Dopo aver creato lo schema, dovrai creare un set di dati.

Per creare un set di dati, seguire le istruzioni riportate nella [guida utente del set di dati](../../catalog/datasets/user-guide.md#create). Segui l&#39;opzione **[!UICONTROL Crea set di dati dallo schema]** utilizzando lo schema creato in precedenza.

![Lo schema utilizzato per creare il database è evidenziato.](../images/tutorials/external-audiences/select-schema.png)

Dopo aver creato il set di dati, continua a seguire le istruzioni riportate nella [guida utente del set di dati](../../catalog/datasets/user-guide.md#enable-profile) per abilitare questo set di dati per Real-Time Customer Profile.

![L&#39;opzione per abilitare lo schema per il profilo è evidenziata nel flusso di lavoro per la creazione di set di dati.](../images/tutorials/external-audiences/dataset-profile.png)

## Impostare e importare i dati di iscrizione del pubblico esterno

Con il set di dati abilitato, ora i dati possono essere inviati a Platform tramite l’interfaccia utente o utilizzando le API Experience Platform. Puoi acquisire questi dati tramite una connessione in batch o in streaming.

### Acquisire dati utilizzando una connessione batch

Per creare una connessione batch, segui le istruzioni riportate nella generica [guida dell&#39;interfaccia utente di caricamento file locale](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Per un elenco completo delle origini disponibili con cui è possibile utilizzare i dati di acquisizione, leggere la [panoramica delle origini](../../sources/home.md).

### Acquisire dati utilizzando una connessione in streaming

Per creare una connessione in streaming, puoi seguire le istruzioni contenute nell&#39;[esercitazione API](../../sources/tutorials/api/create/streaming/http.md) o nell&#39;[esercitazione interfaccia utente](../../sources/tutorials/ui/create/streaming/http.md).

Dopo aver creato la connessione in streaming, potrai accedere all’endpoint di streaming univoco a cui inviare i dati. Per informazioni su come inviare dati a questi endpoint, leggi l&#39;[esercitazione sullo streaming dei dati dei record](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![L&#39;endpoint di streaming per la connessione di streaming è evidenziato nella pagina dei dettagli di origine.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Struttura di iscrizione al segmento

Dopo aver creato una connessione, ora puoi acquisire i dati in Platform.

Di seguito è riportato un esempio del payload di iscrizione al pubblico esterno:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
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
| `schemaRef` | Lo schema **must** fa riferimento allo schema creato in precedenza per i dati di appartenenza al segmento. |
| `datasetId` | L&#39;ID del set di dati **deve** fare riferimento al set di dati creato in precedenza per lo schema di appartenenza appena creato. |
| `xdmEntity._id` | ID appropriato utilizzato per identificare in modo univoco il record all’interno del set di dati. |
| `{TENANT_NAME}.identities` | Questa sezione viene utilizzata per collegare il gruppo di campi delle identità personalizzate con gli utenti importati in precedenza. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | Questa è l’etichetta dello spazio dei nomi dell’identità personalizzata creato in precedenza. Quindi, per esempio, se hai chiamato il tuo spazio dei nomi di identità &quot;externalAudience&quot;, lo utilizzerai come chiave dell’array. |

>[!NOTE]
>
>Per impostazione predefinita, le appartenenze a un pubblico esterno vengono eliminate dopo 30 giorni. Per evitare l&#39;eliminazione e conservarle per più di 30 giorni, utilizza il campo `validUntil` durante l&#39;acquisizione dei dati sul pubblico. Per ulteriori informazioni su questo campo, consulta la guida sui gruppi di campi dello schema [Dettagli appartenenza al segmento](../../xdm/field-groups/profile/segmentation.md).
