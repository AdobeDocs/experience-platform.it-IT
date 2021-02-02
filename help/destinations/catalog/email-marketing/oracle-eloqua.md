---
keywords: email;Email;e-mail;destinazioni e-mail; oracle eloqua; oracle
title: ' destinazione Oracle Eloqua'
seo-title: ' destinazione Oracle Eloqua'
description: ' Oracle Eloqua è un software come piattaforma di servizio (SaaS) per l''automazione del marketing offerto da  Oracle che mira ad aiutare gli esperti di marketing e le organizzazioni B2B a gestire campagne di marketing e la generazione di lead di vendita.'
seo-description: ' Oracle Eloqua è un software come piattaforma di servizio (SaaS) per l''automazione del marketing offerto da  Oracle che mira ad aiutare gli esperti di marketing e le organizzazioni B2B a gestire campagne di marketing e la generazione di lead di vendita.'
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# [!DNL Oracle Eloqua]

## Panoramica

[[!DNL Oracle Eloqua]](https://www.oracle.com/marketingcloud/products/marketing-automation/) è un software come piattaforma di servizio (SaaS) per l&#39;automazione del marketing offerto da  [!DNL Oracle] che mira ad aiutare gli esperti di marketing e le organizzazioni B2B a gestire le campagne di marketing e la generazione di lead di vendita.

Per inviare i dati del segmento a [!DNL Oracle Eloqua], è necessario prima [collegare la destinazione](#connect-destination) in Adobe Experience Platform, quindi [impostare un&#39;importazione di dati](#import-data-into-eloqua) dal percorso di memorizzazione in [!DNL Oracle Eloqua].

## Tipo di esportazione {#export-type}

**Basato**  su profilo: si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata degli attributi selezionati del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

## Connetti alla destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Oracle Eloqua], quindi selezionare **[!UICONTROL Connect destination]**.

[Connetti a Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

Nel passaggio **[!UICONTROL Authentication]**, se in precedenza è stata impostata una connessione alla destinazione di archiviazione cloud, selezionare **[!UICONTROL Existing Account]** e selezionare una delle connessioni esistenti. In alternativa, è possibile selezionare **[!UICONTROL New Account]** per impostare una nuova connessione. Compilate le credenziali di autenticazione dell&#39;account e selezionate **[!UICONTROL Connect to destination]**. Per [!DNL Oracle Eloqua], è possibile selezionare tra **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, e seleziona **[!UICONTROL Connect to destination]**.

Per le connessioni **[!UICONTROL SFTP with Password]**, dovete fornire Domain, Port, UserName e Password.
Per le connessioni **[!UICONTROL SFTP with SSH Key]**, è necessario fornire Domain, Port, Username e SSH Key.

![Configurare la procedura guidata Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

Nel passaggio **[!UICONTROL Setup]**, compila le informazioni rilevanti per la tua destinazione come indicato di seguito:
- **[!UICONTROL Name]**: Scegli un nome appropriato per la tua destinazione.
- **[!UICONTROL Description]**: Inserite una descrizione per la destinazione.
- **[!UICONTROL Folder Path]**: Specificate il percorso nel percorso di archiviazione in cui Platform depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
- **[!UICONTROL File Format]**:  **** CSVo  **TAB_DELIMITED**. Selezionare il formato di file da esportare nel percorso di memorizzazione.

![Informazioni di base Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

Fare clic su **[!UICONTROL Create destination]** dopo aver compilato i campi riportati sopra. La destinazione viene creata e potete [attivare i segmenti](../../ui/activate-destinations.md) alla destinazione.

## Attivare i segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, vedere [Attivare profili e segmenti in una destinazione](../../ui/activate-destinations.md).

## Attributi di destinazione {#destination-attributes}

Quando si attivano [segmenti](../../ui/activate-destinations.md) alla destinazione [!DNL Oracle Eloqua], è consigliabile selezionare un identificatore univoco dal [schema unione](../../../profile/home.md#profile-fragments-and-union-schemas). Selezionate l’identificatore univoco ed eventuali altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, vedere [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file esportati](./overview.md#destination-attributes) in Destinazioni marketing e-mail.

## Dati esportati {#exported-data}

Per le destinazioni [!DNL Oracle Eloqua], Platform crea un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedi [Destinazioni di marketing e archiviazione di e-mail e Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell&#39;esercitazione sull&#39;attivazione dei segmenti.

## Imposta l&#39;importazione dei dati in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Dopo aver collegato la piattaforma allo storage Amazon S3 o SFTP , è necessario impostare l&#39;importazione dei dati dalla posizione di archiviazione in [!DNL Oracle Eloqua]. Per informazioni su come eseguire questa operazione, vedere [Importazione di contatti o account](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in [!DNL Oracle Eloqua Help Center].