---
title: Acquisisci i dati dei pagamenti dal tuo account di Stripe per Experienci Platform utilizzando l’interfaccia utente di.
description: Scopri come acquisire i dati dei pagamenti dall’account di Stripe a Experienci Platform utilizzando l’interfaccia utente.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: b5e791882ddb7cb8c87c15d4812470b3bbc9a72e
workflow-type: tm+mt
source-wordcount: '1636'
ht-degree: 3%

---

# Acquisisci i dati dei pagamenti dal tuo [!DNL Stripe] Experience Platform dell’account tramite l’interfaccia utente

>[!NOTE]
>
>Il [!DNL Stripe] sorgente in versione beta. Leggi le [termini e condizioni](../../../../home.md#terms-and-conditions) nella panoramica delle sorgenti per ulteriori informazioni sull’utilizzo di sorgenti etichettate beta.

Leggi il seguente tutorial per scoprire come acquisire i dati di pagamento dal tuo [!DNL Stripe] da Adobe Experience Platform tramite l’interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Autenticazione

Leggi le [[!DNL Stripe] panoramica](../../../../connectors/payments/stripe.md) per informazioni su come recuperare le credenziali di autenticazione.

## Connetti [!DNL Stripe] account {#connect}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *Pagamenti* categoria, seleziona **[!DNL Stripe]** e quindi selezionare **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano **[!UICONTROL Configurazione]** quando una determinata origine non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini nell’interfaccia utente di Experienci Platform, con la scheda Stripe origine selezionata.](../../../../images/tutorials/create/stripe/catalog.png)

Il **[!UICONTROL Connetti account Stripe]** viene visualizzata. In questa pagina è possibile utilizzare credenziali nuove o esistenti.

>[!BEGINTABS]

>[!TAB Crea un nuovo account]

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome, una descrizione facoltativa e le tue credenziali.

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia di creazione account del flusso di lavoro sorgenti.](../../../../images/tutorials/create/stripe/new.png)

| Credenziali | Descrizione |
| --- | --- |
| Token di accesso | Il tuo [!DNL Stripe] token di accesso. Per informazioni su come recuperare il token di accesso, leggi [[!DNL Stripe] guida all’autenticazione](../../../../connectors/payments/stripe.md). |

>[!TAB Usa un account esistente]

Per utilizzare un account esistente, seleziona **[!UICONTROL Account esistente]** quindi selezionare l&#39;account che si desidera utilizzare dal catalogo account esistente.

Seleziona **[!UICONTROL Avanti]** per procedere.

![Pagina di selezione account esistente del catalogo delle origini.](../../../../images/tutorials/create/stripe/existing.png)

>[!ENDTABS]

## Selezionare i dati {#select-data}

Ora che hai accesso al tuo account, devi identificare il percorso appropriato per [!DNL Stripe] i dati che desideri acquisire. Seleziona **[!UICONTROL Percorso risorsa]** quindi seleziona l’endpoint da cui desideri acquisire i dati. Il valore [!DNL Stripe] gli endpoint sono:

* Spese
* Abbonamenti
* Rimborsi
* Transazioni saldo
* Clienti
* Prezzi

![Finestra a discesa Percorso risorsa.](../../../../images/tutorials/create/stripe/select-resource-path.png)

Una volta selezionato l’endpoint, l’interfaccia si aggiorna in una schermata di anteprima, che mostra la struttura dati del [!DNL Stripe] endpoint selezionato. Seleziona **[!UICONTROL Avanti]** per procedere.

![Finestra di anteprima dei dati Stripe.](../../../../images/tutorials/create/stripe/preview.png)

## Fornisci i dettagli del set di dati e del flusso di dati {#provide-dataset-and-dataflow-details}

Quindi, devi fornire informazioni sul set di dati e sul flusso di dati.

### Dettagli del set di dati {#dataset-details}

Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I dati acquisiti correttamente in Experienci Platform vengono memorizzati nel data lake come set di dati. Durante questo passaggio, puoi creare un nuovo set di dati o utilizzare un set di dati esistente.

>[!BEGINTABS]

>[!TAB Utilizza un nuovo set di dati]

Per utilizzare un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]** quindi fornisci un nome e una descrizione facoltativa per il set di dati. Devi anche selezionare uno schema Experience Data Model (XDM) a cui aderisce il set di dati.

