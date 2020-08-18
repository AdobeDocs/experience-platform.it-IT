---
keywords: Experience Platform;home;popular topics; delete dataflows
description: I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per eliminare i flussi di dati dall'area di lavoro Origini.
solution: Experience Platform
title: Eliminare i flussi di dati
topic: overview
translation-type: tm+mt
source-git-commit: 6bd5dc5a68fb2814ab99d43b34f90aa7e50aa463
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 1%

---


# Eliminare i flussi di dati

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per eliminare i flussi di dati dall&#39; [!UICONTROL Sources] area di lavoro.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [[!DNL Profilo cliente in tempo reale]](../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Eliminare i flussi di dati mediante l’interfaccia utente

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; **[!UICONTROL Sources]** area di lavoro. Nella **[!UICONTROL Catalog]** schermata sono visualizzate diverse origini per le quali è possibile creare account e flussi di dati. Ogni origine mostra il numero di account e di flussi di dati esistenti ad essi associati.

Selezionate **[!UICONTROL Dataflows]** per accedere alla **[!UICONTROL Dataflows]** pagina.

![dataset-flow-activity](../../images/tutorials/delete/dataflows.png)

Viene visualizzato un elenco dei flussi di dati esistenti. In questa pagina è presente un elenco di informazioni ordinabili per i flussi di dati esistenti, quali origine, nome utente, stato di esecuzione e data dell&#39;ultima esecuzione. Selezionate l’icona **** funnel in alto a sinistra per ordinare i dati.

![elenco dei flussi di dati](../../images/tutorials/delete/dataflows-list.png)

Il pannello di ordinamento viene visualizzato sul lato sinistro dello schermo, contenente un elenco delle sorgenti disponibili.
È possibile selezionare più origini utilizzando la funzione di ordinamento.

Selezionare l&#39;origine a cui si desidera accedere e individuare il flusso di dati che si desidera eliminare dall&#39;elenco dei flussi di dati nell&#39;interfaccia principale. Nell&#39;esempio, l&#39;origine selezionata è e il nome del flusso di dati è **[!DNL Azure Blob Storage]** **[!UICONTROL Customer profiles dataflow]**. Quando si selezionano più origini dal pannello di ordinamento, i flussi di dati creati più di recente vengono visualizzati per primi, perché l&#39;elenco è ordinato in base alla data di creazione.

Selezionare il flusso di dati da eliminare.

![ordinamento dei dati](../../images/tutorials/delete/dataflows-sort.png)

Il **[!UICONTROL Properties]** pannello viene visualizzato sul lato destro dello schermo, contenente informazioni relative al flusso di dati selezionato e un’opzione per **[!UICONTROL Edit schedule]**.

Per eliminare il flusso di dati, selezionare **[!UICONTROL Delete]**.

![ordinamento dei dati](../../images/tutorials/delete/dataflows-properties.png)

Viene visualizzata una finestra di dialogo di conferma finale; selezionate **[!UICONTROL Delete]** per completare il processo.

![delete](../../images/tutorials/delete/delete.png)

Dopo alcuni istanti, nella parte inferiore dello schermo viene visualizzata una casella di conferma verde per confermare l’avvenuta eliminazione.

![confermata](../../images/tutorials/delete/confirmed.png)

## Passaggi successivi

Seguendo questa esercitazione, è stato possibile accedere agli account e ai flussi di dati esistenti dall&#39; **[!UICONTROL Sources]** area di lavoro. I dati in entrata possono ora essere utilizzati dai [!DNL Platform] servizi a valle come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i documenti seguenti:

- [[!DNL Real-time Customer Profile] panoramica](../../../profile/home.md)
- [[!DNL Data Science Workspace] panoramica](../../../data-science-workspace/home.md)