---
keywords: e-mail;e-mail;e-mail;destinazioni;adobe campaign;campaign
title: Connessione Adobe Campaign
description: Adobe Campaign è un set di soluzioni che consentono di personalizzare e distribuire campagne su tutti i canali online e offline.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 2%

---

# Connessione Adobe Campaign

## Panoramica {#overview}

Adobe Campaign è un set di soluzioni che consentono di personalizzare e distribuire campagne su tutti i canali online e offline. Vedi [Guida introduttiva di Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) per ulteriori informazioni.

Per inviare i dati dei segmenti ad Adobe Campaign, devi prima [collegare la destinazione](#connect-destination) in Adobe Experience Platform e quindi [impostare un’importazione di dati](#import-data-into-campaign) dal percorso di archiviazione in Adobe Campaign.

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

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

Adobe Campaign supporta i seguenti tipi di connessione:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP con password]**
* **[!UICONTROL SFTP con chiave SSH]**
* **[!UICONTROL BLOB di Azure]**

Il metodo preferito per inviare dati ad Adobe Campaign è tramite [!DNL Amazon S3] o [!DNL Azure Blob].

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* Per **[!UICONTROL Amazon S3]** connessioni, è necessario fornire [!UICONTROL ID chiave di accesso] e [!UICONTROL Chiave di accesso segreto].
* Per **[!UICONTROL SFTP con password]** connessioni, è necessario fornire [!UICONTROL Dominio], [!UICONTROL Porta], [!UICONTROL Nome utente]e [!UICONTROL Password].
* Per **[!UICONTROL SFTP con chiave SSH]** connessioni, è necessario fornire [!UICONTROL Dominio], [!UICONTROL Porta], [!UICONTROL Nome utente]e [!UICONTROL Chiave SSH].
* Per **[!UICONTROL BLOB di Azure]** connessioni, è necessario fornire una stringa di connessione.
* Facoltativamente, puoi allegare la tua chiave pubblica in formato RSA per aggiungere la crittografia con PGP/GPG ai file esportati sotto **[!UICONTROL Chiave]** sezione . La chiave pubblica deve essere scritta come [!DNL Base64] stringa codificata.
* **[!UICONTROL Nome]**: Scegli un nome appropriato per la destinazione.
* **[!UICONTROL Descrizione]**: Inserisci una descrizione per la destinazione.
* **[!UICONTROL Nome blocco]**: *Per connessioni S3*. Immetti la posizione del tuo bucket S3 dove [!DNL Platform] depositerà i dati di esportazione come file CSV.
* **[!UICONTROL Percorso cartella]**: Fornisci il percorso nel percorso di archiviazione in cui [!DNL Platform] depositerà i dati di esportazione come file CSV.
* **[!UICONTROL Contenitore]**: *Per connessioni BLOB*. Il contenitore contenente il BLOB nel percorso della cartella è in.
* **[!UICONTROL Formato file]**: Seleziona **CSV** per esportare i file CSV nel percorso di archiviazione.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.


Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Attributi di destinazione {#destination-attributes}

Quando attivi i segmenti su questa destinazione, Adobe consiglia di selezionare un identificatore univoco dal [schema unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione. Per ulteriori informazioni, consulta [best practice per attivare i tipi di pubblico nelle destinazioni di marketing via e-mail](overview.md#best-practices).

## Dati esportati {#exported-data}

Per [!DNL Adobe Campaign] destinazioni, [!DNL Platform] crea un `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedi [verifica attivazione segmento](../../ui/activate-batch-profile-destinations.md#verify) nell’esercitazione sull’attivazione dei segmenti.

## Configurare l’importazione di dati in Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Tieni presente che [!DNL SFTP] limiti di archiviazione, limiti di archiviazione del database e limiti del profilo attivo in base al contratto Adobe Campaign durante l&#39;esecuzione di questa integrazione.
>* Devi pianificare, importare e mappare i segmenti esportati in Adobe Campaign utilizzando [!DNL Campaign] flussi di lavoro. Fai riferimento a [Impostazione di un’importazione ricorrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) nella documentazione di Adobe Campaign Classic e [Informazioni sulle attività di gestione dati](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) nella documentazione di Adobe Campaign Standard.
>* Il metodo preferito per inviare dati ad Adobe Campaign è tramite [!DNL Amazon S3] o [!DNL Azure Blob].


Dopo la connessione [!DNL Platform] al tuo [!DNL Amazon S3] o [!DNL Azure Blob] archiviazione, è necessario impostare l&#39;importazione di dati dal percorso di archiviazione in Adobe Campaign. Per informazioni su come eseguire questa operazione, consulta le seguenti pagine di documentazione di Adobe Campaign:
* [Guida introduttiva all’importazione e all’esportazione dei dati](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=it) e [Caricamento dati (file)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) nella documentazione di Adobe Campaign Classic.
* [Guida introduttiva ai processi e alla gestione dei dati](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) e [Load file](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) nella documentazione di Adobe Campaign Standard.
