---
keywords: e-mail;e-mail;destinazioni e-mail;adobe campaign;campaign
title: Connessione Adobe Campaign
description: Adobe Campaign è un insieme di soluzioni che ti aiutano a personalizzare e distribuire campagne su tutti i canali online e offline.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 1%

---

# Connessione Adobe Campaign

## Panoramica {#overview}

Adobe Campaign è un insieme di soluzioni che ti aiutano a personalizzare e distribuire campagne su tutti i canali online e offline. Consulta [Introduzione a Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) per ulteriori informazioni.

Per inviare i dati dei segmenti ad Adobe Campaign, devi prima [connettere la destinazione](#connect-destination) in Adobe Experience Platform, quindi [impostare un’importazione di dati](#import-data-into-campaign) dalla posizione di archiviazione in Adobe Campaign.

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
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

Adobe Campaign supporta i seguenti tipi di connessione:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP con password]**
* **[!UICONTROL SFTP con chiave SSH]**
* **[!UICONTROL BLOB di Azure]**

Il metodo preferito per inviare dati ad Adobe Campaign è tramite [!DNL Amazon S3] o [!DNL Azure Blob].

### Parametri di connessione {#parameters}

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

* Per **[!UICONTROL Amazon S3]** connessioni, è necessario specificare [!UICONTROL ID chiave di accesso] e [!UICONTROL Chiave di accesso segreta].
* Per **[!UICONTROL SFTP con password]** connessioni, è necessario fornire [!UICONTROL Dominio], [!UICONTROL Porta], [!UICONTROL Nome utente], e [!UICONTROL Password].
* Per **[!UICONTROL SFTP con chiave SSH]** connessioni, è necessario fornire [!UICONTROL Dominio], [!UICONTROL Porta], [!UICONTROL Nome utente], e [!UICONTROL Chiave SSH].
* Per **[!UICONTROL BLOB di Azure]** connessioni, è necessario specificare una stringa di connessione.
* In alternativa, è possibile allegare la chiave pubblica in formato RSA per aggiungere la crittografia con PGP/GPG ai file esportati in **[!UICONTROL Chiave]** sezione. La chiave pubblica deve essere scritta come [!DNL Base64] stringa codificata.
* **[!UICONTROL Nome]**: scegli un nome pertinente per la destinazione.
* **[!UICONTROL Descrizione]**: immetti una descrizione per la destinazione.
* **[!UICONTROL Nome bucket]**: *Per connessioni S3*. Immetti la posizione del bucket S3 in cui [!DNL Platform] depositerà i dati di esportazione come file CSV.
* **[!UICONTROL Percorso cartella]**: specifica il percorso nel percorso di archiviazione in cui [!DNL Platform] depositerà i dati di esportazione come file CSV.
* **[!UICONTROL Contenitore]**: *Per le connessioni BLOB*. Il contenitore che contiene il BLOB nel percorso della cartella si trova in.
* **[!UICONTROL Formato file]**: Seleziona **CSV** per esportare i file CSV nel percorso di archiviazione.

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

Per [!DNL Adobe Campaign] destinazioni, [!DNL Platform] crea un `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [verifica attivazione segmento](../../ui/activate-batch-profile-destinations.md#verify) nell’esercitazione di attivazione dei segmenti.

## Configurare l’importazione dei dati in Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Nota bene [!DNL SFTP] limiti di archiviazione, limiti di archiviazione del database e limiti del profilo attivo in base al contratto Adobe Campaign durante l’esecuzione di questa integrazione.
>* È necessario pianificare, importare e mappare i segmenti esportati in Adobe Campaign utilizzando [!DNL Campaign] flussi di lavoro. Fai riferimento a [Impostazione di un’importazione ricorrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) nella documentazione di Adobe Campaign Classic e [Informazioni sulle attività di gestione dati](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) nella documentazione di Adobe Campaign Standard.
>* Il metodo preferito per inviare dati ad Adobe Campaign è tramite [!DNL Amazon S3] o [!DNL Azure Blob].


Dopo la connessione [!DNL Platform] al tuo [!DNL Amazon S3] o [!DNL Azure Blob] di archiviazione, è necessario configurare l’importazione dei dati dalla posizione di archiviazione in Adobe Campaign. Per informazioni su come eseguire questa operazione, consulta le seguenti pagine della documentazione di Adobe Campaign:
* [Introduzione all’importazione e l’esportazione dei dati](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=it) e [Caricamento dati (file)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) nella documentazione di Adobe Campaign Classic.
* [Introduzione ai processi e alla gestione dei dati](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) e [Carica file](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) nella documentazione di Adobe Campaign Standard.
