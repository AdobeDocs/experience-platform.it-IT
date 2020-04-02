---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare i viaggi per visitatori e clienti al fine di personalizzare la loro esperienza.
seo-description: Salesforce Marketing Cloud è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare i viaggi per visitatori e clienti al fine di personalizzare la loro esperienza.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Salesforce Marketing Cloud

## Panoramica

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare i viaggi per visitatori e clienti per personalizzare la loro esperienza.

Per inviare i dati del segmento a Salesforce Marketing Cloud, è innanzitutto necessario [collegare la destinazione](#connect-destination) in Adobe Real-time CDP, quindi [impostare un&#39;importazione](#import-data-into-salesforce) di dati dalla posizione di archiviazione in Salesforce Marketing Cloud.

## Destinazione Connect {#connect-destination}

1. In **[!UICONTROL Connections > Destinations]**, seleziona Salesforce Marketing Cloud, quindi seleziona **[!UICONTROL Connect destination]**.

   ![Connessione a Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. Nel **[!UICONTROL Authentication]** passaggio, se in precedenza hai impostato una connessione alla destinazione di archiviazione cloud, seleziona **[!UICONTROL Existing Account]** e seleziona una delle tue connessioni esistenti. In alternativa, potete selezionare **[!UICONTROL New Account]** di impostare una nuova connessione. Compilate le credenziali di autenticazione dell&#39;account e selezionate **[!UICONTROL Connect to destination]**. Per Salesforce Marketing Cloud, potete scegliere tra **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, e seleziona **[!UICONTROL Connect to destination]**.

   Per **[!UICONTROL SFTP with Password]** le connessioni, dovete fornire Domain, Port, UserName e Password.
Per **[!UICONTROL SFTP with SSH Key]** le connessioni, è necessario fornire Domain, Port, Username e SSH Key.

   ![Compila le informazioni di Salesforce](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. Nel **[!UICONTROL Setup]** passaggio, compila le informazioni rilevanti per la tua destinazione come indicato di seguito:
   * **[!UICONTROL Name]**: Scegli un nome appropriato per la tua destinazione.
   * **[!UICONTROL Description]**: Inserite una descrizione per la destinazione.
   * **[!UICONTROL Folder Path]**: Specificate il percorso nel percorso di archiviazione in cui CDP in tempo reale depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
   * **[!UICONTROL File Format]**: **[!UICONTROL CSV]** o **[!UICONTROL TAB_DELIMITED]**. Selezionare il formato di file da esportare nel percorso di memorizzazione.
   ![Informazioni di base di Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Fare clic **[!UICONTROL Create destination]** dopo aver compilato i campi sopra. La destinazione è ora connessa e puoi [attivare i segmenti](/help/rtcdp/destinations/activate-destinations.md) alla destinazione.

## Attributi di destinazione {#destination-attributes}

Quando si [attivano segmenti](/help/rtcdp/destinations/activate-destinations.md) nella destinazione Salesforce Marketing Cloud, si consiglia di selezionare un identificatore univoco dallo schema [](../../profile/home.md#profile-fragments-and-union-schemas)unione. Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, vedere [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) esportati in Destinazioni di marketing e-mail.

## Configurare l&#39;importazione di dati in Salesforce Marketing Cloud {#import-data-into-salesforce}

Dopo aver collegato CDP in tempo reale allo storage Amazon S3 o SFTP, è necessario configurare l&#39;importazione dei dati dalla posizione di archiviazione in Salesforce Marketing Cloud. Per informazioni su come eseguire questa operazione, consulta [Importazione di utenti iscritti a Marketing Cloud da un file](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) nell’Aiuto di Salesforce.