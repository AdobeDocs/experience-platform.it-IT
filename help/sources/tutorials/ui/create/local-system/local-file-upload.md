---
keywords: Experience Platform;home;argomenti popolari;sistema locale;caricamento file;mappare il file csv;mappare il file csv a xdm;mappare il file csv a xdm;guida dell'interfaccia utente;
solution: Experience Platform
title: Creare un connettore di origine per il caricamento di file locali nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente per il sistema locale per portare i file locali in Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# Creare un connettore di origine per il caricamento di file locale nell’interfaccia utente

Questo tutorial illustra i passaggi necessari per creare un connettore di origine per il caricamento di file locale al fine di acquisire i file locali in Platform utilizzando l’interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Carica file locali in Platform

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL Sistema locale] categoria, seleziona **[!UICONTROL Caricamento di file locali]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/local/catalog.png)

### Usa un set di dati esistente

Il [!UICONTROL Dettagli del flusso di dati] consente di selezionare se acquisire i dati CSV in un set di dati esistente o in un nuovo set di dati.

Per acquisire i dati CSV in un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**. Puoi recuperare un set di dati esistente utilizzando [!UICONTROL Ricerca avanzata] oppure scorrendo l’elenco dei set di dati esistenti nel menu a discesa.

Con un set di dati selezionato, fornisci un nome per il flusso di dati e una descrizione facoltativa.

Durante questo processo, puoi anche abilitare [!UICONTROL Diagnostica degli errori] e [!UICONTROL Acquisizione parziale]. [!UICONTROL Diagnostica degli errori] consente la generazione di messaggi di errore dettagliati per eventuali record errati che si verificano nel flusso di dati, mentre [!UICONTROL Acquisizione parziale] consente di acquisire dati contenenti errori, fino a una determinata soglia definita manualmente. Consulta la [panoramica dell’acquisizione in blocco parziale](../../../../../ingestion/batch-ingestion/partial.md) per ulteriori informazioni.

![existing-dataset](../../../../images/tutorials/create/local/existing-dataset.png)

### Utilizza un nuovo set di dati

Per acquisire i dati CSV in un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]** quindi fornisci un nome per il set di dati di output e una descrizione facoltativa. Quindi, seleziona uno schema a cui mappare utilizzando [!UICONTROL Ricerca avanzata] oppure scorrendo l’elenco degli schemi esistenti nel menu a discesa.

Con uno schema selezionato, fornisci un nome per il flusso di dati e una descrizione facoltativa, quindi applica il [!UICONTROL Diagnostica degli errori] e [!UICONTROL Acquisizione parziale] impostazioni desiderate per il flusso di dati. Al termine, seleziona **[!UICONTROL Successivo]**.

![new-dataset](../../../../images/tutorials/create/local/new-dataset.png)

### Selezionare i dati

Il [!UICONTROL Seleziona dati] viene visualizzata un&#39;interfaccia per caricare i file locali e visualizzarne la struttura e il contenuto in anteprima. Seleziona **[!UICONTROL Scegli i file]** per caricare un file CSV dal sistema locale. In alternativa, puoi trascinare e rilasciare il file CSV da caricare nella [!UICONTROL Trascinare i file] pannello.

>[!TIP]
>
>Al momento solo i file CSV sono supportati dal caricamento di file locali. La dimensione massima del file per ogni file è di 1 GB.

![choose-files](../../../../images/tutorials/create/local/choose-files.png)

Una volta caricato il file, l’interfaccia di anteprima viene aggiornata per visualizzarne il contenuto e la struttura.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

A seconda del file, è possibile selezionare un delimitatore di colonna come tabulazioni, virgole, barre verticali o un delimitatore di colonna personalizzato per i dati di origine. Seleziona la **[!UICONTROL Delimitatore]** e quindi selezionare il delimitatore appropriato dal menu.

Al termine, seleziona **[!UICONTROL Successivo]**.

![delimitatore](../../../../images/tutorials/create/local/delimiter.png)

## Mappatura

Il [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un’interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia di mappatura, vedi [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md).

Una volta pronti i set di mappatura, seleziona **[!UICONTROL Fine]** e attendi alcuni istanti per la creazione del nuovo flusso di dati.

![mappatura](../../../../images/tutorials/create/local/mapping.png)

## Monitoraggio dell’acquisizione di dati

Una volta mappato e creato il file CSV, puoi monitorare i dati che vengono acquisiti tramite di esso utilizzando il dashboard di monitoraggio. Per ulteriori informazioni, consulta l’esercitazione su [monitoraggio dei flussi di dati di origine nell’interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

## Passaggi successivi

Seguendo questa esercitazione, hai mappato correttamente un file CSV semplice su uno schema XDM e lo hai acquisito in Platform. Questi dati possono ora essere utilizzati da downstream [!DNL Platform] servizi quali [!DNL Real-Time Customer Profile]. Consulta la panoramica di [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) per ulteriori informazioni.
