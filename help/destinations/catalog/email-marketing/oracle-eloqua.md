---
keywords: e-mail;e-mail;destinazioni e-mail;oracle eloqua;oracle
title: (File) Connessione Oracle Eloqua
description: Oracle Eloqua è una piattaforma SaaS (software as a service) per l’automazione del marketing offerta da Oracle che ha lo scopo di aiutare gli esperti di marketing B2B e le organizzazioni a gestire campagne di marketing e la generazione di lead di vendita.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 3%

---

# Connessione [!DNL (Files) Oracle Eloqua]

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) è una piattaforma SaaS (Software as a Service) per l&#39;automazione del marketing offerta da [!DNL Oracle] che ha lo scopo di aiutare gli addetti al marketing B2B e le organizzazioni a gestire le campagne di marketing e la generazione di lead di vendita.

Per inviare i dati del pubblico a [!DNL Oracle Eloqua], devi prima [connettere la destinazione](#connect-destination) in Adobe Experience Platform, quindi [configurare un&#39;importazione dati](#import-data-into-eloqua) dal percorso di archiviazione in [!DNL Oracle Eloqua].

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## ELENCO CONSENTITI di indirizzo IP {#allow-list}

Quando configuri le destinazioni di e-mail marketing con l’archiviazione SFTP, Adobe consiglia di aggiungere determinati intervalli IP all’elenco consentiti.

Se devi aggiungere degli IP Adobe elenco consentiti all&#39;elenco consentiti, consulta l&#39;[indirizzo IP per le destinazioni SFTP](../cloud-storage/ip-address-allow-list.md).

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Gestione destinazioni]** [controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

Questa destinazione supporta i seguenti tipi di connessione:

* **[!UICONTROL SFTP con password]**
* **[!UICONTROL SFTP con chiave SSH]**

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* Per le connessioni **[!UICONTROL SFTP con password]**, è necessario fornire:
   * [!UICONTROL Dominio]
   * [!UICONTROL Porta]
   * [!UICONTROL Nome utente]
   * [!UICONTROL Password]
* Per **[!UICONTROL SFTP con connessioni chiave SSH]**, è necessario fornire:
   * [!UICONTROL Dominio]
   * [!UICONTROL Porta]
   * [!UICONTROL Nome utente]
   * [!UICONTROL Chiave SSH]

* In alternativa, è possibile allegare la chiave pubblica in formato RSA per aggiungere la crittografia con PGP/GPG ai file esportati nella sezione **[!UICONTROL Chiave]**. La chiave pubblica deve essere scritta come stringa con codifica [!DNL Base64].
* **[!UICONTROL Nome]**: scegliere un nome appropriato per la destinazione.
* **[!UICONTROL Descrizione]**: immetti una descrizione per la destinazione.
* **[!UICONTROL Percorso cartella]**: specifica il percorso nel percorso di archiviazione in cui Experience Platform depositerà i dati di esportazione come file CSV.
* **[!UICONTROL Formato file]**: seleziona **CSV** per esportare i file CSV nel percorso di archiviazione.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione profilo batch](../../ui/activate-batch-profile-destinations.md).

### Attributi di destinazione {#destination-attributes}

Quando si attivano i tipi di pubblico in questa destinazione, Adobe consiglia di selezionare un identificatore univoco dallo [schema di unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, consulta [best practice per l&#39;attivazione dei tipi di pubblico nelle destinazioni del marketing via e-mail](overview.md#best-practices).

## Dati esportati {#exported-data}

Per le destinazioni [!DNL Oracle Eloqua], Experience Platform crea un file `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedi [verificare l&#39;attivazione del pubblico](../../ui/activate-batch-profile-destinations.md#verify) nell&#39;esercitazione di attivazione del pubblico.

## Configura l&#39;importazione dei dati in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Dopo aver connesso [!DNL Experience Platform] all&#39;archivio [!DNL SFTP], è necessario configurare l&#39;importazione dei dati dal percorso di archiviazione in [!DNL Oracle Eloqua]. Per informazioni su come eseguire questa operazione, vedere [Importazione di contatti o account](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in [!DNL Oracle Eloqua Help Center].
