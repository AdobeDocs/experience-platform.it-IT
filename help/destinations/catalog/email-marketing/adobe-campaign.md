---
keywords: e-mail;e-mail;e-mail;destinazioni;adobe campaign;campaign
title: Connessione Adobe Campaign
description: Adobe Campaign è un set di soluzioni che consentono di personalizzare e distribuire campagne su tutti i canali online e offline.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---


# Connessione Adobe Campaign

Adobe Campaign è un set di soluzioni che consentono di personalizzare e distribuire campagne su tutti i canali online e offline. Per ulteriori informazioni, consulta [Introduzione a Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) .

Per inviare i dati dei segmenti ad Adobe Campaign, è necessario prima [collegare la destinazione](#connect-destination) in Adobe Experience Platform, quindi [impostare un&#39;importazione di dati](#import-data-into-campaign) dalla posizione di archiviazione in Adobe Campaign.

## Tipo di esportazione {#export-type}

**Basato su profilo** : stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nel  **[!UICONTROL Select attributes]** passaggio del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

## Collegare la destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleziona Adobe Campaign, quindi seleziona **[!UICONTROL Configure]**.

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra [!UICONTROL Activate] e [!UICONTROL Configure], consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

![Connettersi ad Adobe Campaign](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Nel passaggio **[!UICONTROL Account]** del flusso di lavoro di destinazione Connetti , seleziona **[!UICONTROL Connection type]** per il percorso di archiviazione. Per Adobe Campaign, puoi selezionare tra **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP with Password]**, **[!UICONTROL SFTP with SSH Key]** e **[!UICONTROL Azure Blob]**. Il metodo preferito per inviare dati ad Adobe Campaign è tramite [!DNL Amazon S3] o [!DNL Azure Blob]. Compila le informazioni seguenti, a seconda del tipo di connessione, quindi seleziona **[!UICONTROL Connect]**.


![Configurazione guidata Campaign](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Per le connessioni **[!UICONTROL Amazon S3]**, devi fornire il tuo ID chiave di accesso e la chiave di accesso segreto.
- Per le connessioni **[!UICONTROL SFTP with Password]**, è necessario specificare Dominio, Porta, Nome utente e Password.
- Per le connessioni **[!UICONTROL SFTP with SSH Key]**, è necessario specificare Dominio, Porta, Nome utente e Chiave SSH.
- Per le connessioni **[!UICONTROL Azure Blob]**, è necessario fornire una stringa di connessione.

Facoltativamente, puoi allegare la tua chiave pubblica in formato RSA per aggiungere la crittografia con PGP/GPG ai file esportati nella sezione **[!UICONTROL Key]** . Tieni presente che questa chiave pubblica **deve** essere scritta come stringa codificata Base64.

![Compila le informazioni di Campaign](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

In **[!UICONTROL Account authentication]**, compila le informazioni rilevanti per la tua destinazione, come mostrato di seguito:
- **[!UICONTROL Name]**: Scegli un nome appropriato per la destinazione.
- **[!UICONTROL Description]**: Inserisci una descrizione per la destinazione.
- **[!UICONTROL Bucket Name]**:  *Per connessioni* S3. Immetti la posizione del bucket S3 in cui [!DNL Platform] depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
- **[!UICONTROL Folder Path]**: Fornisci il percorso nel percorso di archiviazione in cui  [!DNL Platform] verranno depositati i dati di esportazione come file CSV o delimitati da tabulazioni.
- **[!UICONTROL Container]**:  *Per connessioni* Blob. Il contenitore contenente il BLOB nel percorso della cartella è in.
- **[!UICONTROL File Format]**:  **** CSVo  **TAB_DELIMITTED**. Selezionare il formato di file da esportare nel percorso di archiviazione.
- **[!UICONTROL Marketing actions]**: Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la pagina [Panoramica dei criteri di utilizzo dei dati](../../../data-governance/policies/overview.md) . Consulta anche [azioni di marketing definite in Adobe](../../../data-governance/policies/overview.md#core-actions) nello stesso documento.

![Informazioni di base su Campaign](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Selezionare **[!UICONTROL Create destination]** dopo aver compilato i campi precedenti. La destinazione è ora connessa ed è possibile [attivare segmenti](../../ui/activate-destinations.md) alla destinazione.

## Attiva segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, consulta [Attivare profili e segmenti su una destinazione](../../ui/activate-destinations.md) .

## Attributi di destinazione {#destination-attributes}

Quando si attivano [segmenti](../../ui/activate-destinations.md) nella destinazione Adobe Campaign, si consiglia di selezionare un identificatore univoco dal [schema di unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, consulta [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file esportati](./overview.md#destination-attributes) nella documentazione sulle destinazioni di marketing e-mail.

## Dati esportati {#exported-data}

Per le destinazioni [!DNL Adobe Campaign], [!DNL Platform] crea un file `.txt` o `.csv` delimitato da tabulazioni nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [Destinazioni di e-mail marketing e destinazioni di archiviazione Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell’esercitazione sull’attivazione dei segmenti.

## Configurare l’importazione di dati in Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Tieni presente i limiti di archiviazione SFTP, i limiti di archiviazione del database e i limiti dei profili attivi in base al contratto Adobe Campaign durante l’esecuzione di questa integrazione.
>- Devi pianificare, importare e mappare i segmenti esportati in Adobe Campaign utilizzando i flussi di lavoro [!DNL Campaign] . Consulta [Impostazione di un&#39;importazione ricorrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) nella documentazione di Adobe Campaign Classic e [Informazioni sulle attività di gestione dati](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) nella documentazione di Adobe Campaign Standard.
>- Il metodo preferito per inviare dati ad Adobe Campaign è tramite [!DNL Amazon S3] o [!DNL Azure Blob].



Dopo aver effettuato la connessione di [!DNL Platform] allo storage [!DNL Amazon S3] o [!DNL Azure Blob], è necessario impostare l&#39;importazione dei dati dal percorso di archiviazione in Adobe Campaign. Per informazioni su come eseguire questa operazione, consulta le seguenti pagine di documentazione di Adobe Campaign:
- [Guida introduttiva all’importazione, all’](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html) esportazione e al caricamento  [dei dati (file)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html)  nella documentazione di Adobe Campaign Classic.
- [Guida introduttiva ai processi e alla ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) gestione dei dati e al  [caricamento ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) dei file nella documentazione di Adobe Campaign Standard.