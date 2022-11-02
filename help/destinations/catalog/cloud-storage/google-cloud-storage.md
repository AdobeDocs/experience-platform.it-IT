---
title: (Beta) Connessione Google Cloud Storage
description: Scopri come connettersi a Google Cloud Storage e attivare segmenti o esportare set di dati.
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---

# (Beta) [!DNL Google Cloud Storage] connection

>[!IMPORTANT]
>
>Questa destinazione è attualmente in versione beta ed è disponibile solo per un numero limitato di clienti. Per richiedere l’accesso al [!DNL Google Cloud Storage] contatta il tuo rappresentante di Adobe e fornisci [!DNL Organization ID].

## Panoramica {#overview}

Creare una connessione in uscita diretta con [!DNL Google Cloud Storage] per esportare periodicamente i file di dati da Adobe Experience Platform nei blocchi personali.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema applicabili, come scelto nella schermata Seleziona attributi profilo della [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Batch]** | Le destinazioni batch esportano file su piattaforme downstream con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni [destinazioni batch basate su file](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Configurazione obbligatoria per la connessione [!DNL Google Cloud Storage] account {#prerequisites}

Per collegare Platform a [!DNL Google Cloud Storage], è innanzitutto necessario abilitare l&#39;interoperabilità per [!DNL Google Cloud Storage] conto. Per accedere all&#39;impostazione di interoperabilità, aprire [!DNL Google Cloud Platform] e seleziona **[!UICONTROL Impostazioni]** dal **[!UICONTROL Archiviazione cloud]** nel pannello di navigazione.

![Dashboard di Google Cloud Platform con Cloud Storage e impostazioni evidenziate.](/help/sources/images/tutorials/create/google-cloud-storage/nav.png)

La **[!UICONTROL Impostazioni]** viene visualizzata la pagina . Da qui puoi vedere le informazioni relative al tuo [!DNL Google] ID progetto e dettagli [!DNL Google Cloud Storage] conto. Per accedere alle impostazioni di interoperabilità, selezionare **[!UICONTROL Interoperabilità]** dall’intestazione superiore.

![La scheda Interoperabilità evidenziata nel dashboard di Google Cloud Platform.](/help/sources/images/tutorials/create/google-cloud-storage/project-access.png)

La **[!UICONTROL Interoperabilità]** contiene informazioni sull’autenticazione, le chiavi di accesso e il progetto predefinito associato all’account del servizio. Per generare un nuovo ID chiave di accesso e una chiave di accesso segreta per l’account del servizio, seleziona **[!UICONTROL Creare una chiave per un account di servizio]**.

![Crea una chiave per un controllo account del servizio evidenziato nel dashboard di Google Cloud Platform.](/help/sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Puoi usare il tuo ID chiave di accesso appena generato e la chiave di accesso segreto per collegare il tuo [!DNL Google Cloud Storage] a Platform.

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](/help/destinations/ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti e seleziona **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL ID chiave di accesso]**: Una stringa alfanumerica di 61 caratteri utilizzata per autenticare il tuo [!DNL Google Cloud Storage] a Platform. Per informazioni su come ottenere questo valore, consulta la [prerequisiti](#prerequisites) sezione precedente.
* **[!UICONTROL Chiave di accesso segreta]**: Una stringa con codifica base a 64 caratteri utilizzata per l&#39;autenticazione [!DNL Google Cloud Storage] a Platform. Per informazioni su come ottenere questo valore, consulta la [prerequisiti](#prerequisites) sezione precedente.
* **[!UICONTROL Chiave di crittografia]**: Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come [!DNL Base64-encoded] stringa. Visualizza un esempio di una chiave con codifica base64 formattata correttamente nel collegamento della documentazione sottostante. La parte centrale è ridotta per brevità.

   ![Immagine che mostra un esempio di chiave PGP formattata correttamente e crittografata in base64 nell’interfaccia utente](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Per ulteriori informazioni su questi valori, consulta la sezione [Chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guida. Per i passaggi su come generare il tuo ID chiave di accesso e la chiave di accesso segreta, consulta [[!DNL Google Cloud Storage] panoramica di origine](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: Facoltativo. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione.
* **[!UICONTROL Nome blocco]**: Immetti il nome della [!DNL Google Cloud Storage] bucket utilizzato da questa destinazione.
* **[!UICONTROL Percorso cartella]**: Immettere il percorso della cartella di destinazione che ospiterà i file esportati.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Pianificazione

In **[!UICONTROL Pianificazione]** passo, puoi [impostare il programma di esportazione](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) per [!DNL Google Cloud Storage] destinazione e [configurare il nome dei file esportati](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappare attributi e identità {#map}

In **[!UICONTROL Mappatura]** puoi selezionare i campi attributo e identità da esportare per i profili. Puoi anche scegliere di modificare le intestazioni nel file esportato con qualsiasi nome descrittivo che desideri. Per ulteriori informazioni, consulta la sezione [fase di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) nell’esercitazione per l’interfaccia utente attiva destinazioni batch .

## (Beta) Esportare i set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta la sezione [esercitazione sui set di dati di esportazione](/help/destinations/ui/export-datasets.md).

## Convalida dell’esportazione dei dati riuscita {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla il tuo [!DNL Google Cloud Storage] e assicurati che i file esportati contengano le popolazioni di profilo previste.
