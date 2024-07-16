---
title: Acquisizione dei dati Acxiom
description: Utilizza Acxiom Data Ingestion per acquisire dati Acxiom in Real-Time CDP e arricchire profili di prime parti. Utilizza i profili di prime parti arricchiti con Acxiom per migliorare il pubblico e attivarli tra i canali di marketing.
last-substantial-update: 2024-03-19T00:00:00Z
badge: Beta
exl-id: a0a080ef-4603-437f-8a68-11dbf530ac90
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 4%

---

# Crea una connessione di origine [!DNL Acxiom Data Ingestion] e un flusso di dati nell&#39;interfaccia utente

>[!NOTE]
>
>L&#39;origine [!DNL Acxiom Data Ingestion] è in versione beta. Leggi i [termini e condizioni](../../../../home.md#terms-and-conditions) nella panoramica delle origini per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta.

Utilizza l&#39;origine [!DNL Acxiom Data Ingestion] per acquisire i dati [!DNL Acxiom] in Real-time Customer Data Platform e arricchire i profili di prime parti. Puoi quindi utilizzare i profili di prime parti arricchiti con [!DNL Acxiom] per migliorare i tipi di pubblico e attivarli tra i canali di marketing.

Leggi questa esercitazione per scoprire come creare una connessione di origine [!DNL Acxiom Data Ingestion] e un flusso di dati utilizzando l&#39;interfaccia utente di Adobe Experience Platform. L&#39;origine [!DNL Acxiom Data Ingestion] viene utilizzata per recuperare e mappare la risposta dal servizio di miglioramento [!DNL Acxiom] utilizzando Amazon S3 come punto di rilascio.

## Prerequisiti {#prerequisites}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Raccogli le credenziali richieste

Per accedere al bucket in Experience Platform, devi fornire valori validi per le seguenti credenziali:

| Credenziali | Descrizione |
| --- | --- |
| Chiave di autenticazione [!DNL Acxiom] | Chiave di autenticazione. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Chiave di accesso [!DNL Amazon S3] | ID della chiave di accesso per il bucket. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Chiave segreta [!DNL Amazon S3] | ID della chiave segreta del bucket. È possibile recuperare questo valore dal team [!DNL Acxiom]. |
| Nome del bucket | Questo è il bucket in cui verranno condivisi i file. È possibile recuperare questo valore dal team [!DNL Acxiom]. |

>[!IMPORTANT]
>
>Per connettere l&#39;account [!DNL Acxiom] all&#39;Experience Platform, è necessario avere entrambe le autorizzazioni **[!UICONTROL Visualizza origini]** e **[!UICONTROL Gestisci origini]** abilitate per il proprio account. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../../../access-control/ui/overview.md).

## Connetti il tuo account [!DNL Acxiom]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Partner dati e identità]**, seleziona **[!UICONTROL Acquisizione dati Acxiom]**, quindi seleziona **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Una scheda di origine che visualizza **[!UICONTROL Aggiungi dati]** indica che l&#39;origine dispone già di un account autenticato. D&#39;altra parte, una scheda di origine che visualizza **[!UICONTROL Configurazione]** significa che devi fornire le credenziali e creare un nuovo account per utilizzare tale origine.

![Catalogo delle origini con origine Acxiom selezionata.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-catalog.png)

### Crea un nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL Acxiom]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova interfaccia account del flusso di lavoro di origine.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-new-account.png)

| Credenziali | Descrizione |
| --- | --- |
| Nome account | Nome dell’account. |
| Descrizione | (Facoltativo) Breve spiegazione dello scopo del conto. |
| Chiave di autenticazione [!DNL Acxiom] | La chiave fornita da [!DNL Acxiom] è necessaria per l&#39;approvazione dell&#39;account. Prima di poter stabilire una connessione al database, è necessario che il valore corrisponda a quello corretto.  La chiave deve contenere 24 caratteri e può includere solo: A-Z, a-z e 0-9. |
| Chiave di accesso S3 | La chiave di accesso S3 fa riferimento alla posizione di Amazon S3. Questo viene fornito dall’amministratore quando vengono definite le autorizzazioni del ruolo S3. |
| Chiave segreta S3 | La chiave segreta S3 fa riferimento alla posizione di Amazon S3. Questo viene fornito dall’amministratore quando vengono definite le autorizzazioni del ruolo S3. |
| s3SessionToken | (Facoltativo) Il valore del token di autenticazione durante la connessione a S3. |
| serviceUrl | (Facoltativo) La posizione URL da utilizzare per la connessione a S3 in una posizione non standard. |
| Nome del bucket | (Facoltativo) Nome del bucket S3 impostato su S3 che funge da percorso iniziale nella selezione dei dati. |
| Percorso della cartella | Se vengono utilizzate sottodirectory in un bucket, puoi anche specificare un percorso come percorso iniziale nella selezione dei dati. |

