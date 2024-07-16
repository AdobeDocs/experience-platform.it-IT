---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv a xdm;mappare csv a xdm;guida interfaccia utente;mapper;mappare;preparazione dati;preparazione dati;preparazione dati;
title: Guida dell’interfaccia utente per la preparazione dei dati
description: Questo documento fornisce istruzioni su come utilizzare le funzioni di preparazione dei dati nell’interfaccia utente di Platform per mappare i file CSV su uno schema XDM.
exl-id: fafa4aca-fb64-47ff-a97d-c18e58ae4dae
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 0%

---

# Guida dell’interfaccia utente per la preparazione dei dati

Questo documento fornisce istruzioni su come utilizzare le funzioni di preparazione dei dati nell’interfaccia utente di Adobe Experience Platform per mappare i file CSV su uno schema XDM.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): framework standardizzato in base al quale Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [Identity Service](../../identity-service/home.md): ottieni una migliore visione dei singoli clienti e del loro comportamento collegando le identità tra dispositivi e sistemi.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Origini](../../sources/home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.

## Dettaglio del flusso di dati

>[!TIP]
>
>Puoi accedere ai dettagli del flusso di dati selezionando qualsiasi origine dal catalogo delle origini. Per ulteriori informazioni, vedere [panoramica origini](../../sources/home.md).

Prima di poter mappare i dati CSV su uno schema XDM, devi stabilire i dettagli del flusso di dati.

La pagina [!UICONTROL Dettagli flusso di dati] consente di scegliere se acquisire i dati CSV in un set di dati di destinazione esistente o in un nuovo set di dati di destinazione. Un set di dati esistente include uno schema di destinazione predefinito a cui mappare i dati, mentre un nuovo set di dati richiede di selezionare uno schema esistente o crearne uno nuovo a cui mappare i dati.

### Usa un set di dati di destinazione esistente

Per acquisire i dati CSV in un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**. Puoi recuperare un set di dati esistente utilizzando l&#39;opzione [!UICONTROL Ricerca avanzata] oppure scorrendo l&#39;elenco dei set di dati esistenti nel menu a discesa.

Con un set di dati selezionato, fornisci un nome per il flusso di dati e una descrizione facoltativa.

Durante questo processo, puoi anche abilitare [!UICONTROL Diagnostica errori] e [!UICONTROL Acquisizione parziale]. [!UICONTROL Diagnostica errori] consente la generazione di messaggi di errore dettagliati per eventuali record errati che si verificano nel flusso di dati, mentre [!UICONTROL L&#39;acquisizione parziale] consente di acquisire dati contenenti errori, fino a una determinata soglia definita manualmente. Per ulteriori informazioni, consulta la [panoramica sull&#39;acquisizione batch parziale](../../ingestion/batch-ingestion/partial.md).

![set di dati esistente](../images/ui/mapping/existing-dataset.png)

### Utilizza un nuovo set di dati di destinazione

Per acquisire i dati CSV in un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]**, quindi fornisci un nome per il set di dati di output e una descrizione facoltativa. Quindi, seleziona uno schema a cui mappare utilizzando l&#39;opzione [!UICONTROL Ricerca avanzata] o scorrendo l&#39;elenco degli schemi esistenti nel menu a discesa.

Con uno schema selezionato, fornisci un nome per il flusso di dati e una descrizione facoltativa, quindi applica le impostazioni [!UICONTROL Diagnostica errori] e [!UICONTROL Acquisizione parziale] desiderate per il flusso di dati. Al termine, selezionare **[!UICONTROL Avanti]**.

![nuovo-set di dati](../images/ui/mapping/new-dataset.png)

## Seleziona dati

Viene visualizzato il passaggio [!UICONTROL Seleziona dati], che fornisce un&#39;interfaccia per caricare i file locali e visualizzarne in anteprima la struttura e il contenuto. Seleziona **[!UICONTROL Scegli i file]** per caricare un file CSV dal tuo sistema locale. In alternativa, puoi trascinare e rilasciare il file CSV da caricare nel pannello [!UICONTROL Trascina i file].

>[!TIP]
>
>Al momento solo i file CSV sono supportati dal caricamento di file locali. La dimensione massima del file per ogni file è di 1 GB.

![choose-files](../images/ui/mapping/choose-files.png)

Una volta caricato il file, l’interfaccia di anteprima viene aggiornata per visualizzarne il contenuto e la struttura.

![preview-sample-data](../images/ui/mapping/preview-sample-data.png)

A seconda del file, è possibile selezionare un delimitatore di colonna come tabulazioni, virgole, barre verticali o un delimitatore di colonna personalizzato per i dati di origine. Selezionare la freccia a discesa **[!UICONTROL Delimitatore]**, quindi selezionare il delimitatore appropriato dal menu.

Al termine, selezionare **[!UICONTROL Avanti]**.

![delimitatore](../images/ui/mapping/delimiter.png)

## Mappatura

L&#39;interfaccia **[!UICONTROL mapping]** offre uno strumento completo per mappare i campi di origine dallo schema di origine ai campi XDM di destinazione appropriati nello schema di destinazione.

![map-csv-to-xdm](../images/ui/mapping/map-csv-to-xdm.png)

### Interfaccia di mappatura {#mapping-interface}

L’interfaccia di mappatura include una dashboard che fornisce informazioni sullo stato dei campi di mappatura nel contesto del flusso di lavoro di acquisizione. Il dashboard mostra i seguenti dettagli relativi ai campi di mappatura:

| Proprietà | Descrizione |
| --- | --- |
| [!UICONTROL Campi mappati] | Visualizza il numero totale di campi sorgente mappati a un campo XDM di destinazione, indipendentemente dagli errori. |
| [!UICONTROL Campi obbligatori] | Visualizza il numero di campi di mappatura obbligatori. |
| [!UICONTROL Campi di identità] | Visualizza il numero totale di campi di mappatura definiti come identità. Questi campi di mappatura sono rappresentati da un&#39;icona di impronta digitale. |
| [!UICONTROL Errori] | Visualizza il numero di campi di mappatura errati. |

![pannello superiore](../images/ui/mapping/top-panel.png)

L’interfaccia di mappatura fornisce anche un pannello di opzioni tra cui puoi scegliere per interagire meglio o filtrare i campi di mappatura.

![secondo pannello](../images/ui/mapping/second-panel.png)

Per cercare un set di mappatura specifico, selezionare **[!UICONTROL Cerca campi origine]** e immettere il nome dei dati origine che si desidera isolare.

![ricerca](../images/ui/mapping/search.png)

Seleziona **[!UICONTROL Tutti i campi di origine]** per visualizzare un menu a discesa di opzioni di filtro che consentono di limitare meglio la visualizzazione dell&#39;interfaccia di mappatura.

Le opzioni di filtro sono:

| Campi Source | Descrizione |
| --- | --- |
| [!UICONTROL Tutti i campi di origine] | Questa opzione visualizza tutti i campi sorgente dello schema di origine. Questa opzione è visualizzata per impostazione predefinita. |
| [!UICONTROL Campi obbligatori] | Questa opzione filtra lo schema di origine in modo da visualizzare solo i campi necessari per completare la mappatura. |
| [!UICONTROL Campi di identità] | Questa opzione filtra lo schema di origine in modo da visualizzare solo i campi contrassegnati per l’identità. |
| [!UICONTROL Campi mappati] | Questa opzione filtra lo schema di origine in modo da visualizzare solo i campi già mappati. |
| [!UICONTROL Campi non mappati] | Questa opzione filtra lo schema di origine in modo da visualizzare solo i campi non ancora mappati. |
| [!UICONTROL Campi con consigli] | Questa opzione filtra lo schema di origine in modo da visualizzare solo i campi che contengono i consigli di mappatura. |

Seleziona **[!UICONTROL Campi con errori]** per visualizzare tutti i campi di mappatura con errori.

![filtro](../images/ui/mapping/filter.png)

Viene visualizzata una visualizzazione isolata dei campi di mappatura errati, che consente di risolvere gli errori tramite suggerimenti di mappatura intelligente o tramite la struttura di mappatura manuale.

![campi con errori](../images/ui/mapping/fields-with-errors.png)

### Aggiungi un nuovo tipo di campo

È possibile aggiungere un nuovo campo di mappatura o un campo calcolato selezionando **[!UICONTROL Nuovo tipo di campo]**.

#### Nuovo campo di mappatura

Per aggiungere un nuovo campo di mappatura, selezionare **[!UICONTROL Nuovo tipo di campo]**, quindi selezionare **[!UICONTROL Aggiungi nuovo campo]** dal menu a discesa visualizzato.

![aggiungi-nuovo-campo](../images/ui/mapping/add-new-field.png)

Selezionare quindi il campo di origine che si desidera aggiungere dalla struttura dello schema di origine visualizzata, quindi selezionare **[!UICONTROL Seleziona]**.

![select-new-field](../images/ui/mapping/select-new-field.png)

L’interfaccia di mappatura viene aggiornata con il campo sorgente selezionato e un campo di destinazione vuoto. Seleziona **[!UICONTROL Mappa campo di destinazione]** per iniziare a mappare il nuovo campo di origine al relativo campo XDM di destinazione appropriato.

![map-target-field](../images/ui/mapping/map-target-field.png)

Viene visualizzata una struttura di schema di destinazione interattiva che consente di scorrere manualmente lo schema di destinazione e di trovare il campo XDM di destinazione appropriato per il campo di origine.

![mapping manuale](../images/ui/mapping/manual-mapping.png)

Al termine, seleziona l’icona schema per chiudere l’interfaccia dello schema di destinazione.

![albero-schema](../images/ui/mapping/schema-tree.png)

#### Campi calcolati {#calculated-fields}

I campi calcolati consentono la creazione di valori in base agli attributi nello schema di input. Questi valori possono quindi essere assegnati ad attributi nello schema di destinazione e ricevere un nome e una descrizione per consentire un riferimento più semplice. I campi calcolati hanno una lunghezza massima di 4096 caratteri.

Per creare un campo calcolato, selezionare **[!UICONTROL Nuovo tipo di campo]**, quindi selezionare **[!UICONTROL Aggiungi campo calcolato]**

![aggiungi-campo calcolato](../images/ui/mapping/add-calculated-field.png)

Viene visualizzato il pannello **[!UICONTROL Crea campo calcolato]**. La finestra di dialogo a sinistra contiene i campi, le funzioni e gli operatori supportati nei campi calcolati. Seleziona una delle schede per iniziare ad aggiungere funzioni, campi o operatori all’editor di espressioni.

| Scheda | Descrizione |
| --- | ----------- |
| [!UICONTROL Funzione] | Nella scheda Funzioni sono elencate le funzioni disponibili per la trasformazione dei dati. Per ulteriori informazioni sulle funzioni utilizzabili nei campi calcolati, leggere la guida sulle [funzioni di preparazione dati (mapper)](../functions.md). |
| [!UICONTROL Campo] | Nella scheda Campi sono elencati i campi e gli attributi disponibili nello schema di origine. |
| [!UICONTROL Operatore] | Nella scheda operatori sono elencati gli operatori disponibili per la trasformazione dei dati. |

![schede](../images/ui/mapping/tabs.png)

Puoi aggiungere manualmente campi, funzioni e operatori utilizzando l’editor di espressioni al centro. Seleziona l’editor per iniziare a creare un’espressione. Al termine, selezionare **[!UICONTROL Salva]** per continuare.

![create-calculated-field](../images/ui/mapping/create-calculated-field.png)

### Importa mappatura {#import}

Puoi riutilizzare la mappatura di un flusso di dati esistente per ridurre il tempo di configurazione manuale dell’acquisizione dei dati e limitare gli errori. Seleziona **[!UICONTROL Importa mapping]** per riutilizzare un mapping esistente.

![import-mapping](../images/ui/mapping/import-mapping.png)

Viene visualizzata la finestra [!UICONTROL Importa mapping], che fornisce un elenco di flussi di dati tra cui scegliere.

Seleziona l’icona di anteprima per visualizzare in anteprima la mappatura del flusso di dati selezionato.

![list-mapping](../images/ui/mapping/list-mapping.png)

La finestra di anteprima consente di controllare la mappatura esistente prima di importarla nel flusso di dati. Dopo aver verificato la mappatura, puoi selezionare **[!UICONTROL Indietro]** per tornare all&#39;elenco dei flussi di dati ed esaminare un altro set di mappatura, oppure puoi selezionare **[!UICONTROL Seleziona]** per continuare.

![anteprima-mappatura](../images/ui/mapping/preview-mapping.png)

In alternativa, è possibile selezionare la mappatura che si desidera importare dalla finestra elenco dei flussi di dati. Selezionare il flusso di dati contenente il mapping da importare, quindi selezionare **[!UICONTROL Seleziona]** per continuare.

![select-mapping](../images/ui/mapping/select-mapping.png)

L’interfaccia viene aggiornata con la mappatura importata.

>[!NOTE]
>
>Eventuali set di mappatura esistenti che stabilisci o consigli di mappatura ML vengono sostituiti dalla mappatura importata da un flusso di dati esistente.

![mapping-imported](../images/ui/mapping/mapping-imported.png)

Seleziona **[!UICONTROL Anteprima dati]** per visualizzare i risultati della mappatura per un massimo di 100 righe di dati di esempio dal set di dati selezionato.

![dati-anteprima](../images/ui/mapping/preview-data.png)

Durante l’anteprima, alla colonna Identity viene assegnata la priorità come primo campo, in quanto si tratta delle informazioni chiave necessarie durante la convalida dei risultati della mappatura. Al termine, selezionare **[!UICONTROL Chiudi]**.

![anteprima](../images/ui/mapping/preview-screen.png)

Per rimuovere tutti i campi di mapping, selezionare **[!UICONTROL Cancella tutti i mapping]**.

![cancella tutto](../images/ui/mapping/clear-all.png)

### Utilizzo dell’interfaccia di mappatura

Platform fornisce automaticamente consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso o correggere eventuali campi di mappatura duplicati per cancellare eventuali errori.

![interfaccia-mappatura](../images/ui/mapping/mapping-interface.png)

Selezionare l&#39;icona della lampadina nel campo di destinazione che si desidera regolare.

![mapping-recc](../images/ui/mapping/mapping-recc.png)

Viene visualizzato il pannello a comparsa [!UICONTROL Consigli di mappatura], con un elenco di campi di destinazione consigliati che possono essere mappati a un particolare campo di origine. Per impostazione predefinita, il primo consiglio viene applicato automaticamente.

A volte, per lo schema di origine sono disponibili più consigli. In questo caso, nella scheda di mappatura viene visualizzato il consiglio più importante, seguito da un’icona che contiene il numero di consigli aggiuntivi disponibili. Selezionando l’icona a forma di lampadina viene visualizzato un elenco dei consigli aggiuntivi. Puoi scegliere uno dei consigli alternativi selezionando la casella di controllo accanto al consiglio a cui desideri mappare.

Da qui, puoi modificare il campo di destinazione selezionato per correggere un errore o adattarlo al tuo caso d’uso.

In alternativa, è possibile selezionare **[!UICONTROL Seleziona manualmente]** per utilizzare manualmente la struttura di mappatura dello schema di destinazione interattivo.

![recc-panel](../images/ui/mapping/recc-panel.png)

L’interfaccia di mappatura dello schema di destinazione viene visualizzata nella stessa vista dei campi di mappatura, consentendo di modificare le coppie di mappatura all’interno della stessa schermata. Seleziona il campo di destinazione adatto al tuo caso d’uso o correggi gli errori.

![select-target-field](../images/ui/mapping/select-target-field.png)

Al termine, selezionare **[!UICONTROL Fine]** per continuare.

![fine](../images/ui/mapping/finish.png)

## Passaggi successivi

Una volta letto questo documento, hai mappato correttamente un file CSV a uno schema XDM di destinazione utilizzando l’interfaccia di mappatura nell’interfaccia utente di Platform. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica sulla preparazione dati](../home.md)
* [Panoramica sulle origini](../../sources/home.md)
* [Monitorare i flussi di dati di origine nell’interfaccia utente](../../dataflows/ui/monitor-sources.md)
