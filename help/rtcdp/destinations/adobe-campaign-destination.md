---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign è un insieme di soluzioni che consentono di personalizzare e distribuire le campagne su tutti i canali online e offline.
seo-description: Adobe Campaign è un insieme di soluzioni che consentono di personalizzare e distribuire le campagne su tutti i canali online e offline.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Adobe Campaign

## Panoramica

Adobe Campaign è un insieme di soluzioni che consentono di personalizzare e distribuire le campagne su tutti i canali online e offline. Per ulteriori informazioni, consulta [Informazioni su Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) .

Per inviare i dati del segmento ad Adobe Campaign, devi prima [collegare la destinazione](#connect-destination) nella piattaforma dati cliente Adobe in tempo reale, quindi [impostare un&#39;importazione](#import-data-into-campaign) di dati dalla posizione di archiviazione in Adobe Campaign.

## Destinazione Connect {#connect-destination}

1. In **[!UICONTROL Connessioni > Destinazioni]**, seleziona Adobe Campaign, quindi seleziona la destinazione **[!UICONTROL di]** Connect.

   ![Connetti ad adobe campaign](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. Nella procedura guidata di destinazione di Connect, selezionate il tipo **[!UICONTROL di]** connessione per il percorso di memorizzazione. Per Adobe Campaign, puoi scegliere tra **Amazon S3**, **SFTP con password** e **SFTP con chiave** SSH. Compila le informazioni seguenti, a seconda del tipo di connessione, quindi seleziona **[!UICONTROL Connect]**.

   ![Configurazione guidata campagna](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Per le connessioni **S3** , dovete fornire il vostro ID chiave di accesso e la chiave di accesso segreta.
Per **SFTP con connessioni con password** , dovete fornire Domain, Port, UserName e Password.
Per **SFTP con connessioni chiavi** SSH, dovete fornire Domain, Port, Username e Chiave SSH.

   ![Compila le informazioni sulla campagna](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. In Informazioni **** di base, compila le informazioni relative alla tua destinazione, come indicato di seguito:
   * **Nome**: Scegli un nome appropriato per la tua destinazione.
   * **Descrizione**: Inserite una descrizione per la destinazione.
   * **Nome** intervallo: *Per connessioni* S3. Immettete la posizione del bucket S3 in cui CDP in tempo reale depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
   * **Percorso** cartella: Specificate il percorso nel percorso di archiviazione in cui CDP in tempo reale depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
   * **Formato** file: **CSV** o **TAB_DELIMITED**. Selezionare il formato di file da esportare nel percorso di memorizzazione.
   ![Informazioni di base sulla campagna](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Fate clic su **Crea** dopo aver compilato i campi in Informazioni **di** base. La destinazione è ora connessa e puoi [attivare i segmenti](/help/rtcdp/destinations/activate-destinations.md) alla destinazione.

## Attributi di destinazione {#destination-attributes}

Quando [attivi i segmenti](/help/rtcdp/destinations/activate-destinations.md) nella destinazione Adobe Campaign, ti consigliamo di selezionare un identificatore univoco dallo schema [](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)unione. Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, vedere [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) esportati in Destinazioni di marketing e-mail.


## Impostazione dell&#39;importazione di dati in Adobe Campaign {#import-data-into-campaign}

Dopo aver collegato CDP in tempo reale allo storage Amazon S3 o SFTP, devi configurare l&#39;importazione dei dati dalla posizione di archiviazione in Adobe Campaign. Per informazioni su come eseguire questa operazione, consulta [Importazione di dati](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) nella documentazione della Guida di Adobe Campaign.