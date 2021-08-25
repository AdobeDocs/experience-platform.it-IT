---
keywords: collegare destinazione;connessione destinazione;come collegare destinazione
title: Crea una nuova connessione di destinazione
type: Tutorial
description: Questa esercitazione elenca i passaggi per la connessione a una destinazione in Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Crea una nuova connessione di destinazione

## Panoramica {#overview}

Prima di poter inviare i dati sul pubblico a una destinazione, è necessario impostare una connessione alla piattaforma di destinazione. Questo articolo illustra come impostare una nuova destinazione utilizzando l’interfaccia utente di Adobe Experience Platform.

## Crea una nuova connessione di destinazione {#setup}

1. Vai a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]** e seleziona la scheda **[!UICONTROL Catalogo]** .

   ![Pagina del catalogo](../assets/ui/connect-destinations/catalog.png)

1. A seconda che si disponga di una connessione esistente alla destinazione, è possibile visualizzare un pulsante **[!UICONTROL Configurazione]** o un pulsante **[!UICONTROL Attiva segmenti]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Attiva segmenti]** e **[!UICONTROL Imposta]**, consulta la sezione [Catalogo](../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

   Seleziona **[!UICONTROL Imposta]** o **[!UICONTROL Attiva segmenti]**, a seconda del pulsante disponibile.

   ![Pagina del catalogo](../assets/ui/connect-destinations/set-up.png)

   ![Attivare i segmenti](../assets/ui/connect-destinations/activate-segments.png)

1. Se hai selezionato **[!UICONTROL Imposta]**, passa al passaggio successivo.

   Se hai selezionato **[!UICONTROL Attiva segmenti]**, ora puoi visualizzare un elenco delle connessioni di destinazione esistenti.

   Selezionare **[!UICONTROL Configura nuova destinazione]**.

   ![Configurare una nuova destinazione](../assets/ui/connect-destinations/configure-new-destination.png)

1. Immetti i dettagli di connessione della piattaforma di destinazione, quindi seleziona **[!UICONTROL Connetti a destinazione]**.

   >[!NOTE]
   >
   >L&#39;immagine seguente è utilizzata solo a scopo illustrativo. I dettagli della connessione di destinazione variano tra le destinazioni. Per informazioni dettagliate sui dettagli di connessione per la destinazione, consulta la sezione **Parametri di connessione** in ogni pagina [catalogo di destinazione](../catalog/overview.md) (ad esempio, [Customer Match di Google](..//catalog/advertising/google-customer-match.md#parameters)).

   ![Connetti alla destinazione](../assets/ui/connect-destinations/connect-destination.png)

1. Seleziona **[!UICONTROL Avanti]**.

   ![Connetti alla destinazione](../assets/ui/connect-destinations/next.png)

1. Seleziona le azioni di marketing applicabili ai dati da esportare nella destinazione. Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la pagina [panoramica dei criteri di utilizzo dei dati](../../data-governance/policies/overview.md) .

   ![Selezionare le azioni di marketing](../assets/ui/connect-destinations/governance.png)

1. Seleziona **[!UICONTROL Salva e esci]** per salvare la configurazione di destinazione, oppure seleziona **[!UICONTROL Avanti]** per procedere con i dati del pubblico [flusso di attivazione](activation-overview.md).