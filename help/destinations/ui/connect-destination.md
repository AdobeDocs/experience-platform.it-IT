---
title: Creare una nuova connessione di destinazione
type: Tutorial
description: Scopri come connettersi a una destinazione in Adobe Experience Platform, abilitare gli avvisi e impostare azioni di marketing per la destinazione connessa.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 0%

---

# Creare una nuova connessione di destinazione

>[!IMPORTANT]
> 
>* Per connettersi a una destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per connettersi a una destinazione che supporta le esportazioni di set di dati, è necessario **[!UICONTROL Gestire e attivare le destinazioni dei set di dati]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

## Panoramica {#overview}

Prima di poter inviare dati sul pubblico a una destinazione, devi impostare una connessione alla piattaforma di destinazione. Questo articolo mostra come impostare una nuova connessione di destinazione, alla quale è quindi possibile attivare i tipi di pubblico o esportare i set di dati utilizzando l’interfaccia utente di Adobe Experience Platform.

## Trovare la destinazione desiderata nel catalogo {#setup}

1. Vai a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]**, e seleziona la **[!UICONTROL Catalogo]** scheda.

   ![Schermata dell’interfaccia utente di Experience Platform che mostra la pagina del catalogo delle destinazioni.](../assets/ui/connect-destinations/catalog.png)

