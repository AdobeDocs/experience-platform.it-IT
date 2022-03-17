---
keywords: e-mail;e-mail;e-mail;destinazioni e-mail;oracle eloqua;oracle
title: Oracle collegamento Eloqua
description: Oracle Eloqua è una piattaforma software as a service (SaaS) per l'automazione del marketing offerta da Oracle che ha lo scopo di aiutare gli esperti di marketing e le organizzazioni B2B a gestire le campagne di marketing e la generazione di lead di vendita.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---

# [!DNL Oracle Eloqua] connection

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) è una piattaforma software as a service (SaaS) per l&#39;automazione del marketing offerta da [!DNL Oracle] che ha lo scopo di aiutare gli esperti di marketing e le organizzazioni B2B a gestire le campagne di marketing e la generazione di lead di vendita.

Per inviare i dati del segmento a [!DNL Oracle Eloqua], devi prima [collegare la destinazione](#connect-destination) in Adobe Experience Platform e quindi [impostare un’importazione di dati](#import-data-into-eloqua) dalla posizione di archiviazione in [!DNL Oracle Eloqua].

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Batch]** | Le destinazioni batch esportano file su piattaforme downstream con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni [destinazioni batch basate su file](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## ELENCO CONSENTITI di indirizzo IP {#allow-list}

Quando si impostano le destinazioni di marketing e-mail con l’archiviazione SFTP, Adobe consiglia di aggiungere determinati intervalli IP al proprio elenco consentiti.

Fai riferimento a [ELENCO CONSENTITI di indirizzi IP per le destinazioni di archiviazione cloud](../cloud-storage/ip-address-allow-list.md) se devi aggiungere IP di Adobe al tuo elenco consentiti.

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

Questa destinazione supporta i seguenti tipi di connessione:

* **[!UICONTROL SFTP con password]**
* **[!UICONTROL SFTP con chiave SSH]**

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* Per **[!UICONTROL SFTP con password]** connessioni, è necessario fornire:
   * [!UICONTROL Dominio]
   * [!UICONTROL Porta ]
   * [!UICONTROL Nome utente]
   * [!UICONTROL Password]
* Per **[!UICONTROL SFTP con chiave SSH]** connessioni, è necessario fornire:
   * [!UICONTROL Dominio]
   * [!UICONTROL Porta ]
   * [!UICONTROL Nome utente]
   * [!UICONTROL Chiave SSH]

* Facoltativamente, puoi allegare la tua chiave pubblica in formato RSA per aggiungere la crittografia con PGP/GPG ai file esportati sotto **[!UICONTROL Chiave]** sezione . La chiave pubblica deve essere scritta come [!DNL Base64] stringa codificata.
* **[!UICONTROL Nome]**: Scegli un nome appropriato per la destinazione.
* **[!UICONTROL Descrizione]**: Inserisci una descrizione per la destinazione.
* **[!UICONTROL Percorso cartella]**: Fornisci il percorso nella posizione di archiviazione in cui Platform depositerà i dati di esportazione come file CSV.
* **[!UICONTROL Formato file]**: Seleziona **CSV** per esportare i file CSV nel percorso di archiviazione.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Attiva i segmenti in questa destinazione {#activate}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Attributi di destinazione {#destination-attributes}

Quando attivi i segmenti su questa destinazione, Adobe consiglia di selezionare un identificatore univoco dal [schema unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, consulta [best practice per attivare i tipi di pubblico nelle destinazioni di marketing via e-mail](overview.md#best-practices).

## Dati esportati {#exported-data}

Per [!DNL Oracle Eloqua] destinazioni, Platform crea un `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedi [verifica attivazione segmento](../../ui/activate-batch-profile-destinations.md#verify) nell’esercitazione sull’attivazione dei segmenti.

## Imposta l’importazione di dati in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Dopo la connessione [!DNL Platform] al tuo [!DNL SFTP] archiviazione, è necessario impostare l&#39;importazione di dati dal percorso di archiviazione in [!DNL Oracle Eloqua]. Per scoprire come eseguire questa operazione, consulta [Importazione di contatti o account](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in [!DNL Oracle Eloqua Help Center].
