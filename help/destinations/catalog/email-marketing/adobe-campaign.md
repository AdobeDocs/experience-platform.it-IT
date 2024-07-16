---
keywords: e-mail;e-mail;destinazioni e-mail;adobe campaign;campaign
title: Connessione Adobe Campaign
description: Adobe Campaign è un insieme di soluzioni che consentono di personalizzare e distribuire campagne su tutti i canali online e offline.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 5%

---

# Connessione Adobe Campaign

## Panoramica {#overview}

Adobe Campaign è un insieme di soluzioni che ti aiutano a personalizzare e distribuire campagne su tutti i canali online e offline. Per ulteriori informazioni, vedere [Introduzione a Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Per inviare dati sul pubblico ad Adobe Campaign, devi prima [connettere la destinazione](#connect-destination) in Adobe Experience Platform, quindi [configurare un&#39;importazione dati](#import-data-into-campaign) dal percorso di archiviazione in Adobe Campaign.

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Indirizzo IP inserisco nell&#39;elenco Consentiti {#allow-list}

Quando configuri le destinazioni di e-mail marketing con l’archiviazione SFTP, l’Adobe inserii nell&#39;elenco Consentiti consiglia di aggiungere determinati intervalli IP al tuo.

Se hai bisogno di aggiungere IP Adobi al inserisco nell&#39;elenco Consentiti di, consulta la [inserisce nell&#39;elenco Consentiti di indirizzi IP per le destinazioni SFTP](../cloud-storage/ip-address-allow-list.md).

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Gestione destinazioni]** [controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

Adobe Campaign supporta i seguenti tipi di connessione:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP con password]**
* **[!UICONTROL SFTP con chiave SSH]**
* **[!UICONTROL BLOB di Azure]**

Il metodo preferito per inviare dati ad Adobe Campaign è tramite [!DNL Amazon S3] o [!DNL Azure Blob].

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* Per le **[!UICONTROL connessioni Amazon S3]**, è necessario fornire [!UICONTROL ID chiave di accesso] e [!UICONTROL Chiave di accesso segreta].
* Per **[!UICONTROL SFTP con connessioni Password]**, è necessario fornire [!UICONTROL Dominio], [!UICONTROL Porta], [!UICONTROL Nome utente] e [!UICONTROL Password].
* Per **[!UICONTROL SFTP con connessioni chiave SSH]**, è necessario fornire [!UICONTROL Dominio], [!UICONTROL Porta], [!UICONTROL Nome utente] e [!UICONTROL Chiave SSH].
* Per **[!UICONTROL connessioni BLOB di Azure]**, è necessario specificare una stringa di connessione.
* In alternativa, è possibile allegare la chiave pubblica in formato RSA per aggiungere la crittografia con PGP/GPG ai file esportati nella sezione **[!UICONTROL Chiave]**. La chiave pubblica deve essere scritta come stringa con codifica [!DNL Base64].
* **[!UICONTROL Nome]**: scegliere un nome appropriato per la destinazione.
* **[!UICONTROL Descrizione]**: immetti una descrizione per la destinazione.
* **[!UICONTROL Nome Bucket]**: *Per connessioni S3*. Immetti il percorso del bucket S3 in cui [!DNL Platform] depositerà i dati di esportazione come file CSV.
* **[!UICONTROL Percorso cartella]**: fornisci il percorso nel percorso di archiviazione in cui [!DNL Platform] depositerà i dati di esportazione come file CSV.
* **[!UICONTROL Contenitore]**: *Per connessioni BLOB*. Il contenitore che contiene il BLOB nel percorso della cartella si trova in.
* **[!UICONTROL Formato file]**: seleziona **CSV** per esportare i file CSV nel percorso di archiviazione.

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

Per [!DNL Adobe Campaign] destinazioni, [!DNL Platform] crea un file `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta la sezione [verifica attivazione pubblico](../../ui/activate-batch-profile-destinations.md#verify) nell&#39;esercitazione di attivazione pubblico.

## Configurare l’importazione dei dati in Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Durante l&#39;esecuzione di questa integrazione, tieni presente i limiti di archiviazione [!DNL SFTP], i limiti di archiviazione del database e i limiti del profilo attivo in base al tuo contratto Adobe Campaign.
>* È necessario pianificare, importare e mappare i segmenti esportati in Adobe Campaign utilizzando [!DNL Campaign] flussi di lavoro. Consulta [Configurazione di un&#39;importazione ricorrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) nella documentazione di Adobe Campaign Classic e [Informazioni sulle attività di gestione dati](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) nella documentazione di Adobe Campaign Standard.
>* Il metodo preferito per inviare dati ad Adobe Campaign è tramite [!DNL Amazon S3] o [!DNL Azure Blob].

Dopo aver connesso [!DNL Platform] all&#39;archivio [!DNL Amazon S3] o [!DNL Azure Blob], è necessario configurare l&#39;importazione dei dati dal percorso di archiviazione in Adobe Campaign. Per informazioni su come eseguire questa operazione, consulta le seguenti pagine della documentazione di Adobe Campaign:
* [Introduzione all&#39;importazione ed esportazione dei dati](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=it) e [Caricamento dei dati (file)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) nella documentazione di Adobe Campaign Classic.
* [Introduzione ai processi e alla gestione dei dati](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) e [Carica file](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) nella documentazione di Adobe Campaign Standard.
