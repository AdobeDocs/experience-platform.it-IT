---
title: Marketing Cloud Salesforce
seo-title: Marketing Cloud Salesforce
description: Salesforce Marketing Cloud è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare i viaggi per visitatori e clienti al fine di personalizzare la loro esperienza.
seo-description: Salesforce Marketing Cloud è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare i viaggi per visitatori e clienti al fine di personalizzare la loro esperienza.
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud]

## Panoramica

[!DNL Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare viaggi per visitatori e clienti per personalizzare la loro esperienza.

Per inviare i dati del segmento a [!DNL Salesforce Marketing Cloud], è innanzitutto necessario [collegare la destinazione](#connect-destination) in CDP in tempo reale  Adobe, quindi [impostare un&#39;importazione](#import-data-into-salesforce) di dati dalla posizione di archiviazione in [!DNL Salesforce Marketing Cloud].

## Destinazione Connect {#connect-destination}

1. In **[!UICONTROL Connections > Destinations]**, selezionare [!DNL Salesforce Marketing Cloud], quindi **[!UICONTROL Connect destination]**.

   ![Connessione a Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. Nel **[!UICONTROL Authentication]** passaggio, se in precedenza hai impostato una connessione alla destinazione di archiviazione cloud, seleziona **[!UICONTROL Existing Account]** e seleziona una delle tue connessioni esistenti. In alternativa, potete selezionare **[!UICONTROL New Account]** di impostare una nuova connessione. Compilate le credenziali di autenticazione dell&#39;account e selezionate **[!UICONTROL Connect to destination]**. Ad [!DNL Salesforce Marketing Cloud]esempio, potete scegliere tra **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, e seleziona **[!UICONTROL Connect to destination]**.

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

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](/help/rtcdp/destinations/activate-destinations.md) per informazioni sul flusso di lavoro di attivazione dei segmenti.

## Attributi di destinazione {#destination-attributes}

Quando si [attivano i segmenti](/help/rtcdp/destinations/activate-destinations.md) alla [!DNL Salesforce Marketing Cloud] destinazione, si consiglia di selezionare un identificatore univoco dallo schema [](../../profile/home.md#profile-fragments-and-union-schemas)unione. Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, vedere [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) esportati in Destinazioni di marketing e-mail.

## Dati esportati {#exported-data}

Per [!DNL Salesforce Marketing Cloud] le destinazioni,  Adobe CDP in tempo reale crea un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di memorizzazione specificato. Per ulteriori informazioni sui file, vedi Destinazioni di marketing [e-mail e destinazioni](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) di archiviazione cloud nell&#39;esercitazione sull&#39;attivazione del segmento.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Salesforce_Marketing_Cloud_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## Imposta importazione dati in [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Dopo aver collegato CDP in tempo reale allo storage [!DNL Amazon S3] o SFTP, è necessario impostare l&#39;importazione dei dati dalla posizione di archiviazione in [!DNL Salesforce Marketing Cloud]. Per informazioni su come eseguire questa operazione, consultate [Importazione di utenti iscritti in Marketing Cloud da un file](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) nella [!DNL Salesforce Help Center].