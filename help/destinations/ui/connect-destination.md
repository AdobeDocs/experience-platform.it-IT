---
title: Creare una nuova connessione di destinazione
type: Tutorial
description: Scopri come connettersi a una destinazione in Adobe Experience Platform, abilitare gli avvisi e impostare azioni di marketing per la destinazione connessa.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 0%

---

# Creare una nuova connessione di destinazione

>[!IMPORTANT]
> 
>* Per connettersi a una destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per connettersi a una destinazione che supporta le esportazioni dei set di dati, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione e attivazione dei set di dati]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

## Panoramica {#overview}

Prima di poter inviare dati sul pubblico a una destinazione, devi impostare una connessione alla piattaforma di destinazione. Questo articolo mostra come impostare una nuova connessione di destinazione, alla quale è quindi possibile attivare i tipi di pubblico o esportare i set di dati utilizzando l’interfaccia utente di Adobe Experience Platform.

## Trovare la destinazione desiderata nel catalogo {#setup}

1. Vai a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]** e seleziona la scheda **[!UICONTROL Catalogo]**.

   ![Schermata dell&#39;interfaccia utente di Experience Platform che mostra la pagina del catalogo delle destinazioni.](../assets/ui/connect-destinations/catalog.png)

2. Le schede di destinazione nel catalogo possono avere controlli di azione diversi, a seconda che tu disponga di una connessione esistente alla destinazione e che le destinazioni supportino l’attivazione di tipi di pubblico, l’esportazione di set di dati o entrambi. Potresti visualizzare uno dei seguenti controlli per le schede di destinazione:

   * **[!UICONTROL Configurazione]**. Prima di poter attivare i tipi di pubblico o esportare i set di dati, è necessario impostare una connessione a questa destinazione.
   * **[!UICONTROL Attiva]**. Connessione già impostata a questa destinazione. Questa destinazione supporta l’attivazione del pubblico e le esportazioni di set di dati.
   * **[!UICONTROL Attiva tipi di pubblico]**. Connessione già impostata a questa destinazione. Questa destinazione supporta solo l’attivazione del pubblico.

   Per ulteriori informazioni sulla differenza tra questi controlli, è inoltre possibile fare riferimento alla sezione [Catalogo](../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

   Selezionare **[!UICONTROL Configura]**, **[!UICONTROL Attiva]** o **[!UICONTROL Attiva tipi di pubblico]**, a seconda del controllo disponibile.

   ![Schermata dell&#39;interfaccia utente di Experience Platform che mostra la pagina del catalogo delle destinazioni con il controllo di configurazione evidenziato.](../assets/ui/connect-destinations/set-up.png)

   ![Schermata dell&#39;interfaccia utente di Experience Platform che mostra la pagina del catalogo delle destinazioni in cui è evidenziato il controllo Attiva pubblico.](../assets/ui/connect-destinations/activate-segments.png)

3. Se hai selezionato **[!UICONTROL Configura]**, passa al passaggio successivo, per [autenticare](#authenticate) nella destinazione.

   Se hai selezionato **[!UICONTROL Attiva]**, **[!UICONTROL Attiva pubblico]** o **[!UICONTROL Esporta set di dati]**, ora puoi visualizzare un elenco delle connessioni di destinazione esistenti.

   Selezionare **[!UICONTROL Configura nuova destinazione]** per stabilire una nuova connessione alla destinazione.

   ![Schermata dell&#39;interfaccia utente di Experience Platform in cui è visualizzato un elenco delle destinazioni disponibili ed è evidenziato il controllo Configura nuova destinazione.](../assets/ui/connect-destinations/configure-new-destination.png)

## Autenticarsi nella destinazione {#authenticate}

Il primo passaggio nella connessione a una destinazione consiste nell’eseguire l’autenticazione nella piattaforma di destinazione.

A seconda della destinazione a cui ti stai connettendo, potresti essere reindirizzato alla pagina del partner di destinazione per l’autenticazione oppure ti potrebbe essere richiesto di immettere le credenziali di autenticazione direttamente nel flusso di lavoro di Platform. Di seguito è riportato un esempio di input necessario per l&#39;autenticazione in una destinazione [!DNL Amazon S3]. Istruzioni dettagliate sull&#39;input richiesto vengono fornite in ogni pagina della documentazione di destinazione (vedere, ad esempio, la sezione di autenticazione per [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) e per [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)).

**[!DNL Amazon S3]parametri di autenticazione obbligatori e facoltativi**

![Immagine che mostra i parametri di input obbligatori e facoltativi durante l&#39;autenticazione in una destinazione Amazon S3.](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## Impostare i parametri di connessione {#set-up-connection-parameters}

Se hai già impostato l’autenticazione per la destinazione, puoi continuare con l’account esistente oppure puoi impostarne uno nuovo.

A seconda della destinazione a cui ti stai connettendo, potrebbe essere richiesto di immettere diversi tipi di parametri di connessione. Ad esempio, quando ti connetti a una destinazione [!DNL Amazon S3], ti viene richiesto di fornire dettagli relativi al nome del bucket [!DNL Amazon S3] e al percorso della cartella in cui verranno depositati i file. Di seguito sono riportati due esempi di input richiesti per una destinazione [!DNL Amazon S3] e una destinazione [!DNL Trade Desk]. Istruzioni dettagliate sull’input richiesto sono fornite in ogni pagina della documentazione di destinazione.

>[!IMPORTANT]
>
>Le immagini seguenti sono utilizzate solo a scopo illustrativo. I dettagli della connessione di destinazione variano tra le destinazioni. Per informazioni dettagliate sui dettagli di connessione per la destinazione, leggere la sezione **Connetti alla destinazione** in ogni [pagina del catalogo di destinazione](../catalog/overview.md) (ad esempio, [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect) o [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)).

**[!DNL Amazon S3]parametri di input obbligatori e facoltativi**

![Immagine che mostra i parametri di input obbligatori e facoltativi durante la connessione a una destinazione Amazon S3.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]parametri di input obbligatori e facoltativi**

![Immagine che mostra i parametri di input obbligatori e facoltativi durante la connessione a una destinazione Trade Desk.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### Impostare le opzioni di formattazione per i file esportati {#file-formatting-and-compression-options}

Per le destinazioni basate su file, puoi configurare varie impostazioni relative al modo in cui i file esportati vengono formattati e compressi. Per ulteriori informazioni su tutte le opzioni di formattazione e compressione disponibili, leggere l&#39;esercitazione [Configurare le opzioni di formattazione per le destinazioni basate su file](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![Immagine che mostra la selezione del tipo di file e varie opzioni per i file CSV.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### Imposta la connessione di destinazione per l’attivazione del pubblico, dell’account, dei potenziali clienti o per le esportazioni di set di dati {#segment-activation-or-dataset-exports}

Alcune destinazioni basate su file supportano l’attivazione del pubblico per clienti noti, clienti account o potenziali clienti, nonché le esportazioni di set di dati. Per queste destinazioni, puoi scegliere se creare una connessione che ti consenta di [attivare tipi di pubblico](/help/destinations/ui/activate-batch-profile-destinations.md), [account](/help/destinations/ui/activate-account-audiences.md), [potenziali](/help/destinations/ui/activate-prospect-audiences.md) o [esportare set di dati](/help/destinations/ui/export-datasets.md).

>[!WARNING]
>
>Durante l’esportazione dei set di dati, tieni presente che le esportazioni in file JSON sono supportate solo in modalità compressa. Le esportazioni in file [!DNL Parquet] sono supportate in modalità compressa e non compressa.

![Immagine che mostra il controllo di selezione del tipo di dati che consente agli utenti di scegliere tra l&#39;attivazione del pubblico e le esportazioni del set di dati.](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### Abilita avvisi di destinazione {#enable-alerts}

1. (Facoltativo) Seleziona gli avvisi del flusso di dati di destinazione a cui desideri abbonarti. È possibile abbonarsi agli avvisi durante la creazione di un flusso di dati per ricevere messaggi di avviso relativi allo stato, al completamento o al fallimento dell’esecuzione del flusso. Gli avvisi disponibili variano in base al tipo di destinazione (basata su file o streaming) a cui ti stai connettendo. Leggi [Abbonati agli avvisi contestuali di destinazione](alerts.md) per informazioni dettagliate sugli avvisi di flusso di dati di destinazione.

   ![Finestra di dialogo Configura nuova destinazione con le opzioni di sottoscrizione degli avvisi di destinazione contestuali evidenziate.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. Seleziona **[!UICONTROL Avanti]**.

   ![La finestra di dialogo Configura nuova destinazione con il controllo Successivo evidenziato consente all&#39;utente di procedere al passaggio successivo nel flusso di lavoro.](../assets/ui/connect-destinations/next.png)

## Seleziona azioni di marketing {#select-marketing-actions}

1. Seleziona le azioni di marketing applicabili ai dati da esportare nella destinazione. Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite dall’Adobe oppure creare un’azione di marketing personalizzata. Per ulteriori informazioni sulle azioni di marketing, consulta la pagina [panoramica dei criteri di utilizzo dei dati](../../data-governance/policies/overview.md).

   ![Viene evidenziata la finestra di dialogo Configura nuova destinazione con le azioni di marketing disponibili. Sono evidenziati anche i controlli disponibili per completare il flusso di lavoro Connetti a destinazione.](../assets/ui/connect-destinations/governance.png)

2. Seleziona **[!UICONTROL Salva ed esci]** per salvare la configurazione di destinazione oppure seleziona **[!UICONTROL Avanti]** per passare ai dati del pubblico [flusso di attivazione](activation-overview.md).

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, hai imparato a utilizzare l’interfaccia utente di Experience Platform per stabilire una connessione a una destinazione. I parametri di connessione disponibili e richiesti variano da destinazione a destinazione. È inoltre necessario consultare la pagina della documentazione di destinazione nel [catalogo delle destinazioni](/help/destinations/catalog/overview.md) per informazioni specifiche sugli input richiesti e sulle opzioni disponibili per tipo di destinazione.

Quindi, puoi procedere all&#39;[attivazione dei tipi di pubblico](/help/destinations/ui/activation-overview.md) o all&#39;[esportazione dei set di dati](/help/destinations/ui/export-datasets.md) nella tua destinazione.