---
title: Destinazione Oracle Eloqua
seo-title: Destinazione Oracle Eloqua
description: Oracle Eloqua è un software come piattaforma di servizio (SaaS) per l'automazione del marketing offerto da Oracle che mira ad aiutare gli esperti di marketing e le organizzazioni B2B a gestire le campagne di marketing e la generazione di lead di vendita.
seo-description: Oracle Eloqua è un software come piattaforma di servizio (SaaS) per l'automazione del marketing offerto da Oracle che mira ad aiutare gli esperti di marketing e le organizzazioni B2B a gestire le campagne di marketing e la generazione di lead di vendita.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# [!DNL Oracle Eloqua]

## Panoramica

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) è un software come piattaforma di servizio (SaaS) per l&#39;automazione del marketing offerto da [!DNL Oracle] che mira ad aiutare gli esperti di marketing e le organizzazioni B2B a gestire campagne di marketing e la generazione di lead di vendita.

Per inviare i dati del segmento a [!DNL Oracle Eloqua], è innanzitutto necessario [collegare la destinazione](#connect-destination) in Adobe Real-time Customer Data Platform, quindi [impostare un&#39;importazione](#import-data-into-eloqua) di dati dalla posizione di archiviazione in [!DNL Oracle Eloqua].

## Connetti alla destinazione {#connect-destination}

1. In **[!UICONTROL Connections > Destinations]**, selezionare [!DNL Oracle Eloqua], quindi **[!UICONTROL Connect destination]**.

   ![Connetti a Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Nel **[!UICONTROL Authentication]** passaggio, se in precedenza hai impostato una connessione alla destinazione di archiviazione cloud, seleziona **[!UICONTROL Existing Account]** e seleziona una delle tue connessioni esistenti. In alternativa, potete selezionare **[!UICONTROL New Account]** di impostare una nuova connessione. Compilate le credenziali di autenticazione dell&#39;account e selezionate **[!UICONTROL Connect to destination]**. Ad [!DNL Oracle Eloqua]esempio, potete scegliere tra **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, e seleziona **[!UICONTROL Connect to destination]**.

   Per **[!UICONTROL SFTP with Password]** le connessioni, dovete fornire Domain, Port, UserName e Password.
Per **[!UICONTROL SFTP with SSH Key]** le connessioni, è necessario fornire Domain, Port, Username e SSH Key.

   ![Configurare la procedura guidata Eloqua](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. Nel **[!UICONTROL Setup]** passaggio, compila le informazioni rilevanti per la tua destinazione come indicato di seguito:
   * **[!UICONTROL Name]**: Scegli un nome appropriato per la tua destinazione.
   * **[!UICONTROL Description]**: Inserite una descrizione per la destinazione.
   * **[!UICONTROL Folder Path]**: Specificate il percorso nel percorso di archiviazione in cui CDP in tempo reale depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
   * **[!UICONTROL File Format]**: **CSV** o **TAB_DELIMITED**. Selezionare il formato di file da esportare nel percorso di memorizzazione.

   ![Informazioni di base Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Fare clic **[!UICONTROL Create destination]** dopo aver compilato i campi sopra. Ora viene creata la destinazione e puoi [attivare i segmenti](/help/rtcdp/destinations/activate-destinations.md) alla destinazione.

## Attributi di destinazione

Quando si [attivano i segmenti](/help/rtcdp/destinations/activate-destinations.md) alla [!DNL Oracle Eloqua] destinazione, si consiglia di selezionare un identificatore univoco dallo schema [](../../profile/home.md#profile-fragments-and-union-schemas)unione. Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, vedere [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) esportati in Destinazioni di marketing e-mail.

## Imposta importazione dati in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Dopo aver collegato CDP in tempo reale allo storage Amazon S3 o SFTP, è necessario configurare l&#39;importazione dei dati dalla posizione di archiviazione in [!DNL Oracle Eloqua]. Per informazioni su come eseguire questa operazione, consulta [Importazione di contatti o account](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) nella [!DNL Oracle Eloqua Help Center].