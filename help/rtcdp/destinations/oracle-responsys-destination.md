---
title: Destinazione Oracle Responsys
seo-title: Destinazione Oracle Responsys
description: Responsys è uno strumento di marketing e-mail aziendale per campagne di marketing multicanale offerto da Oracle per personalizzare le interazioni tra e-mail, dispositivi mobili, visualizzazione e social.
seo-description: Responsys è uno strumento di marketing e-mail aziendale per campagne di marketing multicanale offerto da Oracle per personalizzare le interazioni tra e-mail, dispositivi mobili, visualizzazione e social.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Responsys

## Panoramica

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) è uno strumento di marketing e-mail aziendale per campagne di marketing multicanale offerto da Oracle per personalizzare le interazioni tra e-mail, dispositivi mobili, visualizzazione e social.

Per inviare i dati del segmento a Oracle Responsys, è innanzitutto necessario [collegare la destinazione](#connect-destination) in Adobe Real-time Customer Data Platform, quindi [impostare un&#39;importazione](#import-data-into-responsys) di dati dalla posizione di archiviazione in Oracle Responsys.

## Destinazione Connect {#connect-destination}

1. In **[!UICONTROL Connessioni > Destinazioni]**, selezionare Oracle Responsys, quindi selezionare la destinazione **[!UICONTROL di]** Connect.

   ![Connetti alle risposte](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

1. Nella procedura guidata di destinazione di Connect, selezionate il tipo **[!UICONTROL di]** connessione per il percorso di memorizzazione. Per Oracle Responsys, è possibile scegliere tra **SFTP con password** e **SFTP con chiave** SSH. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, e seleziona **[!UICONTROL Connect]**.

   ![Impostazione della procedura guidata Risposte](/help/rtcdp/destinations/assets/responsys-wizard.png)

   Per **SFTP con connessioni con password** , dovete fornire Domain, Port, UserName e Password.
Per **SFTP con connessioni chiavi** SSH, dovete fornire Domain, Port, Username e Chiave SSH.

   ![Compila le informazioni sulle risposte](/help/rtcdp/destinations/assets/responsys-step2.png)

1. In Informazioni **** di base, compila le informazioni relative alla tua destinazione, come indicato di seguito:
   * **Nome**: Scegli un nome appropriato per la tua destinazione.
   * **Descrizione**: Inserite una descrizione per la destinazione.
   * **Percorso** cartella: Specificate il percorso nel percorso di archiviazione in cui CDP in tempo reale depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
   * **Formato** file: **CSV** o **TAB_DELIMITED**. Selezionare il formato di file da esportare nel percorso di memorizzazione.
   ![Rispondi alle informazioni di base](/help/rtcdp/destinations/assets/responsys-basic-information.png)

1. Fate clic su **Crea** dopo aver compilato i campi in Informazioni **di** base. La destinazione è ora connessa e puoi [attivare i segmenti](/help/rtcdp/destinations/activate-destinations.md) alla destinazione.

## Attributi di destinazione {#destination-attributes}

Quando si [attivano i segmenti](/help/rtcdp/destinations/activate-destinations.md) alla destinazione Oracle Responsys, è consigliabile selezionare un identificatore univoco dallo schema [](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)unione. Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, vedere [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) esportati in Destinazioni di marketing e-mail.

## Impostazione dell&#39;importazione di dati in Oracle Responsys {#import-data-into-responsys}

Dopo aver collegato CDP in tempo reale allo storage Amazon S3 o SFTP, è necessario impostare l&#39;importazione dei dati dalla posizione di archiviazione in Oracle Responsys. Per informazioni su come eseguire questa operazione, vedere [Importazione di contatti o account](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in Oracle Responsys Help Center.