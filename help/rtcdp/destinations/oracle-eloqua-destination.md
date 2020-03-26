---
title: Destinazione Oracle Eloqua
seo-title: Destinazione Oracle Eloqua
description: Oracle Eloqua è un software come piattaforma di servizio (SaaS) per l'automazione del marketing offerto da Oracle che mira ad aiutare gli esperti di marketing e le organizzazioni B2B a gestire le campagne di marketing e la generazione di lead di vendita.
seo-description: Oracle Eloqua è un software come piattaforma di servizio (SaaS) per l'automazione del marketing offerto da Oracle che mira ad aiutare gli esperti di marketing e le organizzazioni B2B a gestire le campagne di marketing e la generazione di lead di vendita.
translation-type: tm+mt
source-git-commit: c3fe5753fb23f99076f9c85b4e07af2d25a121a9

---


# Oracle Eloqua

## Panoramica

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) è un software come piattaforma di servizio (SaaS) per l&#39;automazione del marketing offerto da Oracle che mira ad aiutare gli esperti di marketing e le organizzazioni B2B a gestire le campagne di marketing e la generazione di lead di vendita.

Per inviare i dati del segmento a Oracle Eloqua, è innanzitutto necessario [collegare la destinazione](#connect-destination) in Adobe Real-time Customer Data Platform, quindi [impostare un&#39;importazione](#import-data-into-eloqua) di dati dalla posizione di storage in Oracle Eloqua.

## Connetti alla destinazione {#connect-destination}

1. In **[!UICONTROL Connections > Destinations]**, selezionare Oracle Eloqua, quindi **[!UICONTROL Connect destination]**.

   ![Connetti a Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Nel passaggio **Autenticazione** , se in precedenza avete impostato una connessione alla destinazione di archiviazione cloud, selezionate **[!UICONTROL Existing Account]** e selezionate una delle connessioni esistenti. In alternativa, potete selezionare **[!UICONTROL New Account]** di impostare una nuova connessione. Compilate le credenziali di autenticazione dell&#39;account e selezionate **[!UICONTROL Connect to destination]**. Per Oracle Eloqua, è possibile scegliere tra **SFTP con password** e **SFTP con chiave** SSH. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, e seleziona **[!UICONTROL Connect to destination]**.

   Per **SFTP con connessioni con password** , dovete fornire Domain, Port, UserName e Password.
Per **SFTP con connessioni chiavi** SSH, dovete fornire Domain, Port, Username e Chiave SSH.

   ![Configurare la procedura guidata Eloqua](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. Nel passaggio **Configurazione** , compila le informazioni relative alla destinazione come indicato di seguito:
   * **Nome**: Scegli un nome appropriato per la tua destinazione.
   * **Descrizione**: Inserite una descrizione per la destinazione.
   * **Percorso** cartella: Specificate il percorso nel percorso di archiviazione in cui CDP in tempo reale depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
   * **Formato** file: **CSV** o **TAB_DELIMITED**. Selezionare il formato di file da esportare nel percorso di memorizzazione.
   ![Informazioni di base Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Fate clic su **Crea destinazione** dopo aver compilato i campi qui sopra. Ora viene creata la destinazione e puoi [attivare i segmenti](/help/rtcdp/destinations/activate-destinations.md) alla destinazione.

## Attributi di destinazione

Quando si [attivano i segmenti](/help/rtcdp/destinations/activate-destinations.md) alla destinazione Oracle Eloqua, è consigliabile selezionare un identificatore univoco dallo schema [](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)unione. Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, vedere [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) esportati in Destinazioni di marketing e-mail.

## Impostazione dell&#39;importazione di dati in Oracle Eloqua {#import-data-into-eloqua}

Dopo aver collegato CDP in tempo reale allo storage Amazon S3 o SFTP, è necessario impostare l&#39;importazione dei dati dalla posizione di storage in Oracle Eloqua. Per informazioni su come eseguire questa operazione, vedere [Importazione di contatti o account](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in Oracle Eloqua Help Center.