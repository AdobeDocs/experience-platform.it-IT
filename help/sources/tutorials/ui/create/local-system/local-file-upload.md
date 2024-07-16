---
keywords: Experience Platform;home;argomenti popolari;sistema locale;caricamento file;mappare il file csv;mappare il file csv a xdm;mappare il file csv a xdm;guida dell'interfaccia utente;
solution: Experience Platform
title: Creare un connettore Source per il caricamento di file locali nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente per il sistema locale per portare i file locali in Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# Creare un connettore di origine per il caricamento di file locale nell’interfaccia utente

Questo tutorial illustra i passaggi necessari per creare un connettore di origine per il caricamento di file locale al fine di acquisire i file locali in Platform utilizzando l’interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Carica file locali in Platform

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL Sistema locale], selezionare **[!UICONTROL Caricamento file locale]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/local/catalog.png)

### Usa un set di dati esistente

La pagina [!UICONTROL Dettagli flusso di dati] consente di scegliere se acquisire i dati CSV in un set di dati esistente o in un nuovo set di dati.

Per acquisire i dati CSV in un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**. Puoi recuperare un set di dati esistente utilizzando l&#39;opzione [!UICONTROL Ricerca avanzata] oppure scorrendo l&#39;elenco dei set di dati esistenti nel menu a discesa.

Con un set di dati selezionato, fornisci un nome per il flusso di dati e una descrizione facoltativa.

Durante questo processo, puoi anche abilitare [!UICONTROL Diagnostica errori] e [!UICONTROL Acquisizione parziale]. [!UICONTROL Diagnostica errori] consente la generazione di messaggi di errore dettagliati per eventuali record errati che si verificano nel flusso di dati, mentre [!UICONTROL L&#39;acquisizione parziale] consente di acquisire dati contenenti errori, fino a una determinata soglia definita manualmente. Per ulteriori informazioni, consulta la [panoramica sull&#39;acquisizione batch parziale](../../../../../ingestion/batch-ingestion/partial.md).

![set di dati esistente](../../../../images/tutorials/create/local/existing-dataset.png)

### Utilizza un nuovo set di dati

Per acquisire i dati CSV in un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]**, quindi fornisci un nome per il set di dati di output e una descrizione facoltativa. Quindi, seleziona uno schema a cui mappare utilizzando l&#39;opzione [!UICONTROL Ricerca avanzata] o scorrendo l&#39;elenco degli schemi esistenti nel menu a discesa.

Con uno schema selezionato, fornisci un nome per il flusso di dati e una descrizione facoltativa, quindi applica le impostazioni [!UICONTROL Diagnostica errori] e [!UICONTROL Acquisizione parziale] desiderate per il flusso di dati. Al termine, selezionare **[!UICONTROL Avanti]**.

![nuovo-set di dati](../../../../images/tutorials/create/local/new-dataset.png)

### Selezionare i dati

Viene visualizzato il passaggio [!UICONTROL Seleziona dati], che fornisce un&#39;interfaccia per caricare i file locali e visualizzarne in anteprima la struttura e il contenuto. Seleziona **[!UICONTROL Scegli i file]** per caricare un file CSV dal tuo sistema locale. In alternativa, puoi trascinare e rilasciare il file CSV da caricare nel pannello [!UICONTROL Trascina i file].

>[!TIP]
>
>Al momento solo i file CSV sono supportati dal caricamento di file locali. La dimensione massima del file per ogni file è di 1 GB.

![choose-files](../../../../images/tutorials/create/local/choose-files.png)

Una volta caricato il file, l’interfaccia di anteprima viene aggiornata per visualizzarne il contenuto e la struttura.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

A seconda del file, è possibile selezionare un delimitatore di colonna come tabulazioni, virgole, barre verticali o un delimitatore di colonna personalizzato per i dati di origine. Selezionare la freccia a discesa **[!UICONTROL Delimitatore]**, quindi selezionare il delimitatore appropriato dal menu.

Al termine, selezionare **[!UICONTROL Avanti]**.

![delimitatore](../../../../images/tutorials/create/local/delimiter.png)

## Mappatura

Viene visualizzato il passaggio [!UICONTROL Mappatura] che fornisce un&#39;interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia di mappatura, consulta la [Guida dell&#39;interfaccia utente della preparazione dati](../../../../../data-prep/ui/mapping.md).

Quando i set di mappatura sono pronti, seleziona **[!UICONTROL Fine]** e consenti la creazione del nuovo flusso di dati per alcuni istanti.

![mappatura](../../../../images/tutorials/create/local/mapping.png)

## Monitorare l’acquisizione dei dati

Una volta mappato e creato il file CSV, puoi monitorare i dati che vengono acquisiti tramite di esso utilizzando il dashboard di monitoraggio. Per ulteriori informazioni, consulta l&#39;esercitazione sui [flussi di dati delle origini di monitoraggio nell&#39;interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

## Passaggi successivi

Seguendo questa esercitazione, hai mappato correttamente un file CSV semplice su uno schema XDM e lo hai acquisito in Platform. Questi dati possono ora essere utilizzati dai servizi [!DNL Platform] downstream come [!DNL Real-Time Customer Profile]. Per ulteriori informazioni, vedere la panoramica di [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md).
