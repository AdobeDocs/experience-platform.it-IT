---
title: Acquisisci i dati dei pagamenti dal tuo account di Stripe per Experience Platform utilizzando l’interfaccia utente di.
description: Scopri come acquisire i dati dei pagamenti dall’account di Stripe a Experience Platform utilizzando l’interfaccia utente.
badge: Beta
exl-id: f20c5935-a7c0-4387-b29e-73e78cab4972
source-git-commit: dd9afe650f4c83b3877f980acac66e703e9ae5d8
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 3%

---

# Acquisire i dati dei pagamenti dall&#39;account [!DNL Stripe] per Experience Platform utilizzando l&#39;interfaccia utente

>[!NOTE]
>
>L&#39;origine [!DNL Stripe] è in versione beta. Leggi i [termini e condizioni](../../../../home.md#terms-and-conditions) nella panoramica delle origini per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta.

Leggi l&#39;esercitazione seguente per scoprire come acquisire i dati dei pagamenti dall&#39;account [!DNL Stripe] a Adobe Experience Platform utilizzando l&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Autenticazione

Leggi la [[!DNL Stripe] panoramica](../../../../connectors/payments/stripe.md) per informazioni su come recuperare le credenziali di autenticazione.

## Connetti il tuo account [!DNL Stripe] {#connect}

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *Pagamenti*, selezionare **[!DNL Stripe]**, quindi **[!UICONTROL Configura]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo origini nell&#39;interfaccia utente di Experience Platform, con la scheda Stripe origine selezionata.](../../../../images/tutorials/create/stripe/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account di Stripe]**. In questa pagina è possibile utilizzare credenziali nuove o esistenti.

>[!BEGINTABS]

>[!TAB Crea un nuovo account]

Per creare un nuovo account, selezionare **[!UICONTROL Nuovo account]** e fornire un nome, una descrizione facoltativa e le credenziali.

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova interfaccia di creazione account del flusso di lavoro di origine.](../../../../images/tutorials/create/stripe/new.png)