### Usa un account esistente

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**.

Selezionare un account dall&#39;elenco per visualizzarne i dettagli. Dopo aver selezionato un account, seleziona **[!UICONTROL Avanti]** per procedere.

![Interfaccia account esistente del flusso di lavoro origini.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-existing-account.png)

## Seleziona dati

Seleziona il file da acquisire dal bucket e dalla sottodirectory desiderati. È possibile fornire un’anteprima dei dati una volta definito il delimitatore e il tipo di compressione. Dopo aver selezionato il file, seleziona **[!UICONTROL Avanti]** per continuare.

![Interfaccia di anteprima di file e dati selezionati del flusso di lavoro di origine.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-preview.png)

>[!NOTE]
>
>Mentre i tipi di file JSON e Parquet sono elencati, non è necessario o previsto che vengano utilizzati durante il flusso di lavoro sorgente [!DNL Acxiom].

## Fornisci i dettagli del set di dati e del flusso di dati

Quindi, devi fornire informazioni relative al set di dati e al flusso di dati.

### Dettagli del set di dati

>[!BEGINTABS]

>[!TAB Utilizza un nuovo set di dati]

Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I dati acquisiti correttamente in Experience Platform vengono memorizzati nel data lake come set di dati. Per utilizzare un nuovo set di dati, selezionare **[!UICONTROL Nuovo set di dati]**.

![Nuova interfaccia del set di dati.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-new-dataset.png)

