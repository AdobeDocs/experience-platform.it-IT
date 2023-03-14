---
keywords: e-mail;E-mail;Destinazioni e-mail;Destinazione oracle responsys
title: Connessione Responsys Oracle
description: Responsys è uno strumento di e-mail marketing aziendale per campagne di marketing cross-channel offerto da Oracle per personalizzare le interazioni tra e-mail, dispositivi mobili, display e social network.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---

# [!DNL Oracle Responsys] connessione

## Panoramica {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/) è uno strumento di e-mail marketing aziendale per campagne di marketing cross-channel offerto da [!DNL Oracle] per personalizzare le interazioni tra e-mail, dispositivi mobili, display e social network.

Per inviare i dati del segmento a [!DNL Oracle Responsys], devi prima [connettersi alla destinazione](#connect-destination) in Adobe Experience Platform, quindi [impostare un’importazione di dati](#import-data-into-responsys) dalla posizione di archiviazione in [!DNL Oracle Responsys].

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni su [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## ELENCO CONSENTITI di indirizzo IP {#allow-list}

Quando configuri le destinazioni di e-mail marketing con l’archiviazione SFTP, Adobe consiglia di aggiungere determinati intervalli IP all’elenco consentiti.

Fai riferimento a [ELENCO CONSENTITI di indirizzo IP per le destinazioni di archiviazione cloud](../cloud-storage/ip-address-allow-list.md) se devi aggiungere degli IP di Adobe all’elenco consentiti.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

Questa destinazione supporta i seguenti tipi di connessione:

* **[!UICONTROL SFTP con password]**
* **[!UICONTROL SFTP con chiave SSH]**

### Parametri di connessione {#parameters}

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

* Per **[!UICONTROL SFTP con password]** connessioni, devi fornire:
   * [!UICONTROL Dominio]
   * [!UICONTROL Porta ]
   * [!UICONTROL Nome utente]
   * [!UICONTROL Password]
* Per **[!UICONTROL SFTP con chiave SSH]** connessioni, devi fornire:
   * [!UICONTROL Dominio]
   * [!UICONTROL Porta ]
   * [!UICONTROL Nome utente]
   * [!UICONTROL Chiave SSH]
* In alternativa, è possibile allegare la chiave pubblica in formato RSA per aggiungere la crittografia con PGP/GPG ai file esportati in **[!UICONTROL Chiave]** sezione. La chiave pubblica deve essere scritta come [!DNL Base64] stringa codificata.
* **[!UICONTROL Nome]**: scegli un nome pertinente per la destinazione.
* **[!UICONTROL Descrizione]**: immetti una descrizione per la destinazione.
* **[!UICONTROL Percorso cartella]**: specifica il percorso nel percorso di archiviazione in cui Platform depositerà i dati di esportazione come file CSV.
* **[!UICONTROL Formato file]**: Seleziona **CSV** per esportare i file CSV nel percorso di archiviazione.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

### Attributi di destinazione {#destination-attributes}

Quando si attivano i segmenti in questa destinazione, Adobe consiglia di selezionare un identificatore univoco dal [schema di unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, consulta [best practice per l’attivazione di tipi di pubblico su destinazioni di e-mail marketing](overview.md#best-practices).

## Dati esportati {#exported-data}

Per [!DNL Oracle Responsys] destinazioni, Platform crea un’ `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [verifica attivazione segmento](../../ui/activate-batch-profile-destinations.md#verify) nell’esercitazione di attivazione dei segmenti.

## Configurare l’importazione dei dati in [!DNL Oracle Responsys] {#import-data-into-responsys}

Dopo la connessione [!DNL Platform] al tuo [!DNL SFTP] di archiviazione, è necessario impostare l&#39;importazione dei dati dalla posizione di archiviazione in [!DNL Oracle Responsys]. Per scoprire come eseguire questa operazione, consulta [Importazione di contatti o account](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) nel [!DNL Oracle Responsys Help Center].
