---
keywords: collegare destinazione;connessione destinazione;come collegare destinazione
title: Crea una nuova connessione di destinazione
type: Tutorial
description: Scopri come connettersi a una destinazione in Adobe Experience Platform, abilitare gli avvisi e impostare azioni di marketing per la destinazione connessa.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 434b9ed4f64320b5fd73b752716cb34a8e48aec9
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# Crea una nuova connessione di destinazione

>[!IMPORTANT]
> 
>* Per connettersi a una destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.
>* Per connettersi a una destinazione che supporta le esportazioni di set di dati, è necessario **[!UICONTROL Gestire e attivare le destinazioni del set di dati]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.


## Panoramica {#overview}

Prima di poter inviare i dati sul pubblico a una destinazione, è necessario impostare una connessione alla piattaforma di destinazione. Questo articolo illustra come impostare una nuova connessione di destinazione, alla quale è quindi possibile attivare segmenti o esportare set di dati utilizzando l’interfaccia utente di Adobe Experience Platform.

## Trova la destinazione desiderata nel catalogo {#setup}

1. Vai a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]**, quindi seleziona la **[!UICONTROL Catalogo]** scheda .

   ![Schermata dell’interfaccia utente Experience Platform, che mostra la pagina del catalogo delle destinazioni.](../assets/ui/connect-destinations/catalog.png)