| Credenziali | Descrizione |
| --- | --- |
| Token di accesso | Il token di accesso [!DNL Stripe]. Per informazioni su come recuperare il token di accesso, leggere la [[!DNL Stripe] guida all&#39;autenticazione](../../../../connectors/payments/stripe.md). |

>[!TAB Usa un account esistente]

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account che si desidera utilizzare dal catalogo degli account esistente.

Seleziona **[!UICONTROL Avanti]** per procedere.

![Pagina di selezione account esistente del catalogo delle origini.](../../../../images/tutorials/create/stripe/existing.png)

>[!ENDTABS]

## Selezionare i dati {#select-data}

Ora che hai accesso al tuo account, devi identificare il percorso appropriato per i dati [!DNL Stripe] che desideri acquisire. Selezionare **[!UICONTROL Percorso risorsa]**, quindi selezionare l&#39;endpoint da cui si desidera acquisire i dati. I [!DNL Stripe] endpoint disponibili sono:

* Spese
* Abbonamenti
* Rimborsi
* Transazioni saldo
* Clienti
* Prezzi

![Finestra a discesa del percorso della risorsa.](../../../../images/tutorials/create/stripe/select-resource-path.png)

Dopo aver selezionato l&#39;endpoint, l&#39;interfaccia si aggiorna in una schermata di anteprima, visualizzando la struttura dati dell&#39;endpoint [!DNL Stripe] selezionato. Seleziona **[!UICONTROL Avanti]** per procedere.

![Finestra di anteprima dei dati di Stripe.](../../../../images/tutorials/create/stripe/preview.png)

## Fornisci i dettagli del set di dati e del flusso di dati {#provide-dataset-and-dataflow-details}

Quindi, devi fornire informazioni sul set di dati e sul flusso di dati.

### Dettagli del set di dati {#dataset-details}

Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I dati acquisiti correttamente in Experience Platform vengono memorizzati nel data lake come set di dati. Durante questo passaggio, puoi creare un nuovo set di dati o utilizzare un set di dati esistente.

>[!BEGINTABS]

>[!TAB Utilizza un nuovo set di dati]

Per utilizzare un nuovo set di dati, selezionare **[!UICONTROL Nuovo set di dati]**, quindi specificare un nome e una descrizione facoltativa per il set di dati. Devi anche selezionare uno schema Experience Data Model (XDM) a cui aderisce il set di dati.

![Nuova interfaccia di selezione del set di dati.](../../../../images/tutorials/create/stripe/new-dataset.png)

| Dettagli nuovo set di dati | Descrizione |
| --- | --- |
| Nome set di dati di output | Nome del nuovo set di dati. |
| Descrizione | (Facoltativo) Breve spiegazione del nuovo set di dati. |
| Schema | Elenco a discesa degli schemi esistenti nell’organizzazione. Puoi anche creare uno schema personalizzato prima del processo di configurazione sorgente. Per ulteriori informazioni, consulta la guida su [creazione di uno schema XDM nell&#39;interfaccia utente](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Utilizza un set di dati esistente]

Se disponi già di un set di dati, seleziona **[!UICONTROL Set di dati esistente]** e quindi utilizza l&#39;opzione **[!UICONTROL Ricerca avanzata]** per visualizzare una finestra di tutti i set di dati dell&#39;organizzazione, inclusi i rispettivi dettagli, ad esempio se sono abilitati o meno per l&#39;acquisizione in Real-Time Customer Profile.

![Interfaccia di selezione del set di dati esistente.](../../../../images/tutorials/create/stripe/existing-dataset.png)

>[!ENDTABS]

+++Seleziona per i passaggi per abilitare l’acquisizione del profilo, la diagnostica degli errori e l’acquisizione parziale.

Se il set di dati è abilitato per Real-Time Customer Profile, durante questo passaggio puoi attivare/disattivare **[!UICONTROL il set di dati profilo]** per abilitare i dati per l&#39;acquisizione del profilo. È inoltre possibile utilizzare questo passaggio per abilitare **[!UICONTROL Diagnostica errori]** e **[!UICONTROL Acquisizione parziale]**.

* **[!UICONTROL Diagnostica errori]**: selezionare **[!UICONTROL Diagnostica errori]** per indicare all&#39;origine di produrre diagnostica errori a cui fare successivamente riferimento durante il monitoraggio dell&#39;attività del set di dati e dello stato del flusso di dati.
* **[!UICONTROL Acquisizione parziale]**: l&#39;acquisizione parziale in batch consente di acquisire dati contenenti errori, fino a una determinata soglia configurabile. Questa funzione consente di acquisire correttamente in Experience Platform tutti i dati accurati, mentre tutti i dati errati vengono raggruppati separatamente con informazioni sul motivo della validità.

+++

### Dettagli del flusso di dati {#dataflow-details}

Una volta configurato il set di dati, devi quindi fornire dettagli sul flusso di dati, tra cui un nome, una descrizione facoltativa e le configurazioni degli avvisi.

![Passaggio di configurazione dei dettagli del flusso di dati.](../../../../images/tutorials/create/stripe/dataflow-detail.png)

| Configurazioni del flusso di dati | Descrizione |
| --- | --- |
| Nome flusso di dati | Nome del flusso di dati.  Per impostazione predefinita, viene utilizzato il nome del file che si sta importando. |
| Descrizione | (Facoltativo) Breve descrizione del flusso di dati. |
| Avvisi | Experience Platform può generare avvisi basati su eventi a cui gli utenti possono abbonarsi. Tutte queste opzioni richiedono un flusso di dati in esecuzione per attivarle.  Per ulteriori informazioni, leggere la [panoramica degli avvisi](../../alerts.md) <ul><li>**Inizio esecuzione flusso di dati origini**: selezionare questo avviso per ricevere una notifica all&#39;inizio dell&#39;esecuzione del flusso di dati.</li><li>**Esecuzione del flusso di dati origini completata**: selezionare questo avviso per ricevere una notifica se il flusso di dati termina senza errori.</li><li>**Errore di esecuzione del flusso di dati di origini**: selezionare questo avviso per ricevere una notifica se l&#39;esecuzione del flusso di dati termina con errori.</li></ul> |

Al termine, selezionare **[!UICONTROL Avanti]** per continuare.

## Mappare i campi su uno schema XDM {#mapping}

Viene visualizzato il passaggio **[!UICONTROL Mapping]**. Utilizza l’interfaccia di mappatura per mappare i dati di origine sui campi dello schema appropriati prima di acquisire tali dati in Experience Platform. Per una guida dettagliata sull&#39;utilizzo dell&#39;interfaccia di mappatura, leggere la [Guida dell&#39;interfaccia utente della preparazione dati](../../../../../data-prep/ui/mapping.md) per ulteriori informazioni.

![Interfaccia di mappatura del flusso di lavoro di origine.](../../../../images/tutorials/create/stripe/mapping.png)

## Configurare la pianificazione dell’acquisizione {#scheduling}

Quindi, utilizza l’interfaccia di pianificazione per creare una pianificazione di acquisizione per il flusso di dati.

Seleziona il menu a discesa della frequenza per configurare la frequenza di acquisizione del flusso di dati.

![Menu a discesa Frequenza.](../../../../images/tutorials/create/stripe/frequency.png)

Puoi anche selezionare l’icona del calendario e utilizzare un calendario a comparsa per configurare l’ora di inizio dell’acquisizione.

![Calendario configurabile per la pianificazione.](../../../../images/tutorials/create/stripe/calendar.png)

| Configurazione pianificazione | Descrizione |
| --- | --- |
| Frequenza | Configura la frequenza per indicare la frequenza con cui deve essere eseguito il flusso di dati. Puoi impostare la frequenza su: <ul><li>**Una volta**: imposta la frequenza su `once` per creare un&#39;acquisizione unica. Le configurazioni di intervallo e backfill non sono disponibili quando crei un flusso di dati di acquisizione una tantum. Per impostazione predefinita, la frequenza di pianificazione è impostata su una volta.</li><li>**Minuti**: imposta la frequenza su `minute` per pianificare il flusso di dati in modo da acquisire i dati al minuto.</li><li>**Ora**: imposta la frequenza su `hour` per pianificare il flusso di dati per acquisire i dati su base oraria.</li><li>**Giorno**: imposta la frequenza su `day` per pianificare il flusso di dati in modo da acquisire i dati su base giornaliera.</li><li>**Settimana**: imposta la frequenza su `week` per pianificare il flusso di dati in modo da acquisire i dati su base settimanale.</li></ul> |
| Intervallo | Dopo aver selezionato una frequenza, puoi configurare l’impostazione dell’intervallo per stabilire l’intervallo di tempo tra ogni acquisizione. Ad esempio, se imposti la frequenza su giorno e configuri l’intervallo su 15, il flusso di dati verrà eseguito ogni 15 giorni. Impossibile impostare l&#39;intervallo su zero. Il valore dell&#39;intervallo minimo accettato per ciascuna frequenza è il seguente:<ul><li>**Una volta**: n/d</li><li>**Minuto**: 15</li><li>**Ora**: 1</li><li>**Giorno**: 1</li><li>**Settimana**: 1</li></ul> |
| Ora di inizio | La marca temporale per l’esecuzione prevista, presentata in fuso orario UTC. |
| Retrocompilazione | La retrocompilazione determina quali dati vengono inizialmente acquisiti. Se la retrocompilazione è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se la retrocompilazione è disattivata, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di inizio non verranno acquisiti. |

Dopo aver configurato la pianificazione dell&#39;acquisizione del flusso di dati, seleziona **[!UICONTROL Avanti]**.

![Interfaccia di pianificazione del flusso di lavoro di origine.](../../../../images/tutorials/create/stripe/scheduling.png)

## Verifica il flusso di dati

Il passaggio finale nel processo di creazione del flusso di dati consiste nell’esaminare il flusso di dati prima di eseguirlo. Utilizza il passaggio **[!UICONTROL Rivedi]** per rivedere i dettagli del nuovo flusso di dati prima che venga eseguito. I dettagli sono raggruppati nelle seguenti categorie:

* **Connessione**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e il numero di colonne all&#39;interno di tale file di origine.
* **Assegna set di dati e mappa i campi**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.
* **Pianificazione**: mostra il periodo, la frequenza e l&#39;intervallo attivi della pianificazione di acquisizione.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e attendi che venga creato un po&#39; di tempo.

![Passaggio di revisione del flusso di lavoro origini.](../../../../images/tutorials/create/stripe/review.png)

## Passaggi successivi

Seguendo questa esercitazione, è stato creato un flusso di dati per portare i dati dei pagamenti dall&#39;origine [!DNL Stripe] all&#39;Experience Platform. Per ulteriori risorse, consulta la documentazione descritta di seguito.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare il flusso di dati, visita l&#39;esercitazione su [account di monitoraggio e flussi di dati nell&#39;interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

### Aggiornare il flusso di dati

Per aggiornare le configurazioni per la pianificazione, la mappatura e le informazioni generali dei flussi di dati, visita il tutorial su [aggiornamento dei flussi di dati di origine nell&#39;interfaccia utente](../../update-dataflows.md).

### Eliminare il flusso di dati

È possibile eliminare i flussi di dati non più necessari o creati in modo errato utilizzando la funzione **[!UICONTROL Elimina]** disponibile nell&#39;area di lavoro **[!UICONTROL Flussi di dati]**. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l&#39;esercitazione su [eliminazione dei flussi di dati nell&#39;interfaccia utente](../../delete.md).
