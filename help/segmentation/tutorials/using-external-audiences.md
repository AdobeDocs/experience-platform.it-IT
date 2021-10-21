---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Importazione e utilizzo di tipi di pubblico esterni
description: Segui questa esercitazione per scoprire come utilizzare i tipi di pubblico esterni con Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '809'
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

Per creare un set di dati, segui le istruzioni nella sezione [guida utente del set di dati](../../catalog/datasets/user-guide.md#create). Lei vorrà seguire la **[!UICONTROL Creare un set di dati dallo schema]** utilizzando lo schema creato in precedenza.

![](../images/tutorials/external-audiences/select-schema.png)

Dopo aver creato il set di dati, continua a seguire le istruzioni in [guida utente del set di dati](../../catalog/datasets/user-guide.md#enable-profile) per abilitare questo set di dati per il profilo cliente in tempo reale.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configurazione e importazione di dati sul pubblico

Con il set di dati abilitato, i dati possono ora essere inviati in Platform tramite l’interfaccia utente o utilizzando le API di Experience Platform. Per acquisire questi dati in Platform, dovrai creare una connessione in streaming.

Per creare una connessione in streaming, puoi seguire le istruzioni contenute in [Esercitazione API](../../sources/tutorials/api/create/streaming/http.md) o [Esercitazione sull’interfaccia utente](../../sources/tutorials/ui/create/streaming/http.md).

Una volta creata la connessione streaming, avrai accesso all&#39;endpoint streaming univoco a cui puoi inviare i tuoi dati. Per informazioni su come inviare dati a questi endpoint, consulta la sezione [esercitazione sullo streaming dei dati di record](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Creazione di segmenti utilizzando i tipi di pubblico importati

Una volta configurati i tipi di pubblico importati, possono essere utilizzati come parte del processo di segmentazione. Per trovare tipi di pubblico esterni, vai al Generatore di segmenti e seleziona **[!UICONTROL Tipi di pubblico]** nella scheda **[!UICONTROL Campi]** sezione .

![](../images/tutorials/external-audiences/external-audiences.png)

## Passaggi successivi

Ora che puoi utilizzare tipi di pubblico esterni nei segmenti, puoi utilizzare il Generatore di segmenti per creare segmenti. Per scoprire come creare i segmenti, leggi la sezione [esercitazione sulla creazione di segmenti](./create-a-segment.md).