2. Le schede di destinazione nel catalogo possono avere controlli di azione diversi, a seconda che si disponga di una connessione esistente alla destinazione e se le destinazioni supportano l’attivazione dei segmenti, l’esportazione dei set di dati o entrambi. Per le schede di destinazione potrebbe essere visualizzato uno dei seguenti controlli:

   * **[!UICONTROL Configurazione]**. Prima di attivare segmenti o esportare set di dati, è necessario impostare una connessione a questa destinazione.
   * **[!UICONTROL Attiva]**. È già stata impostata una connessione per questa destinazione. Questa destinazione supporta l’attivazione dei segmenti e le esportazioni dei set di dati.
   * **[!UICONTROL Attivare i segmenti]**. È già stata impostata una connessione per questa destinazione. Questa destinazione supporta solo l’attivazione dei segmenti.

   Per ulteriori informazioni sulla differenza tra questi controlli, puoi anche fare riferimento alla [Catalogo](../ui/destinations-workspace.md#catalog) sezione della documentazione dell’area di lavoro di destinazione.

   Seleziona o **[!UICONTROL Configurazione]**, **[!UICONTROL Attiva]** oppure **[!UICONTROL Attivare i segmenti]**, a seconda del controllo disponibile.

   ![Schermata dell’interfaccia utente Experience Platform, che mostra la pagina del catalogo delle destinazioni con il controllo Imposta evidenziato.](../assets/ui/connect-destinations/set-up.png)

   ![Schermata dell’interfaccia utente Experience Platform, che mostra la pagina del catalogo delle destinazioni con il controllo Attiva segmenti evidenziato.](../assets/ui/connect-destinations/activate-segments.png)

3. Se hai selezionato **[!UICONTROL Configurazione]**, passa al passaggio successivo, a [autenticare](#authenticate) alla destinazione.

   Se hai selezionato **[!UICONTROL Attiva]**, **[!UICONTROL Attivare i segmenti]** oppure **[!UICONTROL Esportare i set di dati]**, puoi visualizzare un elenco delle connessioni di destinazione esistenti.

   Seleziona **[!UICONTROL Configurare una nuova destinazione]** stabilire un nuovo collegamento con la destinazione.

   ![Schermata dell’interfaccia utente di Experience Platform, con un elenco delle destinazioni disponibili ed evidenziata la funzione Configura nuova destinazione .](../assets/ui/connect-destinations/configure-new-destination.png)

## Autentica a destinazione {#authenticate}

Il primo passo per la connessione a una destinazione è quello di autenticarsi alla piattaforma di destinazione.

A seconda della destinazione alla quale ti stai connettendo, potresti essere portato alla pagina del partner di destinazione per l’autenticazione, oppure ti potrebbe essere chiesto di immettere le credenziali di autenticazione direttamente nel flusso di lavoro di Platform. Di seguito è riportato un esempio di input necessario per l’autenticazione in un [!DNL Amazon S3] destinazione. Le istruzioni dettagliate sull’input richiesto vengono fornite in ogni pagina della documentazione di destinazione (vedi, ad esempio, la sezione sull’autenticazione per [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) e [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)).

**[!DNL Amazon S3]parametri di autenticazione richiesti e facoltativi**

![Immagine che mostra i parametri di input richiesti e facoltativi durante l’autenticazione in una destinazione Amazon S3.](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## Impostare i parametri di connessione {#set-up-connection-parameters}

Se hai già impostato l&#39;autenticazione per la destinazione, puoi continuare con l&#39;account esistente o impostare un nuovo account.

A seconda della destinazione di connessione, potrebbe essere richiesto di inserire diversi tipi di parametri di connessione. Ad esempio, quando ci si connette a un [!DNL Amazon S3] a destinazione, ti viene chiesto di fornire i dettagli relativi alla [!DNL Amazon S3] nome del bucket e percorso della cartella in cui verranno depositati i file. Di seguito sono riportati due esempi di input necessari per un [!DNL Amazon S3] destinazione e [!DNL Trade Desk] destinazione. Istruzioni dettagliate sull’input richiesto sono fornite in ogni pagina della documentazione di destinazione.

>[!IMPORTANT]
>
>Le immagini seguenti sono utilizzate solo a scopo illustrativo. I dettagli della connessione di destinazione variano tra le destinazioni. Per informazioni dettagliate sui dettagli di connessione per la destinazione, consulta la sezione **Collegati alla destinazione** sezione in ogni [catalogo di destinazione](../catalog/overview.md) (ad esempio, [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect)oppure [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)).

**[!DNL Amazon S3]parametri di input richiesti e opzionali**

![Immagine che mostra i parametri di input richiesti e facoltativi durante la connessione a una destinazione Amazon S3.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]parametri di input richiesti e opzionali**

![Immagine che mostra i parametri di input richiesti e opzionali durante la connessione a una destinazione Trade Desk.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### Impostare le opzioni di formattazione per i file esportati {#file-formatting-and-compression-options}

Per le destinazioni basate su file, puoi configurare varie impostazioni relative alla formattazione e alla compressione dei file esportati. Per ulteriori informazioni su tutte le opzioni di formattazione e compressione disponibili, leggere il [Esercitazione su come configurare le opzioni di formattazione per le destinazioni basate su file](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![Immagine che mostra la selezione del tipo di file e varie opzioni per i file CSV.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### Impostare la connessione di destinazione per l’attivazione dei segmenti o le esportazioni dei set di dati {#segment-activation-or-dataset-exports}

Alcune destinazioni basate su file supportano l’attivazione dei segmenti e le esportazioni di set di dati. Per queste destinazioni, puoi scegliere se creare una connessione che ti consenta di attivare segmenti o esportare set di dati.

![Immagine che mostra il controllo per la selezione del tipo di dati che consente agli utenti di selezionare tra l’attivazione dei segmenti e le esportazioni dei set di dati.](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### Abilitare gli avvisi di destinazione {#enable-alerts}

1. (Facoltativo) Seleziona gli avvisi del flusso di dati di destinazione a cui desideri abbonarti. Puoi abbonarti agli avvisi durante la creazione di un flusso di dati per ricevere messaggi di avviso relativi allo stato, al successo o all’errore dell’esecuzione del flusso. Gli avvisi disponibili variano a seconda del tipo di destinazione (basato su file o in streaming) a cui ti connetti. Leggi [Iscriviti agli avvisi di destinazione nel contesto](alerts.md) per informazioni dettagliate sugli avvisi relativi al flusso di dati di destinazione.

   ![È stata evidenziata la finestra di dialogo Configura nuova destinazione con le opzioni di sottoscrizione avvisi di destinazione contestuali.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. Seleziona **[!UICONTROL Avanti]**.

   ![La finestra di dialogo Configura nuova destinazione con il controllo Successivo evidenziato, che consente all&#39;utente di passare al passaggio successivo nel flusso di lavoro.](../assets/ui/connect-destinations/next.png)

## Selezionare le azioni di marketing {#select-marketing-actions}

1. Seleziona le azioni di marketing applicabili ai dati da esportare nella destinazione. Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la sezione [panoramica dei criteri di utilizzo dei dati](../../data-governance/policies/overview.md) pagina.

   ![Viene evidenziata la finestra di dialogo Configura nuova destinazione con le azioni di marketing disponibili. Vengono inoltre evidenziati i controlli disponibili per completare il flusso di lavoro Connetti a destinazione .](../assets/ui/connect-destinations/governance.png)

2. Seleziona **[!UICONTROL Salva ed esci]** per salvare la configurazione di destinazione, oppure seleziona **[!UICONTROL Successivo]** per passare ai dati sul pubblico [flusso di attivazione](activation-overview.md).

## Passaggi successivi {#next-steps}

Leggendo questo documento, hai imparato a utilizzare l’interfaccia utente di Experience Platform per stabilire una connessione a una destinazione. Come promemoria, i parametri di connessione disponibili e richiesti variano da destinazione a destinazione. È inoltre necessario consultare la pagina della documentazione di destinazione nel [catalogo delle destinazioni](/help/destinations/catalog/overview.md) per informazioni specifiche sugli input richiesti e sulle opzioni disponibili per tipo di destinazione.

Quindi, puoi procedere a [attivazione dei segmenti](/help/destinations/ui/activation-overview.md) o [esportazione di set di dati](/help/destinations/ui/export-datasets.md) alla tua destinazione.