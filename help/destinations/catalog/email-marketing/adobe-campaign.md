---
keywords: email;Email;e-mail;email destinations;adobe campaign;campaign
title: Adobe Campaign
seo-title: Adobe Campaign
description: ' Adobe Campaign è un insieme di soluzioni che consentono di personalizzare e distribuire campagne su tutti i canali online e offline.'
seo-description: ' Adobe Campaign è un insieme di soluzioni che consentono di personalizzare e distribuire campagne su tutti i canali online e offline.'
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---


# Adobe Campaign

## Panoramica

 Adobe Campaign è un insieme di soluzioni che consentono di personalizzare e distribuire campagne su tutti i canali online e offline. Per ulteriori informazioni, consultate [Informazioni su Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) .

Per inviare i dati del segmento a  Adobe Campaign, è innanzitutto necessario [collegare la destinazione](#connect-destination) in Real-time Customer Data Platform, quindi [impostare un&#39;importazione](#import-data-into-campaign) di dati dalla posizione di archiviazione in  Adobe Campaign.

## Tipo esportazione {#export-type}

**Basato** su profilo: si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata degli attributi selezionati del flusso di lavoro [di attivazione della](../../ui/activate-destinations.md#select-attributes)destinazione.

## Destinazione Connect {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionate  Adobe Campaign, quindi selezionate **[!UICONTROL Connect destination]**.

![Connetti ad adobe campaign](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Nel flusso di lavoro di destinazione di Connect, selezionate il percorso **[!UICONTROL Connection type]** di memorizzazione. Per  Adobe Campaign, potete scegliere tra **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, quindi seleziona **[!UICONTROL Connect]**.

![Configurazione guidata campagna](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Per **[!UICONTROL Amazon S3]** le connessioni, dovete fornire il vostro ID chiave di accesso e la chiave di accesso segreta.
- Per **[!UICONTROL SFTP with Password]** le connessioni, dovete fornire Domain, Port, UserName e Password.
- Per **[!UICONTROL SFTP with SSH Key]** le connessioni, è necessario fornire Domain, Port, Username e SSH Key.

Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia con PGP/GPG ai file esportati nella **[!UICONTROL Key]** sezione. Questa chiave pubblica **deve** essere scritta come una stringa codificata Base64.

![Compila le informazioni sulla campagna](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

In **[!UICONTROL Basic Information]**, compila le informazioni pertinenti per la tua destinazione, come mostrato di seguito:
- **[!UICONTROL Name]**: Scegli un nome appropriato per la tua destinazione.
- **[!UICONTROL Description]**: Inserite una descrizione per la destinazione.
- **[!UICONTROL Bucket Name]**: *Per connessioni* S3. Immettete la posizione del bucket S3 in cui CDP in tempo reale depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
- **[!UICONTROL Folder Path]**: Specificate il percorso nel percorso di archiviazione in cui CDP in tempo reale depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
- **[!UICONTROL File Format]**: **CSV** o **TAB_DELIMITED**. Selezionare il formato di file da esportare nel percorso di memorizzazione.

![Informazioni di base sulla campagna](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Fare clic **[!UICONTROL Create]** dopo aver compilato i campi sopra. La destinazione è ora connessa e puoi [attivare i segmenti](../../ui/activate-destinations.md) alla destinazione.

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](../../ui/activate-destinations.md) per informazioni sul flusso di lavoro di attivazione dei segmenti.

## Attributi di destinazione {#destination-attributes}

Quando si [attivano i segmenti](../../ui/activate-destinations.md) nella destinazione Adobe Campaign , si consiglia di selezionare un identificatore univoco dallo schema [](../../../profile/home.md#profile-fragments-and-union-schemas)unione. Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, consulta [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file](./overview.md#destination-attributes) esportati nella documentazione delle destinazioni di e-mail marketing.

## Dati esportati {#exported-data}

Per [!DNL Adobe Campaign] le destinazioni, in Real-time CDP viene creato un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di memorizzazione specificato. Per ulteriori informazioni sui file, vedi Destinazioni di marketing [e-mail e destinazioni](../../ui/activate-destinations.md#esp-and-cloud-storage) di archiviazione cloud nell&#39;esercitazione sull&#39;attivazione del segmento.

## Configurare l&#39;importazione di dati in  Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Ricorda i limiti di archiviazione SFTP, i limiti di archiviazione del database e i limiti di profilo attivi come previsto dal contratto Adobe Campaign  durante l&#39;esecuzione di questa integrazione.
>- Devi pianificare, importare e mappare i segmenti esportati in  Adobe Campaign utilizzando [!DNL Campaign] i flussi di lavoro. Consultate [Impostazione di un&#39;importazione](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows) ricorrente nella documentazione  Adobe Campaign.



Dopo aver collegato CDP in tempo reale allo storage [!DNL Amazon S3] o SFTP, è necessario impostare l&#39;importazione dei dati dalla posizione di archiviazione in  Adobe Campaign. Per informazioni su come eseguire questa operazione, consultare [Importazione di dati](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) nella documentazione Adobe Campaign .