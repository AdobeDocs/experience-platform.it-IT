---
title: Estendere le pianificazioni di esportazione dei set di dati per i flussi di dati creati prima di novembre 2024
description: Scopri come estendere la pianificazione dell’esportazione per i flussi di dati di esportazione dei set di dati creati prima di novembre 2024 che cesseranno di funzionare il 1° settembre 2025.
type: Tutorial
exl-id: a756886b-3f4b-4427-bd26-817221ba68aa
source-git-commit: 0da592dd2846ed0f1eeb31102842c8895cac6952
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Estendere le pianificazioni di esportazione dei set di dati per i flussi di dati creati prima di novembre 2024

>[!IMPORTANT]
>
>**Azione richiesta**: se l&#39;organizzazione dispone di [flussi di dati di esportazione del set di dati](export-datasets.md) creati prima di novembre 2024, questi flussi di dati cesseranno di funzionare il 1° settembre 2025. Questa guida spiega come estendere la pianificazione dell’esportazione oltre questa data per i flussi di dati che desideri mantenere.

## Panoramica {#overview}

Nella versione [di settembre 2024 di Experience Platform](/help/release-notes/2024/september-2024.md#destinations), Adobe ha introdotto una data di fine predefinita del **1 maggio 2025** per tutti i flussi di dati di esportazione dei set di dati creati prima della versione di settembre 2024.

**Questa data è stata aggiornata al 1° settembre 2025** per tutti i flussi di dati di esportazione del set di dati creati **prima di novembre 2024**.

I flussi di dati di esportazione del set di dati creati prima di novembre 2024 interromperanno l’esportazione dei dati il **1 settembre 2025** a meno che non ne estenda manualmente la data di scadenza.

Se i flussi di dati sono necessari per continuare a esportare dati dopo il **1 settembre 2025**, è necessario estendere le pianificazioni per ogni destinazione in cui si esportano i set di dati, seguendo i passaggi descritti in questa guida.

## Destinazioni interessate {#affected-destinations}

La tua organizzazione potrebbe disporre di flussi di dati di esportazione di set di dati attivi che inviano dati alle destinazioni elencate di seguito. Segui i passaggi descritti nelle sezioni successive e guarda il video della procedura dettagliata per scoprire come identificare quali set di dati sono impostati per la scadenza.

* [[!DNL Azure Data Lake Storage Gen2]](../catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../catalog/cloud-storage/sftp.md#changelog)
* [[!DNL Marketo Measure Ultimate]](../catalog/adobe/marketo-measure-ultimate.md)

## Tutorial video {#video}

Guarda il video seguente per una dimostrazione dettagliata di come identificare le esportazioni dei set di dati con le date di fine imminenti ed estendere la pianificazione delle esportazioni per i flussi di dati che desideri mantenere.

>[!VIDEO](https://video.tv.adobe.com/v/3470518/)

## Passaggio 1: identificare i flussi di dati interessati {#identify-dataflows}

Prima di estendere la pianificazione dell’esportazione per i flussi di dati di esportazione del set di dati, devi identificare quali flussi di dati sono interessati dalla data di scadenza imminente. Segui i passaggi seguenti per individuare i flussi di dati che richiedono un’azione.

1. Vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** nell&#39;interfaccia utente di Experience Platform.
2. Seleziona **[!UICONTROL Attiva]** in una destinazione con flussi di dati di esportazione del set di dati attivi.

   >[!TIP]
   >
   >Utilizza il filtro **[!UICONTROL Tipi di dati]** sul lato sinistro del catalogo per filtrare le destinazioni disponibili per **[!UICONTROL Set di dati]**.

3. Selezionare il tipo di dati **[!UICONTROL Set di dati]** per visualizzare solo i flussi di dati con esportazioni di set di dati.
   ![Schermata che mostra come filtrare i flussi di dati per tipo di dati.](/help/destinations/assets/ui/export-datasets/dataset-type.png)
4. Seleziona l&#39;intestazione di colonna **[!UICONTROL Created]** e scegli **[!UICONTROL Sort Ascending]** per visualizzare i flussi di dati precedenti.
   ![Schermata che mostra come ordinare i flussi di dati in modo crescente.](/help/destinations/assets/ui/export-datasets/sort-ascending.png)
5. Identifica quale dei flussi di dati creati prima di novembre 2024 desideri mantenere.

## Passaggio 2: accedere al flusso di lavoro per l’esportazione dei set di dati {#access-workflow}

Per ogni flusso di dati che desideri mantenere, devi accedere al flusso di lavoro Esporta set di dati per modificare la pianificazione.

1. Selezionare il nome del flusso di dati nella colonna **[!UICONTROL Nome]**. Viene visualizzata la pagina **[!UICONTROL Esecuzioni del flusso di dati]**.
2. In questa pagina, seleziona l&#39;opzione **[!UICONTROL Esporta set di dati]**.
   ![Schermata che mostra l&#39;opzione Esporta set di dati nella pagina Esecuzioni del flusso di dati.](/help/destinations/assets/ui/export-datasets/export-datasets-option.png)
3. Nella pagina **[!UICONTROL Seleziona set di dati]**, seleziona **[!UICONTROL Avanti]**. Non è necessario aggiungere nuovi set di dati al flusso di dati.
4. Viene visualizzata la pagina **[!UICONTROL Pianificazione]** in cui è possibile visualizzare una notifica che informa sulla data di scadenza dell&#39;esportazione del set di dati.
   ![Flussi di dati di esportazione del set di dati con notifica di scadenza](/help/destinations/assets/ui/export-datasets/dataset-export-notification.png)

## Passaggio 3: estendere il programma di esportazione {#extend-export-schedule}

Ora puoi modificare la pianificazione dell’esportazione per estenderla oltre il 1° settembre 2025.

1. Seleziona **[!UICONTROL Modifica pianificazione]**.
   ![Schermata del passaggio Pianificazione che mostra il pulsante Modifica pianificazione.](/help/destinations/assets/ui/export-datasets/edit-schedule.png)
2. Seleziona una nuova pianificazione di esportazione, quindi seleziona **[!UICONTROL Salva]**.
   ![Schermata del passaggio Pianificazione che mostra le opzioni di pianificazione.](/help/destinations/assets/ui/export-datasets/edit-schedule-calendar.png)

   >[!TIP]
   >
   >Consultate la [documentazione sull&#39;esportazione dei set di dati](export-datasets.md#scheduling) per informazioni dettagliate su come configurare le pianificazioni di esportazione dei set di dati.

## Cosa succede se non rispetto la scadenza del 1° settembre 2025? {#missed-deadline}

Se i flussi di dati per l’esportazione del set di dati sono scaduti il 1° settembre 2025 e desideri ancora estenderli, segui i passaggi descritti nelle sezioni precedenti per estenderne la pianificazione.

Se estendi la pianificazione dell&#39;esportazione entro 30 giorni (o meno se il [time-to-live impostato nel set di dati esportato](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md) è inferiore a 30 giorni), puoi comunque ottenere una retrocompilazione dei dati che non sono stati esportati tra il 1° settembre e la data in cui hai riabilitato l&#39;esportazione. Quando si imposta una nuova ora di fine, *non* verrà prima eseguita un&#39;esportazione di file completa. Invece, le esportazioni continueranno in modo incrementale da dove si sono interrotte il 1° settembre.