| Dettagli nuovo set di dati | Descrizione |
| --- | --- |
| Nome set di dati di output | Nome del nuovo set di dati. |
| Descrizione | (Facoltativo) Breve spiegazione dello scopo del set di dati. |
| Schema | Elenco a discesa degli schemi esistenti nell’organizzazione. Puoi anche creare uno schema personalizzato prima del processo di configurazione sorgente. Per ulteriori informazioni, leggere la guida alla [creazione dello schema nell&#39;interfaccia utente](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Utilizza un set di dati esistente]

Per utilizzare un set di dati esistente, selezionare **[!UICONTROL Set di dati esistente]**.

Puoi selezionare **[!UICONTROL Ricerca avanzata]** per visualizzare una finestra di tutti i set di dati della tua organizzazione, inclusi i rispettivi dettagli, ad esempio se sono abilitati per l&#39;acquisizione in Real-Time Customer Profile.

![Interfaccia del set di dati esistente.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-dataset.png)

>[!ENDTABS]

+++Seleziona per i passaggi per abilitare l’acquisizione del profilo, la diagnostica degli errori e l’acquisizione parziale.

Se il set di dati è abilitato per Real-Time Customer Profile, durante questo passaggio puoi attivare/disattivare **[!UICONTROL il set di dati profilo]** per abilitare i dati per l&#39;acquisizione del profilo. È inoltre possibile utilizzare questo passaggio per abilitare **[!UICONTROL Diagnostica errori]** e **[!UICONTROL Acquisizione parziale]**.

* **[!UICONTROL Diagnostica errori]**: selezionare **[!UICONTROL Diagnostica errori]** per indicare all&#39;origine di produrre diagnostica errori a cui fare successivamente riferimento durante il monitoraggio dell&#39;attività del set di dati e dello stato del flusso di dati.
* **[!UICONTROL Acquisizione parziale]**: l&#39;acquisizione parziale in batch consente di acquisire dati contenenti errori, fino a una determinata soglia configurabile. Questa funzione consente di acquisire correttamente in Experience Platform tutti i dati accurati, mentre tutti i dati errati vengono raggruppati separatamente con informazioni sul motivo della validità.

+++

### Dettagli del flusso di dati

Una volta configurato il set di dati, devi quindi fornire dettagli sul flusso di dati, tra cui un nome, una descrizione facoltativa e le configurazioni degli avvisi.

![Interfaccia di configurazione dei dettagli del flusso di dati.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-dataset-details.png)

| Configurazioni del flusso di dati | Descrizione |
| --- | --- |
| Nome flusso di dati | Nome del flusso di dati.  Per impostazione predefinita, viene utilizzato il nome del file che si sta importando. |
| Descrizione | (Facoltativo) Breve descrizione del flusso di dati. |
| Avvisi | Experience Platform può generare avvisi basati su eventi a cui gli utenti possono abbonarsi; queste opzioni rappresentano un flusso di dati in esecuzione per attivarli.  Per ulteriori informazioni, leggere la [panoramica degli avvisi](../../alerts.md) <ul><li>**Inizio esecuzione flusso di dati origini**: selezionare questo avviso per ricevere una notifica all&#39;inizio dell&#39;esecuzione del flusso di dati.</li><li>**Esecuzione del flusso di dati origini completata**: selezionare questo avviso per ricevere una notifica se il flusso di dati termina senza errori.</li><li>**Errore di esecuzione del flusso di dati di origini**: selezionare questo avviso per ricevere una notifica se l&#39;esecuzione del flusso di dati termina con errori.</li></ul> |

## Mappatura

Utilizza l’interfaccia di mappatura per mappare i dati di origine sui campi dello schema appropriati prima di acquisire i dati da Experience Platform.  Per ulteriori informazioni, leggere la [guida alla mappatura nell&#39;interfaccia utente](../../../../../data-prep/ui/mapping.md)

![Interfaccia di mappatura.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-mapping.png)

## Pianificare l’acquisizione del flusso di dati

Quindi, utilizza l’interfaccia di pianificazione per definire la pianificazione dell’acquisizione del flusso di dati.

![Interfaccia di configurazione della pianificazione.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-scheduling.png)

| Configurazione pianificazione | Descrizione |
| --- | --- |
| Frequenza | Configura la frequenza per indicare la frequenza con cui deve essere eseguito il flusso di dati. Puoi impostare la frequenza su: <ul><li>**Una volta**: imposta la frequenza su `once` per creare un&#39;acquisizione unica. Le configurazioni di intervallo e backfill non sono disponibili quando crei un flusso di dati di acquisizione una tantum. Per impostazione predefinita, la frequenza di pianificazione è impostata su una volta.</li><li>**Minuti**: imposta la frequenza su `minute` per pianificare il flusso di dati in modo da acquisire i dati al minuto.</li><li>**Ora**: imposta la frequenza su `hour` per pianificare il flusso di dati per acquisire i dati su base oraria.</li><li>**Giorno**: imposta la frequenza su `day` per pianificare il flusso di dati in modo da acquisire i dati su base giornaliera.</li><li>**Settimana**: imposta la frequenza su `week` per pianificare il flusso di dati in modo da acquisire i dati su base settimanale.</li></ul> |
| Intervallo | Dopo aver selezionato una frequenza, puoi configurare l’impostazione dell’intervallo per stabilire l’intervallo di tempo tra ogni acquisizione. Ad esempio, se imposti la frequenza su giorno e configuri l’intervallo su 15, il flusso di dati verrà eseguito ogni 15 giorni. **Nota**: impossibile impostare l&#39;intervallo su zero. |
| Ora di inizio | La marca temporale per l’esecuzione prevista, presentata in fuso orario UTC. |
| Retrocompilazione | La retrocompilazione determina quali dati vengono inizialmente acquisiti. Se la retrocompilazione è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se la retrocompilazione è disattivata, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di avvio non verranno acquisiti. |

## Verifica il flusso di dati

Utilizza la pagina di revisione per un riepilogo del flusso di dati prima dell’acquisizione. I dettagli sono raggruppati nelle seguenti categorie:

* **Connessione** - Mostra il tipo di origine, il percorso pertinente del file di origine scelto e il numero di colonne all&#39;interno di tale file di origine.
* **Assegna set di dati e mappa campi**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati è conforme.
* **Pianificazione** - Mostra il periodo attivo, la frequenza e l&#39;intervallo della pianificazione di acquisizione.
Dopo aver rivisto il flusso di dati, fai clic su Fine e lascia un po’ di tempo per la creazione del flusso di dati.

![Pagina di revisione.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-review.png)

## Passaggi successivi

Seguendo questa esercitazione, è stato creato un flusso di dati per portare i dati batch dall&#39;origine [!DNL Acxiom] all&#39;Experience Platform. Per ulteriori risorse, consulta la documentazione descritta di seguito.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare il flusso di dati, visita l&#39;esercitazione su [account di monitoraggio e flussi di dati nell&#39;interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

### Aggiornare il flusso di dati

Per aggiornare le configurazioni per la pianificazione, la mappatura e le informazioni generali dei flussi di dati, visita il tutorial su [aggiornamento dei flussi di dati di origine nell&#39;interfaccia utente](../../update-dataflows.md).

### Eliminare il flusso di dati

È possibile eliminare i flussi di dati non più necessari o creati in modo errato utilizzando la funzione **[!UICONTROL Elimina]** disponibile nell&#39;area di lavoro **[!UICONTROL Flussi di dati]**. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l&#39;esercitazione su [eliminazione dei flussi di dati nell&#39;interfaccia utente](../../delete.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, leggere [[!DNL Acxiom] InfoBase](https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf).
