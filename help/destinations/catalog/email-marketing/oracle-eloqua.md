---
keywords: e-mail;e-mail;e-mail;destinazioni e-mail;oracle eloqua;oracle
title: Oracle collegamento Eloqua
description: Oracle Eloqua è una piattaforma software as a service (SaaS) per l'automazione del marketing offerta da Oracle che ha lo scopo di aiutare gli esperti di marketing e le organizzazioni B2B a gestire le campagne di marketing e la generazione di lead di vendita.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# [!DNL Oracle Eloqua] connection

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) è una piattaforma software as a service (SaaS) per l&#39;automazione del marketing offerta da  [!DNL Oracle] che ha lo scopo di aiutare gli esperti di marketing e le organizzazioni B2B a gestire le campagne di marketing e la generazione di lead di vendita.

Per inviare i dati dei segmenti a [!DNL Oracle Eloqua], è necessario prima [collegare la destinazione](#connect-destination) in Adobe Experience Platform, quindi [impostare un&#39;importazione di dati](#import-data-into-eloqua) dal percorso di archiviazione in [!DNL Oracle Eloqua].

## Tipo di esportazione {#export-type}

**Basato su profilo** : stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto dalla schermata seleziona attributi del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

## Connetti alla destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Oracle Eloqua], quindi selezionare **[!UICONTROL Configure]**.

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra [!UICONTROL Activate] e [!UICONTROL Configure], consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

![Connettiti a Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

Nel passaggio **[!UICONTROL Account]**, se in precedenza hai impostato una connessione alla destinazione di archiviazione cloud, seleziona **[!UICONTROL Existing Account]** e seleziona una delle connessioni esistenti. In alternativa, è possibile selezionare **[!UICONTROL New Account]** per impostare una nuova connessione. Immetti le credenziali di autenticazione del tuo account e seleziona **[!UICONTROL Connect to destination]**. Per [!DNL Oracle Eloqua], puoi selezionare tra **[!UICONTROL SFTP with Password]** e **[!UICONTROL SFTP with SSH Key]**.

![Connetti account Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/connection-type.png)

Compila le informazioni seguenti, a seconda del tipo di connessione, e seleziona **[!UICONTROL Connect to destination]**.

- Per le connessioni **[!UICONTROL SFTP with Password]**, è necessario specificare [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] e [!UICONTROL Password].
- Per le connessioni **[!UICONTROL SFTP with SSH Key]**, è necessario specificare [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] e [!UICONTROL SSH Key].

Facoltativamente, puoi allegare la tua chiave pubblica in formato RSA per aggiungere la crittografia con PGP/GPG ai file esportati nella sezione **[!UICONTROL Key]** . La chiave pubblica deve essere scritta come stringa codificata [!DNL Base64].

![Eloqua connessione a destinazione](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

Nel passaggio **[!UICONTROL Authentication]** , compila le informazioni rilevanti per la tua destinazione come mostrato di seguito:
- **[!UICONTROL Name]**: Scegli un nome appropriato per la destinazione.
- **[!UICONTROL Description]**: Inserisci una descrizione per la destinazione.
- **[!UICONTROL Folder Path]**: Fornisci il percorso nel percorso di archiviazione in cui Platform depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
- **[!UICONTROL File Format]**:  **** CSVo  **TAB_DELIMITTED**. Selezionare il formato di file da esportare nel percorso di archiviazione.
- **[!UICONTROL Marketing actions]**: Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![Informazioni di base Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

Fai clic su **[!UICONTROL Create destination]** dopo aver compilato i campi sopra riportati. La destinazione viene ora creata ed è possibile [attivare segmenti](../../ui/activate-destinations.md) alla destinazione.

## Attiva segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, consulta [Attivare profili e segmenti su una destinazione](../../ui/activate-destinations.md) .

## Attributi di destinazione {#destination-attributes}

Quando si attivano [i segmenti](../../ui/activate-destinations.md) alla destinazione [!DNL Oracle Eloqua], l&#39;Adobe consiglia di selezionare un identificatore univoco dal proprio [schema di unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, consulta [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file esportati](./overview.md#destination-attributes).

## Dati esportati {#exported-data}

Per le destinazioni [!DNL Oracle Eloqua], Platform crea un file `.txt` o `.csv` delimitato da tabulazioni nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [Destinazioni di e-mail marketing e destinazioni di archiviazione Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell’esercitazione sull’attivazione dei segmenti.

## Imposta l’importazione di dati in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Dopo aver effettuato la connessione di [!DNL Platform] all&#39;archiviazione SFTP, devi impostare l&#39;importazione di dati dal percorso di archiviazione in [!DNL Oracle Eloqua]. Per informazioni su come eseguire questa operazione, consulta [Importazione di contatti o account](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in [!DNL Oracle Eloqua Help Center].