---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare i viaggi per visitatori e clienti al fine di personalizzare la loro esperienza.
seo-description: Salesforce Marketing Cloud è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare i viaggi per visitatori e clienti al fine di personalizzare la loro esperienza.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## Panoramica

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare i viaggi per visitatori e clienti per personalizzare la loro esperienza.

Per inviare i dati del segmento a Salesforce Marketing Cloud, è innanzitutto necessario [collegare la destinazione](#connect-destination) in Adobe Real-time CDP, quindi [impostare un&#39;importazione](#import-data-into-salesforce) di dati dalla posizione di archiviazione in Salesforce Marketing Cloud.

## Destinazione Connect {#connect-destination}

1. In **[!UICONTROL Connessioni > Destinazioni]**, selezionate Salesforce Marketing Cloud, quindi selezionate la destinazione **** Connect.

   ![Connessione a Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. Nella procedura guidata di destinazione di Connect, selezionate il tipo **[!UICONTROL di]** connessione per il percorso di memorizzazione. Per Salesforce Marketing Cloud, potete scegliere tra **SFTP con password** e **SFTP con chiave** SSH. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, e seleziona **[!UICONTROL Connect]**.

   ![Configurazione della procedura guidata Salesforce](/help/rtcdp/destinations/assets/salesforce-step1.png)

   Per **SFTP con connessioni con password** , dovete fornire Domain, Port, UserName e Password.
Per **SFTP con connessioni chiavi** SSH, dovete fornire Domain, Port, Username e Chiave SSH.

   ![Compila le informazioni di Salesforce](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. In Informazioni **** di base, compila le informazioni relative alla tua destinazione, come indicato di seguito:
   * **Nome**: Scegli un nome appropriato per la tua destinazione.
   * **Descrizione**: Inserite una descrizione per la destinazione.
   * **Percorso** cartella: Specificate il percorso nel percorso di archiviazione in cui CDP in tempo reale depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
   * **Formato** file: **CSV** o **TAB_DELIMITED**. Selezionare il formato di file da esportare nel percorso di memorizzazione.
   ![Informazioni di base di Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Fate clic su **Crea** dopo aver compilato i campi in Informazioni **di** base. La destinazione è ora connessa e puoi [attivare i segmenti](/help/rtcdp/destinations/activate-destinations.md) alla destinazione.

## Attributi di destinazione {#destination-attributes}

Quando si [attivano segmenti](/help/rtcdp/destinations/activate-destinations.md) nella destinazione Salesforce Marketing Cloud, si consiglia di selezionare un identificatore univoco dallo schema [](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)unione. Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, vedere [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) esportati in Destinazioni di marketing e-mail.

## Configurare l&#39;importazione di dati in Salesforce Marketing Cloud {#import-data-into-salesforce}

Dopo aver collegato CDP in tempo reale allo storage Amazon S3 o SFTP, è necessario configurare l&#39;importazione dei dati dalla posizione di archiviazione in Salesforce Marketing Cloud. Per informazioni su come eseguire questa operazione, consulta [Importazione di utenti iscritti a Marketing Cloud da un file](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) nell’Aiuto di Salesforce.