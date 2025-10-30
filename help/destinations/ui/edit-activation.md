---
keywords: modifica attivazione, modifica destinazione, modifica destinazione
title: Modifica flussi di dati di attivazione
type: Tutorial
description: Segui i passaggi descritti in questo articolo per modificare un flusso di dati di attivazione esistente in Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 0%

---

# Modifica flussi di dati di attivazione {#edit-activation-flows}

In Adobe Experience Platform, puoi configurare vari componenti dei flussi di dati di attivazione esistenti per le destinazioni, ad esempio:

* [Attiva o disattiva](#enable-disable-dataflows) flussi di dati di attivazione
* [Aggiungi ulteriori tipi di pubblico](#add-audiences) ai flussi di dati di attivazione
* [Modificare attributi e identità mappati](#edit-mapped-attributes)
* [Modifica la pianificazione di attivazione e la frequenza di esportazione](#edit-schedule-frequency)
* [Aggiungi set di dati aggiuntivi](#add-datasets) al flusso di lavoro di attivazione
* [Modifica azioni di marketing](#edit-marketing-actions) per i flussi di dati di attivazione
* [Applica etichette di accesso](#apply-access-labels) ai dati esportati
* [Modifica nomi e descrizioni](#edit-names-descriptions) per i flussi di dati di attivazione

## Sfoglia flussi di dati di attivazione {#browse-activation-dataflows}

Segui i passaggi seguenti per sfogliare i flussi di dati di attivazione esistenti e identificare quello che desideri modificare.

1. Accedi alla [interfaccia utente di Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinations]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Browse]** dall&#39;intestazione superiore per visualizzare i flussi di dati di destinazione esistenti.

   ![Sfoglia destinazioni](../assets/ui/edit-activation/browse-destinations.png)

2. Seleziona l&#39;icona del filtro ![Icona filtro](../../images/icons/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtra destinazioni](../assets/ui/edit-activation/filter-destinations.png)

3. Seleziona il nome del flusso di dati di destinazione da modificare.

   ![Seleziona destinazione](../assets/ui/edit-activation/destination-select.png)

4. Viene visualizzata la pagina **[!UICONTROL Dataflow runs]** per la destinazione, con i controlli disponibili. A seconda del tipo di destinazione, puoi eseguire varie operazioni di flusso di dati. Consulta le sezioni successive per ogni operazione di flusso di dati supportata.

## Abilitare o disabilitare i flussi di dati di attivazione {#enable-disable-dataflows}

Utilizzare l&#39;interruttore **[!UICONTROL Enabled]/[!UICONTROL Disabled]** per avviare o sospendere tutte le esportazioni di dati nella destinazione.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra l&#39;interruttore di esecuzione del flusso di dati abilitato/disabilitato.](../assets/ui/edit-activation/enable-toggle.png)

## Aggiungere tipi di pubblico a un flusso di dati di attivazione {#add-audiences}

Seleziona **[!UICONTROL Activate audiences]** nella barra a destra per modificare i tipi di pubblico da inviare alla destinazione. Questa azione ti porta al flusso di lavoro di attivazione.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra l&#39;opzione di esecuzione Attiva flusso di dati tipi di pubblico.](../assets/ui/edit-activation/activate-audiences.png)

Nel passaggio **[!UICONTROL Select audiences]** del flusso di lavoro di attivazione, puoi rimuovere i tipi di pubblico esistenti o aggiungere nuovi tipi di pubblico al flusso di lavoro di attivazione.

Il flusso di lavoro di attivazione varia leggermente a seconda del tipo di destinazione. Per ulteriori informazioni sui flussi di lavoro di attivazione per ciascun tipo di destinazione, consulta le seguenti guide:

* [Attiva i tipi di pubblico nelle destinazioni di streaming](./activate-segment-streaming-destinations.md) (ad esempio, Facebook o Twitter);
* [Attiva i tipi di pubblico nelle destinazioni di esportazione del profilo batch](./activate-batch-profile-destinations.md) (ad esempio, Amazon S3 o Oracle Eloqua);
* [Attiva i tipi di pubblico nelle destinazioni di esportazione del profilo di streaming](./activate-streaming-profile-destinations.md) (ad esempio, API HTTP o Amazon Kinesis).

## Modifica la pianificazione di attivazione e la frequenza di esportazione {#edit-schedule-frequency}

Seleziona **[!UICONTROL Activate audiences]** nella barra a destra. Questa azione ti porta al flusso di lavoro di attivazione.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra l&#39;opzione di esecuzione Attiva flusso di dati tipi di pubblico.](../assets/ui/edit-activation/activate-audiences.png)

Seleziona il passaggio **[!UICONTROL Scheduling]** nel flusso di lavoro di attivazione per modificare la pianificazione dell&#39;attivazione e la frequenza di esportazione per il flusso di dati. Questo passaggio ti consente di configurare la frequenza con cui i dati vengono esportati nella destinazione.

Nel passaggio **[!UICONTROL Scheduling]** del flusso di lavoro di attivazione è possibile:

* Regola la frequenza di esportazione.
* Imposta o modifica le date di inizio e fine del flusso di dati di attivazione e altro ancora.

Le operazioni di programmazione che è possibile eseguire variano leggermente a seconda del tipo di destinazione. Per ulteriori informazioni sui flussi di lavoro di attivazione per ciascun tipo di destinazione, consulta le seguenti guide:

* [Attiva i tipi di pubblico nelle destinazioni di streaming](./activate-segment-streaming-destinations.md) (ad esempio, Facebook o Twitter);
* [Attiva i tipi di pubblico nelle destinazioni di esportazione del profilo batch](./activate-batch-profile-destinations.md) (ad esempio, Amazon S3 o Oracle Eloqua);
* [Attiva i tipi di pubblico nelle destinazioni di esportazione del profilo di streaming](./activate-streaming-profile-destinations.md) (ad esempio, API HTTP o Amazon Kinesis).

## Modificare attributi e identità mappati {#edit-mapped-attributes}

Seleziona **[!UICONTROL Activate audiences]** nella barra a destra. Questa azione ti porta al flusso di lavoro di attivazione.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra l&#39;opzione di esecuzione Attiva flusso di dati tipi di pubblico.](../assets/ui/edit-activation/activate-audiences.png)

Seleziona il passaggio **[!UICONTROL Mapping]** nel flusso di lavoro di attivazione per modificare gli attributi e le identità mappati per il flusso di dati di attivazione. Questo consente di regolare gli attributi e le identità del profilo da esportare nella destinazione.

Nel passaggio **[!UICONTROL Mapping]** del flusso di lavoro di attivazione è possibile:

* Aggiungi nuovi attributi o identità alla mappatura.
* Rimuovi gli attributi o le identità esistenti dal mapping.
* Regola l’ordine delle mappature per definire l’ordine delle colonne nei file esportati.

Il flusso di lavoro di attivazione varia leggermente a seconda del tipo di destinazione. Per ulteriori informazioni sui flussi di lavoro di attivazione per ciascun tipo di destinazione, consulta le seguenti guide:

* [Attiva i tipi di pubblico nelle destinazioni di streaming](./activate-segment-streaming-destinations.md) (ad esempio, Facebook o Twitter);
* [Attiva i tipi di pubblico nelle destinazioni di esportazione del profilo batch](./activate-batch-profile-destinations.md) (ad esempio, Amazon S3 o Oracle Eloqua);
* [Attiva i tipi di pubblico nelle destinazioni di esportazione del profilo di streaming](./activate-streaming-profile-destinations.md) (ad esempio, API HTTP o Amazon Kinesis).

## Aggiungere set di dati a un flusso di dati di attivazione {#add-datasets}

Seleziona **[!UICONTROL Export datasets]** nella barra a destra per selezionare set di dati aggiuntivi da esportare nella destinazione. Questa opzione consente di accedere al [flusso di lavoro di esportazione del set di dati](export-datasets.md).

>[!NOTE]
>
>Questa opzione è visibile solo per [destinazioni che supportano l&#39;esportazione del set di dati](export-datasets.md#supported-destinations).

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra l&#39;opzione di esecuzione del flusso di dati Esporta set di dati.](../assets/ui/edit-activation/export-datasets.png)

## [!BADGE Beta]{type=Informative} Modifica azioni di marketing {#edit-marketing-actions}

>[!NOTE]
>
>Questa funzionalità è attualmente in **beta**. Per richiedere l’accesso, contatta il rappresentante Adobe.

Puoi aggiungere o rimuovere azioni di marketing impostate al momento della connessione iniziale alla destinazione.

Seleziona **[!UICONTROL Edit marketing actions]** nella barra a destra per aprire la schermata di selezione delle azioni di marketing.

![Immagine dell&#39;interfaccia utente di Experience Platform con l&#39;opzione Modifica azioni di marketing.](../assets/ui/edit-activation/edit-marketing-actions.png)

Selezionare le azioni di marketing applicabili, quindi selezionare **[!UICONTROL Save]** per applicare le modifiche.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra la schermata Modifica azioni di marketing.](../assets/ui/edit-activation/edit-marketing-actions-screen.png)


## Applicare le etichette di accesso {#apply-access-labels}

Selezionare **[!UICONTROL Apply access labels]** per modificare le etichette di utilizzo dei dati per i dati esportati. Per ulteriori informazioni, consulta la [documentazione delle etichette di utilizzo dei dati](../../data-governance/labels/overview.md).

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra l&#39;opzione di esecuzione del flusso di dati Esporta set di dati.](../assets/ui/edit-activation/apply-access-labels.png)

## Modifica nomi e descrizioni dei flussi di dati di attivazione {#edit-names-descriptions}

Per modificare il nome e la descrizione del flusso di dati di attivazione, utilizzare i campi **[!UICONTROL Destination name]** e **[!UICONTROL Description]**.

![Dettagli destinazione](../assets/ui/edit-activation/edit-destination-name-description.png)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, è stata utilizzata l&#39;area di lavoro **[!UICONTROL destinations]** per aggiornare i flussi di dati di destinazione esistenti.

Per ulteriori informazioni sulle destinazioni, consulta la [panoramica sulle destinazioni](../catalog/overview.md).