![La nuova interfaccia per la selezione dei set di dati.](../../../../images/tutorials/create/stripe/new-dataset.png)

| Dettagli nuovo set di dati | Descrizione |
| --- | --- |
| Nome set di dati di output | Nome del nuovo set di dati. |
| Descrizione | (Facoltativo) Breve spiegazione del nuovo set di dati. |
| Schema | Elenco a discesa degli schemi esistenti nell’organizzazione. Puoi anche creare uno schema personalizzato prima del processo di configurazione sorgente. Per ulteriori informazioni, consulta la guida su [creazione di uno schema XDM nell’interfaccia utente](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Usa un set di dati esistente]

Se disponi già di un set di dati, seleziona **[!UICONTROL Set di dati esistente]** e quindi utilizzare il **[!UICONTROL Ricerca avanzata]** per visualizzare una finestra di tutti i set di dati dell’organizzazione, inclusi i rispettivi dettagli, ad esempio se sono abilitati o meno per l’acquisizione in Real-Time Customer Profile.

![Interfaccia di selezione del set di dati esistente.](../../../../images/tutorials/create/stripe/existing-dataset.png)

>[!ENDTABS]

+++Seleziona per i passaggi per abilitare l’acquisizione del profilo, la diagnostica degli errori e l’acquisizione parziale.

Se il set di dati è abilitato per Real-Time Customer Profile, durante questo passaggio puoi attivare/disattivare **[!UICONTROL Set di dati profilo]** per abilitare i dati per l’acquisizione del profilo. Puoi anche utilizzare questo passaggio per abilitare **[!UICONTROL Diagnostica degli errori]** e **[!UICONTROL Acquisizione parziale]**.

* **[!UICONTROL Diagnostica degli errori]**: Seleziona **[!UICONTROL Diagnostica degli errori]** per indicare all’origine di produrre diagnostica degli errori a cui fare successivamente riferimento durante il monitoraggio dell’attività del set di dati e dello stato del flusso di dati.
* **[!UICONTROL Acquisizione parziale]**: l’acquisizione in batch parziale consente di acquisire dati contenenti errori, fino a una determinata soglia configurabile. Questa funzione consente di acquisire correttamente in Experienci Platform tutti i dati accurati, mentre tutti i dati errati vengono raggruppati separatamente con informazioni sul motivo della validità.

+++

### Dettagli del flusso di dati {#dataflow-details}

Una volta configurato il set di dati, devi quindi fornire dettagli sul flusso di dati, tra cui un nome, una descrizione facoltativa e le configurazioni degli avvisi.

![Il passaggio di configurazione dei dettagli del flusso di dati.](../../../../images/tutorials/create/stripe/dataflow-detail.png)

| Configurazioni del flusso di dati | Descrizione |
| --- | --- |
| Nome flusso di dati | Nome del flusso di dati.  Per impostazione predefinita, viene utilizzato il nome del file che si sta importando. |
| Descrizione | (Facoltativo) Breve descrizione del flusso di dati. |
| Avvisi | Experienci Platform può generare avvisi basati su eventi a cui gli utenti possono abbonarsi. Tutte queste opzioni richiedono un flusso di dati in esecuzione per attivarle.  Per ulteriori informazioni, leggere [panoramica degli avvisi](../../alerts.md) <ul><li>**Inizio esecuzione flusso di dati origini**: seleziona questo avviso per ricevere una notifica all’inizio dell’esecuzione del flusso di dati.</li><li>**Esecuzione flusso di dati origini completata**: seleziona questo avviso per ricevere una notifica se il flusso di dati termina senza errori.</li><li>**Errore di esecuzione del flusso di dati origini**: seleziona questo avviso per ricevere una notifica se l’esecuzione del flusso di dati termina con errori.</li></ul> |

Al termine, seleziona **[!UICONTROL Successivo]** per procedere.

## Mappare i campi su uno schema XDM {#mapping}

Il **[!UICONTROL Mappatura]** viene visualizzato il passaggio. Utilizza l’interfaccia di mappatura per mappare i dati di origine sui campi dello schema appropriati prima di acquisire tali dati in Experienci Platform. Per una guida dettagliata sull’utilizzo dell’interfaccia di mappatura, leggi [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md) per ulteriori informazioni.

