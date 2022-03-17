---
keywords: e-mail;e-mail;e-mail;destinazioni e-mail;destinazione risposta oracle
title: Oracle connessione Responsys
description: Responsys è uno strumento di marketing e-mail aziendale per campagne di marketing cross-channel offerte da Oracle per personalizzare le interazioni tra e-mail, dispositivi mobili, display e social.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 2%

---

# [!DNL Oracle Responsys] connection

## Panoramica {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/) è uno strumento di marketing e-mail aziendale per campagne di marketing cross-channel offerte da [!DNL Oracle] per personalizzare le interazioni tra e-mail, dispositivi mobili, visualizzazioni e social.

Per inviare i dati del segmento a [!DNL Oracle Responsys], devi prima [connettersi alla destinazione](#connect-destination) in Adobe Experience Platform e quindi [impostare un’importazione di dati](#import-data-into-responsys) dalla posizione di archiviazione in [!DNL Oracle Responsys].

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

Per [!DNL Oracle Responsys] destinazioni, Platform crea un `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedi [verifica attivazione segmento](../../ui/activate-batch-profile-destinations.md#verify) nell’esercitazione sull’attivazione dei segmenti.

## Imposta l’importazione di dati in [!DNL Oracle Responsys] {#import-data-into-responsys}

Dopo la connessione [!DNL Platform] al tuo [!DNL SFTP] archiviazione, è necessario impostare l&#39;importazione di dati dal percorso di archiviazione in [!DNL Oracle Responsys]. Per scoprire come eseguire questa operazione, consulta [Importazione di contatti o account](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in [!DNL Oracle Responsys Help Center].