2. Le schede di destinazione nel catalogo possono avere controlli di azione diversi, a seconda che tu disponga di una connessione esistente alla destinazione e che le destinazioni supportino l’attivazione di tipi di pubblico, l’esportazione di set di dati o entrambi. Potresti visualizzare uno dei seguenti controlli per le schede di destinazione:

   * **[!UICONTROL Configurazione]**. Prima di poter attivare i tipi di pubblico o esportare i set di dati, è necessario impostare una connessione a questa destinazione.
   * **[!UICONTROL Attiva]**. Connessione già impostata a questa destinazione. Questa destinazione supporta l’attivazione del pubblico e le esportazioni di set di dati.
   * **[!UICONTROL Attiva tipi di pubblico]**. Connessione già impostata a questa destinazione. Questa destinazione supporta solo l’attivazione del pubblico.

   Per ulteriori informazioni sulle differenze tra questi controlli, è inoltre possibile fare riferimento alla [Catalogo](../ui/destinations-workspace.md#catalog) sezione della documentazione di workspace di destinazione.

   Seleziona una **[!UICONTROL Configurazione]**, **[!UICONTROL Attiva]**, o **[!UICONTROL Attiva tipi di pubblico]**, a seconda del controllo disponibile.

   ![Schermata dell’interfaccia utente di Experience Platform che mostra la pagina del catalogo delle destinazioni con il controllo Configura evidenziato.](../assets/ui/connect-destinations/set-up.png)

   ![Schermata dell’interfaccia utente di Experience Platform che mostra la pagina del catalogo delle destinazioni in cui è evidenziato il controllo Attiva pubblico.](../assets/ui/connect-destinations/activate-segments.png)

3. Se hai selezionato **[!UICONTROL Configurazione]**, passa al passaggio successivo, per [autenticare](#authenticate) alla destinazione.

   Se hai selezionato **[!UICONTROL Attiva]**, **[!UICONTROL Attiva tipi di pubblico]**, o **[!UICONTROL Esportare i set di dati]**, è ora disponibile un elenco delle connessioni di destinazione esistenti.

   Seleziona **[!UICONTROL Configurare una nuova destinazione]** per stabilire una nuova connessione alla destinazione.

   ![Schermata dell’interfaccia utente di Experience Platform che mostra un elenco di destinazioni disponibili ed evidenzia il controllo Configura nuova destinazione.](../assets/ui/connect-destinations/configure-new-destination.png)

## Autenticarsi nella destinazione {#authenticate}

Il primo passaggio nella connessione a una destinazione consiste nell’eseguire l’autenticazione nella piattaforma di destinazione.

A seconda della destinazione a cui ti stai connettendo, potresti essere reindirizzato alla pagina del partner di destinazione per l’autenticazione oppure ti potrebbe essere richiesto di immettere le credenziali di autenticazione direttamente nel flusso di lavoro di Platform. Di seguito è riportato un esempio di input necessario per l&#39;autenticazione in un [!DNL Amazon S3] destinazione. Istruzioni dettagliate sull’input richiesto sono fornite in ogni pagina della documentazione di destinazione (vedi, ad esempio, la sezione autenticazione per [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) e per [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)).

**[!DNL Amazon S3]parametri di autenticazione obbligatori e facoltativi**

![Immagine che mostra i parametri di input obbligatori e facoltativi durante l’autenticazione in una destinazione Amazon S3.](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## Impostare i parametri di connessione {#set-up-connection-parameters}

Se hai già impostato l’autenticazione per la destinazione, puoi continuare con l’account esistente oppure puoi impostarne uno nuovo.

A seconda della destinazione a cui ti stai connettendo, potrebbe essere richiesto di immettere diversi tipi di parametri di connessione. Ad esempio, quando ci si connette a un [!DNL Amazon S3] destinazione, ti viene chiesto di fornire dettagli relativi al [!DNL Amazon S3] nome del bucket e percorso della cartella in cui verranno depositati i file. Di seguito sono riportati due esempi di input richiesti per un [!DNL Amazon S3] destinazione e un [!DNL Trade Desk] destinazione. Istruzioni dettagliate sull’input richiesto sono fornite in ogni pagina della documentazione di destinazione.

>[!IMPORTANT]
>
>Le immagini seguenti sono utilizzate solo a scopo illustrativo. I dettagli della connessione di destinazione variano tra le destinazioni. Per informazioni dettagliate sui dettagli di connessione per la destinazione, leggere **Connetti alla destinazione** sezione in ogni [catalogo di destinazione](../catalog/overview.md) pagina (ad esempio, [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect), o [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)).

**[!DNL Amazon S3]parametri di input obbligatori e opzionali**

![Immagine che mostra i parametri di input richiesti e opzionali durante la connessione a una destinazione Amazon S3.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]parametri di input obbligatori e opzionali**

![Immagine che mostra i parametri di input richiesti e opzionali durante il collegamento a una destinazione Trade Desk.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### Impostare le opzioni di formattazione per i file esportati {#file-formatting-and-compression-options}

Per le destinazioni basate su file, puoi configurare varie impostazioni relative al modo in cui i file esportati vengono formattati e compressi. Per ulteriori informazioni su tutte le opzioni di formattazione e compressione disponibili, vedere [Tutorial su come configurare le opzioni di formattazione per le destinazioni basate su file](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![Immagine che mostra la selezione del tipo di file e varie opzioni per i file CSV.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### Imposta la connessione di destinazione per l’attivazione del pubblico, dell’account, dei potenziali clienti o per le esportazioni di set di dati {#segment-activation-or-dataset-exports}

Alcune destinazioni basate su file supportano l’attivazione del pubblico per clienti noti, clienti account o potenziali clienti, nonché le esportazioni di set di dati. Per tali destinazioni, puoi scegliere se creare una connessione che ti consenta di: [attivare i tipi di pubblico](/help/destinations/ui/activate-batch-profile-destinations.md), [account](/help/destinations/ui/activate-account-audiences.md), [potenziali clienti](/help/destinations/ui/activate-prospect-audiences.md), o [esportare i set di dati](/help/destinations/ui/export-datasets.md).

>[!WARNING]
>
>Durante l’esportazione dei set di dati, tieni presente che le esportazioni in file JSON sono supportate solo in modalità compressa. Esporta in [!DNL Parquet] i file sono supportati in modalità compressa e non compressa.

![Immagine che mostra il controllo per la selezione del tipo di dati, che consente agli utenti di scegliere tra l’attivazione del pubblico e le esportazioni di set di dati.](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### Abilita avvisi di destinazione {#enable-alerts}

1. (Facoltativo) Seleziona gli avvisi del flusso di dati di destinazione a cui desideri abbonarti. È possibile abbonarsi agli avvisi durante la creazione di un flusso di dati per ricevere messaggi di avviso relativi allo stato, al completamento o al fallimento dell’esecuzione del flusso. Gli avvisi disponibili variano in base al tipo di destinazione (basata su file o streaming) a cui ti stai connettendo. Letto [Iscriviti agli avvisi contestuali sulle destinazioni](alerts.md) per informazioni dettagliate sugli avvisi del flusso di dati di destinazione.

   ![La finestra di dialogo Configura nuova destinazione con le opzioni di abbonamento degli avvisi di destinazione contestuali evidenziate.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. Seleziona **[!UICONTROL Avanti]**.

   ![Viene evidenziata la finestra di dialogo Configura nuova destinazione con il controllo Successivo, che consente all’utente di procedere al passaggio successivo nel flusso di lavoro.](../assets/ui/connect-destinations/next.png)

## Seleziona azioni di marketing {#select-marketing-actions}

1. Seleziona le azioni di marketing applicabili ai dati da esportare nella destinazione. Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite dall’Adobe oppure creare un’azione di marketing personalizzata. Per ulteriori informazioni sulle azioni di marketing, vedi [panoramica dei criteri di utilizzo dei dati](../../data-governance/policies/overview.md) pagina.

   ![La finestra di dialogo Configura nuova destinazione con le azioni di marketing disponibili evidenziate. Vengono evidenziati anche i controlli disponibili per completare il flusso di lavoro Connetti a destinazione.](../assets/ui/connect-destinations/governance.png)

2. Seleziona **[!UICONTROL Salva ed esci]** per salvare la configurazione di destinazione, oppure seleziona **[!UICONTROL Successivo]** per passare ai dati sul pubblico [flusso di attivazione](activation-overview.md).

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, hai imparato a utilizzare l’interfaccia utente di Experienci Platform per stabilire una connessione a una destinazione. I parametri di connessione disponibili e richiesti variano da destinazione a destinazione. È inoltre necessario consultare la pagina della documentazione di destinazione in [catalogo delle destinazioni](/help/destinations/catalog/overview.md) per informazioni specifiche sugli input richiesti e sulle opzioni disponibili per tipo di destinazione.

Quindi, puoi procedere a [attivazione di tipi di pubblico](/help/destinations/ui/activation-overview.md) o [esportazione di set di dati](/help/destinations/ui/export-datasets.md) a destinazione.