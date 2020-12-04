---
keywords: email;Email;e-mail;email destinations;oracle responsys destination
title: ' destinazione Oracle Responsys'
seo-title: ' destinazione Oracle Responsys'
description: Responsys è uno strumento di marketing e-mail aziendale per campagne di marketing multicanale offerte da  Oracle per personalizzare le interazioni tra e-mail, dispositivi mobili, display e social.
seo-description: Responsys è uno strumento di marketing e-mail aziendale per campagne di marketing multicanale offerte da  Oracle per personalizzare le interazioni tra e-mail, dispositivi mobili, display e social.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---


# [!DNL Oracle Responsys]

## Panoramica

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) è uno strumento di marketing e-mail aziendale per campagne di marketing multicanale offerte [!DNL Oracle] per personalizzare le interazioni tra e-mail, dispositivi mobili, visualizzazione e social network.

Per inviare i dati del segmento a [!DNL Oracle Responsys], è innanzitutto necessario [connettersi alla destinazione](#connect-destination) in Real-time Customer Data Platform, quindi [impostare un&#39;importazione](#import-data-into-responsys) di dati dalla posizione di archiviazione in [!DNL Oracle Responsys].

## Tipo esportazione {#export-type}

**Basato** su profilo: si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata degli attributi selezionati del flusso di lavoro [di attivazione della](../../ui/activate-destinations.md#select-attributes)destinazione.

## Destinazione Connect {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Oracle Responsys], quindi **[!UICONTROL Connect destination]**.

![Connetti alle risposte](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

Nel **[!UICONTROL Authentication]** passaggio, se in precedenza hai impostato una connessione alla destinazione di archiviazione cloud, seleziona **[!UICONTROL Existing Account]** e seleziona una delle tue connessioni esistenti. In alternativa, potete selezionare **[!UICONTROL New Account]** di impostare una nuova connessione. Compilate le credenziali di autenticazione dell&#39;account e selezionate **[!UICONTROL Connect to destination]**. Ad [!DNL Oracle Responsys]esempio, potete scegliere tra **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, e seleziona **[!UICONTROL Connect to destination]**.

Per **[!UICONTROL SFTP with Password]** le connessioni, dovete fornire Domain, Port, UserName e Password.

Per **[!UICONTROL SFTP with SSH Key]** le connessioni, è necessario fornire Domain, Port, Username e SSH Key.

![Compila le informazioni sulle risposte](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

Nel **[!UICONTROL Setup]** passaggio, compila le informazioni rilevanti per la tua destinazione come indicato di seguito:
- **[!UICONTROL Name]**: Scegli un nome appropriato per la tua destinazione.
- **[!UICONTROL Description]**: Inserite una descrizione per la destinazione.
- **[!UICONTROL Folder Path]**: Specificate il percorso nel percorso di archiviazione in cui CDP in tempo reale depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
- **[!UICONTROL File Format]**: **CSV** o **TAB_DELIMITED**. Selezionare il formato di file da esportare nel percorso di memorizzazione.

![Rispondi alle informazioni di base](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Fare clic **[!UICONTROL Create destination]** dopo aver compilato i campi sopra. La destinazione è ora connessa e puoi [attivare i segmenti](../../ui/activate-destinations.md) alla destinazione.

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](../../ui/activate-destinations.md) per informazioni sul flusso di lavoro di attivazione dei segmenti.

## Attributi di destinazione {#destination-attributes}

Quando si [attivano i segmenti](../../ui/activate-destinations.md) alla [!DNL Oracle Responsys] destinazione, si consiglia di selezionare un identificatore univoco dallo schema [](../../../profile/home.md#profile-fragments-and-union-schemas)unione. Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, vedere [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file](./overview.md#destination-attributes) esportati in Destinazioni di marketing e-mail.

## Dati esportati {#exported-data}

Per [!DNL Oracle Responsys] le destinazioni, in Real-time CDP viene creato un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di memorizzazione specificato. Per ulteriori informazioni sui file, vedi Destinazioni di marketing [e-mail e destinazioni](../../ui/activate-destinations.md#esp-and-cloud-storage) di archiviazione cloud nell&#39;esercitazione sull&#39;attivazione del segmento.

## Imposta importazione dati in [!DNL Oracle Responsys] {#import-data-into-responsys}

Dopo aver collegato CDP in tempo reale allo storage [!DNL Amazon S3] o SFTP, è necessario impostare l&#39;importazione dei dati dalla posizione di archiviazione in [!DNL Oracle Responsys]. Per informazioni su come eseguire questa operazione, consulta [Importazione di contatti o account](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) nella [!DNL Oracle Responsys Help Center].