![Interfaccia di mappatura del flusso di lavoro sorgenti.](../../../../images/tutorials/create/stripe/mapping.png)

## Configurare la pianificazione dell’acquisizione {#scheduling}

Quindi, utilizza l’interfaccia di pianificazione per creare una pianificazione di acquisizione per il flusso di dati.

Seleziona il menu a discesa della frequenza per configurare la frequenza di acquisizione del flusso di dati.

![Menu a discesa Frequenza.](../../../../images/tutorials/create/stripe/frequency.png)

Puoi anche selezionare l’icona del calendario e utilizzare un calendario a comparsa per configurare l’ora di inizio dell’acquisizione.

![Il calendario configurabile per la pianificazione.](../../../../images/tutorials/create/stripe/calendar.png)

| Configurazione pianificazione | Descrizione |
| --- | --- |
| Frequenza | Configura la frequenza per indicare la frequenza con cui deve essere eseguito il flusso di dati. Puoi impostare la frequenza su: <ul><li>**Una volta**: imposta la frequenza su `once` per creare un’acquisizione unica. Le configurazioni di intervallo e backfill non sono disponibili quando crei un flusso di dati di acquisizione una tantum. Per impostazione predefinita, la frequenza di pianificazione è impostata su una volta.</li><li>**Minuto**: imposta la frequenza su `minute` per pianificare il flusso di dati per acquisire i dati al minuto.</li><li>**Hour**:Imposta la frequenza su `hour` per pianificare il flusso di dati per acquisire i dati su base oraria.</li><li>**Giorno**: imposta la frequenza su `day` pianificare il flusso di dati per acquisire i dati su base giornaliera.</li><li>**Settimana**: imposta la frequenza su `week` per pianificare il flusso di dati per acquisire i dati settimanalmente.</li></ul> |
| Interval | Dopo aver selezionato una frequenza, puoi configurare l’impostazione dell’intervallo per stabilire l’intervallo di tempo tra ogni acquisizione. Ad esempio, se imposti la frequenza su giorno e configuri l’intervallo su 15, il flusso di dati verrà eseguito ogni 15 giorni. **Nota**: non è possibile impostare l’intervallo su zero. |
| Ora di inizio | La marca temporale per l’esecuzione prevista, presentata in fuso orario UTC. |
| Backfill | La retrocompilazione determina quali dati vengono inizialmente acquisiti. Se la retrocompilazione è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se la retrocompilazione è disattivata, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di inizio non verranno acquisiti. |

Dopo aver configurato la pianificazione di acquisizione del flusso di dati, seleziona **[!UICONTROL Successivo]**.

![Interfaccia di pianificazione del flusso di lavoro origini.](../../../../images/tutorials/create/stripe/scheduling.png)


## Verifica il flusso di dati

Il passaggio finale nel processo di creazione del flusso di dati consiste nell’esaminare il flusso di dati prima di eseguirlo. Utilizza il **[!UICONTROL Revisione]** per rivedere i dettagli del nuovo flusso di dati prima che venga eseguito. I dettagli sono raggruppati nelle seguenti categorie:

* **Connessione**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e il numero di colonne all’interno di tale file di origine.
* **Assegna set di dati e mappa campi**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.
* **Pianificazione**: mostra il periodo attivo, la frequenza e l’intervallo della pianificazione di acquisizione.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

![Passaggio Revisione del flusso di lavoro origini.](../../../../images/tutorials/create/stripe/review.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per portare i dati di pagamento dal tuo [!DNL Stripe] da sorgente a Experience Platform. Per ulteriori risorse, consulta la documentazione descritta di seguito.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare il flusso di dati, consulta l’esercitazione su [monitoraggio di account e flussi di dati nell’interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

### Aggiornare il flusso di dati

Per aggiornare le configurazioni per la pianificazione, la mappatura e le informazioni generali dei flussi di dati, visita il tutorial su [aggiornamento dei flussi di dati di origine nell’interfaccia utente](../../update-dataflows.md).

### Eliminare il flusso di dati

Puoi eliminare i flussi di dati non più necessari o creati in modo errato utilizzando **[!UICONTROL Elimina]** funzione disponibile nella **[!UICONTROL Flussi dati]** Workspace. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l’esercitazione su [eliminazione di flussi di dati nell’interfaccia utente](../../delete.md).
