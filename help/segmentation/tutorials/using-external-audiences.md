---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Applica la conformità all'utilizzo dei dati per i segmenti di pubblico
topic: esercitazione
translation-type: tm+mt
source-git-commit: 2ca0768c951cf67a775fdfc2c1f9440596d118bf
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---


# Importazione e utilizzo di audience esterne

Adobe Experience Platform supporta la possibilità di importare audience esterna, che può essere successivamente utilizzata come componenti per una nuova definizione di segmento. Questo documento fornisce un&#39;esercitazione per configurare  Experience Platform per l&#39;importazione e l&#39;utilizzo di audience esterne.

## Introduzione

- [Servizio](../home.md) segmentazione: Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
- [Profilo](../../profile/home.md) cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.
- [Set](../../catalog/datasets/overview.md) di dati: Il concetto di storage e gestione per la persistenza dei dati nel Experience Platform .
- [Caricamento](../../ingestion/streaming-ingestion/overview.md) streaming:  Experience Platform archivia e archivia in tempo reale i dati provenienti da dispositivi lato client e lato server.

## Creare uno spazio dei nomi di identità per l&#39;audience esterna

Il primo passo per utilizzare audience esterne è la creazione di uno spazio dei nomi di identità. Gli spazi dei nomi delle identità consentono a Platform di associare la posizione di origine di un segmento.

Per creare uno spazio nomi identità, seguire le istruzioni riportate nella [guida allo spazio nomi identità](../../identity-service/namespaces.md#manage-namespaces). Durante la creazione dello spazio dei nomi dell&#39;identità, aggiungete i dettagli dell&#39;origine allo spazio dei nomi dell&#39;identità e contrassegnatene [!UICONTROL Type] come **[!UICONTROL Non-people identifier]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Creare uno schema per i metadati del segmento

Dopo aver creato uno spazio nomi identità, è necessario creare un nuovo schema per il segmento che si desidera creare.

Per iniziare a comporre uno schema, selezionare prima **[!UICONTROL Schemas]** nella barra di navigazione a sinistra, seguita da **[!UICONTROL Create schema]** nell&#39;angolo superiore destro dell&#39;area di lavoro Schemi. Da qui, selezionare **[!UICONTROL Browse]** per visualizzare una selezione completa dei tipi di schema disponibili.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Poiché si sta creando una definizione del segmento, che è una classe predefinita, selezionare **[!UICONTROL Use existing class]**. A questo punto, selezionate la classe **[!UICONTROL Segment definition]**, seguita da **[!UICONTROL Assign class]**.

![](../images/tutorials/external-audiences/assign-class.png)

Una volta creato lo schema, sarà necessario specificare quale campo conterrà l&#39;ID del segmento. Questo campo deve essere contrassegnato come identità principale e assegnato agli spazi dei nomi creati in precedenza.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Dopo aver contrassegnato il campo `_id` come identità principale, selezionare il titolo dello schema, seguito dall&#39;interruttore **[!UICONTROL Profile]**. Selezionare **[!UICONTROL Enable]** per abilitare lo schema per [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Ora, questo schema è abilitato per Profilo, con l&#39;identificazione principale assegnata allo spazio dei nomi di identità non-persona creato. Di conseguenza, i metadati del segmento importati in Piattaforma con questo schema verranno trasferiti in Profilo senza essere uniti ad altri dati di profilo relativi alle persone.

## Creare un dataset per lo schema

Dopo aver configurato lo schema, sarà necessario creare un dataset per i metadati del segmento.

Per creare un set di dati, seguire le istruzioni riportate nella [guida utente del dataset](../../catalog/datasets/user-guide.md#create). Seguire l&#39;opzione **[!UICONTROL Create dataset from schema]**, utilizzando lo schema creato in precedenza.

![](../images/tutorials/external-audiences/select-schema.png)

Dopo aver creato il dataset, continuare a seguire le istruzioni riportate nella [guida utente del dataset](../../catalog/datasets/user-guide.md#enable-profile) per abilitare questo dataset per il profilo cliente in tempo reale.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configurare e importare i dati sul pubblico

Con il set di dati abilitato, i dati possono ora essere inviati in Piattaforma tramite l&#39;interfaccia utente o tramite le API del Experience Platform . Per assimilare questi dati in Platform, dovrete creare una connessione di streaming.

Per creare una connessione in streaming, potete seguire le istruzioni riportate nell&#39; [esercitazione API](../../sources/tutorials/api/create/streaming/http.md) o nell&#39; [esercitazione sull&#39;interfaccia utente](../../sources/tutorials/ui/create/streaming/http.md).

Una volta creata la connessione di streaming, avrete accesso al vostro endpoint di streaming univoco a cui potete inviare i dati. Per informazioni su come inviare i dati a questi endpoint, leggere l&#39; [tutorial on streaming record data](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Creazione di segmenti utilizzando le audience importate

Una volta configurate le audience importate, queste possono essere utilizzate come parte del processo di segmentazione. Per trovare audience esterne, andate al Generatore di segmenti e selezionate la scheda **[!UICONTROL Audiences]** nella sezione **[!UICONTROL Fields]**.

![](../images/tutorials/external-audiences/external-audiences.png)

## Passaggi successivi

Ora che puoi usare audience esterne nei tuoi segmenti, puoi usare Segment Builder (Generatore di segmenti) per creare segmenti. Per informazioni su come creare i segmenti, consulta l&#39; [esercitazione sulla creazione di segmenti](./create-a-segment.md).