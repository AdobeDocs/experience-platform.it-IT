---
title: Destinazione Data Landing Zone
description: Scopri come connettersi alla Data Landing Zone per attivare segmenti ed esportare set di dati.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# (Beta) Destinazione della zona di destinazione dei dati

>[!IMPORTANT]
>
>Questa destinazione è attualmente in versione beta ed è disponibile solo per un numero limitato di clienti. Per richiedere l’accesso al [!DNL Data Landing Zone] contatta il tuo rappresentante di Adobe e fornisci [!DNL Organization ID].


## Panoramica {#overview}

[!DNL Data Landing Zone] è un [!DNL Azure Blob] l’interfaccia di archiviazione fornita da Adobe Experience Platform consente di accedere a una struttura di archiviazione file sicura basata su cloud per esportare i file fuori da Platform. Hai accesso a uno [!DNL Data Landing Zone] Il contenitore per sandbox e il volume totale di dati in tutti i contenitori è limitato ai dati totali forniti con la licenza Platform Products and Services . Tutti i clienti di Platform e dei relativi servizi applicativi, quali [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]e [!DNL Real-Time Customer Data Platform] dispongono di un provisioning [!DNL Data Landing Zone] contenitore per sandbox. È possibile leggere e scrivere file nel contenitore attraverso [!DNL Azure Storage Explorer] o l&#39;interfaccia della riga di comando.

[!DNL Data Landing Zone] supporta l’autenticazione basata su SAS e i relativi dati sono protetti con standard [!DNL Azure Blob] meccanismi di sicurezza dello stoccaggio a riposo e in transito. L&#39;autenticazione basata su SAS consente di accedere in modo sicuro ai [!DNL Data Landing Zone] container tramite una connessione internet pubblica. Non sono necessarie modifiche di rete per accedere al [!DNL Data Landing Zone] , il che significa che non è necessario configurare elenchi consentiti o configurazioni di più aree per la rete.

Platform applica un TTL (time-to-live) di sette giorni su tutti i file caricati in un [!DNL Data Landing Zone] contenitore. Tutti i file vengono eliminati dopo sette giorni.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema applicabili (ad esempio il tuo PPID), come scelto nella schermata Seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Batch]** | Le destinazioni batch esportano file su piattaforme downstream con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni [destinazioni batch basate su file](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Gestire i contenuti [!DNL Data Landing Zone]

È possibile utilizzare [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) per gestire i contenuti del [!DNL Data Landing Zone] contenitore.

In [!DNL Azure Storage Explorer] Nell’interfaccia utente, seleziona l’icona di connessione nella barra di navigazione a sinistra. La **Seleziona risorsa** viene visualizzata una finestra in cui sono disponibili le opzioni per la connessione. Seleziona **[!DNL Blob container]** per connettersi al [!DNL Data Landing Zone] archiviazione.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Quindi, seleziona **URL firma di accesso condiviso (SAS)** come metodo di connessione, quindi selezionare **Successivo**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Dopo aver selezionato il metodo di connessione, è necessario fornire un **nome visualizzato** e **[!DNL Blob]URL SAS contenitore** che corrisponde al tuo [!DNL Data Landing Zone] contenitore.

>[!IMPORTANT]
>
>Devi utilizzare le API di Platform per recuperare le credenziali dell’area di destinazione dei dati. Per informazioni complete, consulta [Recuperare le credenziali della zona di destinazione dei dati](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html?lang=en#retrieve-data-landing-zone-credentials).
>
> Per recuperare le credenziali e accedere ai file esportati, è necessario sostituire il parametro di query `type=user_drop_zone` con `type=dlz_destination` in qualsiasi chiamata HTTP descritta nella pagina precedente.

Fornisci le [!DNL Data Landing Zone] URL SAS, quindi selezionare **Successivo**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

La **Riepilogo** viene visualizzata una finestra che fornisce una panoramica delle impostazioni, incluse informazioni sulle [!DNL Blob] endpoint e autorizzazioni. Quando è pronto, seleziona **Connetti**.

![sommario](/help/sources/images/tutorials/create/dlz/summary.png)

Una connessione corretta aggiorna la [!DNL Azure Storage Explorer] Interfaccia utente con [!DNL Data Landing Zone] contenitore.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Con il tuo [!DNL Data Landing Zone] contenitore collegato a [!DNL Azure Storage Explorer], ora puoi iniziare a esportare i file da Experience Platform al tuo [!DNL Data Landing Zone] contenitore. Per esportare i file, è necessario stabilire una connessione al [!DNL Data Landing Zone] nell’interfaccia utente di Experience Platform, come descritto nella sezione seguente.

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

Perché [!DNL Data Landing Zone] è un archivio con provisioning di Adobe, non è necessario eseguire alcuna operazione per l&#39;autenticazione nella destinazione.

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: Facoltativo. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione.
* **[!UICONTROL Percorso cartella]**: Immettere il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Tipo di file]**: selezionare l&#39;Experience Platform di formato da utilizzare per i file esportati. Quando selezioni [!UICONTROL CSV] è inoltre possibile [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato di compressione]**: selezionare il tipo di compressione che l&#39;Experience Platform deve utilizzare per i file esportati.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Pianificazione

In **[!UICONTROL Pianificazione]** passo, puoi [impostare il programma di esportazione](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) per [!DNL Data Landing Zone] destinazione e [configurare il nome dei file esportati](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappare attributi e identità {#map}

In **[!UICONTROL Mappatura]** puoi selezionare i campi attributo e identità da esportare per i profili. Puoi anche scegliere di modificare le intestazioni nel file esportato con qualsiasi nome descrittivo che desideri. Per ulteriori informazioni, consulta la sezione [fase di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) nell’esercitazione per l’interfaccia utente attiva destinazioni batch .

## (Beta) Esportare i set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta la sezione [esercitazione sui set di dati di esportazione](/help/destinations/ui/export-datasets.md).

## Convalida dell’esportazione dei dati riuscita {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla il tuo [!DNL Data Landing Zone] e assicurati che i file esportati contengano le popolazioni di profili previste.
