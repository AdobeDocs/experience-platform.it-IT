---
keywords: e-mail;e-mail;e-mail;destinazioni;salesforce;destinazione salesforce
title: Collegamento Marketing Cloud Salesforce
seo-description: Salesforce Marketing Cloud è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare percorsi per visitatori e clienti per personalizzare la loro esperienza.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud] connection

## Panoramica {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) è una suite di marketing digitale precedentemente nota come ExactTarget che consente di creare e personalizzare percorsi per visitatori e clienti per personalizzare la loro esperienza.

Per inviare i dati dei segmenti a [!DNL Salesforce Marketing Cloud], è necessario prima [collegare la destinazione](#connect-destination) in Platform, quindi [impostare un&#39;importazione di dati](#import-data-into-salesforce) dal percorso di archiviazione in [!DNL Salesforce Marketing Cloud].

## Tipo di esportazione {#export-type}

**Basato su profilo** : stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto dalla schermata seleziona attributi del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

## ELENCO CONSENTITI di indirizzo IP {#allow-list}

Quando si impostano le destinazioni di marketing e-mail con l’archiviazione SFTP, Adobe consiglia di aggiungere determinati intervalli IP al proprio elenco consentiti.

Per aggiungere IP di Adobe al tuo elenco consentiti, fai riferimento all’ [elenco consentiti di indirizzi IP per le destinazioni di archiviazione cloud](../cloud-storage/ip-address-allow-list.md) .

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

Questa destinazione supporta i seguenti tipi di connessione:

* **[!UICONTROL SFTP con password]**
* **[!UICONTROL SFTP con chiave SSH]**

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* Per le connessioni **[!UICONTROL SFTP con password]**, devi fornire:
   * [!UICONTROL Dominio]
   * [!UICONTROL Porta]
   * [!UICONTROL Nome utente]
   * [!UICONTROL Password]
* Per le connessioni **[!UICONTROL SFTP con chiave SSH]**, devi fornire:
   * [!UICONTROL Dominio]
   * [!UICONTROL Porta]
   * [!UICONTROL Nome utente]
   * [!UICONTROL Chiave SSH]

* Facoltativamente, puoi allegare la tua chiave pubblica in formato RSA per aggiungere la crittografia con PGP/GPG ai file esportati nella sezione **[!UICONTROL Chiave]** . La chiave pubblica deve essere scritta come stringa codificata [!DNL Base64].
* **[!UICONTROL Nome]**: Scegli un nome appropriato per la destinazione.
* **[!UICONTROL Descrizione]**: Inserisci una descrizione per la destinazione.
* **[!UICONTROL Percorso]** cartella: Fornisci il percorso nel percorso di archiviazione in cui Platform depositerà i dati di esportazione come file CSV o delimitati da tabulazioni.
* **[!UICONTROL Formato]** file:  **** CSVo  **TAB_DELIMITTED**. Selezionare il formato di file da esportare nel percorso di archiviazione.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico nelle destinazioni, consulta [Attivare profili e segmenti in una destinazione](../../ui/activate-destinations.md) .

## Attributi di destinazione {#destination-attributes}

Quando si attivano [segmenti](../../ui/activate-destinations.md) a questa destinazione, Adobe consiglia di selezionare un identificatore univoco dal [schema di unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, consulta [Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file esportati](./overview.md#destination-attributes).

## Dati esportati {#exported-data}

Per le destinazioni [!DNL Salesforce Marketing Cloud], Platform crea un file `.csv` delimitato da tabulazioni nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [Destinazioni di e-mail marketing e destinazioni di archiviazione Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell’esercitazione sull’attivazione dei segmenti.

## Imposta l’importazione di dati in [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Dopo aver collegato [!DNL Platform] allo storage [!DNL SFTP], è necessario impostare l&#39;importazione dei dati dal percorso di archiviazione in [!DNL Salesforce Marketing Cloud]. Per informazioni su come eseguire questa operazione, consulta [Importazione di Sottoscrittori in un Marketing Cloud da un file](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in [!DNL Salesforce Help Center].
