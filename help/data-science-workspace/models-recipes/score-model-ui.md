---
keywords: Experience Platform;valutare un modello;Data Science Workspace;argomenti popolari;ui;punteggio esecuzione;punteggio risultati
solution: Experience Platform
title: Punteggio di un modello nell’interfaccia utente di Data Science Workspace
type: Tutorial
description: Il punteggio in Adobe Experience Platform Data Science Workspace può essere ottenuto inserendo i dati di input in un modello addestrato esistente. I risultati del punteggio vengono quindi memorizzati e visualizzabili in un set di dati di output specificato come nuovo batch.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Punteggio di un modello nell’interfaccia utente di Data Science Workspace

Punteggio in Adobe Experience Platform [!DNL Data Science Workspace] può essere ottenuto inserendo i dati di input in un modello già addestrato. I risultati del punteggio vengono quindi memorizzati e visualizzabili in un set di dati di output specificato come nuovo batch.

Questa esercitazione illustra i passaggi necessari per assegnare un punteggio a un modello in [!DNL Data Science Workspace] dell&#39;utente.

## Introduzione

Per completare questa esercitazione, devi avere accesso a [!DNL Experience Platform]. Se non hai accesso a un’organizzazione in [!DNL Experience Platform], contattare l&#39;amministratore di sistema prima di procedere.

Questo tutorial richiede un modello addestrato. Se non disponi di un modello addestrato, segui la [addestrare e valutare un modello nell’interfaccia utente di](./train-evaluate-model-ui.md) prima di continuare.

## Creare una nuova esecuzione di punteggio

Un’esecuzione di punteggio viene creata utilizzando configurazioni ottimizzate da un’esecuzione di apprendimento precedentemente completata e valutata. L’insieme di configurazioni ottimali per un modello viene in genere determinato esaminando le metriche di valutazione dell’esecuzione dell’addestramento.

Trova l’esecuzione di apprendimento più ottimale per utilizzare le sue configurazioni per il punteggio. Aprire quindi l&#39;esercitazione desiderata selezionando il collegamento ipertestuale associato al nome.

![Seleziona esecuzione apprendimento](../images/models-recipes/score/select-run.png)

Dall’esecuzione dell’addestramento **[!UICONTROL Valutazione]** , seleziona **[!UICONTROL Punteggio]** in alto a destra. Viene avviato un nuovo flusso di lavoro di assegnazione del punteggio.

![](../images/models-recipes/score/training_run_overview.png)

Seleziona il set di dati di punteggio di input e seleziona **[!UICONTROL Successivo]**.

![](../images/models-recipes/score/scoring_input.png)

Seleziona il set di dati di punteggio di output, ovvero il set di dati di output dedicato in cui vengono memorizzati i risultati del punteggio. Conferma la selezione e seleziona **[!UICONTROL Successivo]**.

![](../images/models-recipes/score/scoring_results.png)

Nell’ultimo passaggio del flusso di lavoro viene richiesto di configurare l’esecuzione del punteggio. Queste configurazioni vengono utilizzate dal modello per l’esecuzione del punteggio.
Non è possibile rimuovere i parametri ereditati impostati durante la creazione dei modelli. Puoi modificare o ripristinare i parametri non ereditati facendo doppio clic sul valore o selezionando l’icona Ripristina mentre passi il puntatore sulla voce.

![configurazione](../images/models-recipes/score/configuration.png)

Rivedi e conferma le configurazioni di punteggio e seleziona **[!UICONTROL Fine]**  per creare ed eseguire l’esecuzione del punteggio. Si viene indirizzati al **[!UICONTROL Esecuzioni punteggio]** e la nuova esecuzione del punteggio con **[!UICONTROL In sospeso]** viene visualizzato lo stato.

![scheda esecuzioni punteggio](../images/models-recipes/score/scoring_runs_tab.png)

È possibile visualizzare un’esecuzione di punteggio con uno dei seguenti stati:
- In sospeso
- Completa
- Non riuscito
- In esecuzione

Gli stati vengono aggiornati automaticamente. Procedi al passaggio successivo se lo stato è **[!UICONTROL Completa]** o **[!UICONTROL Non riuscito]**.

## Visualizzare i risultati del punteggio

Per visualizzare i risultati del punteggio, inizia selezionando un’esecuzione di apprendimento.

![Seleziona esecuzione apprendimento](../images/models-recipes/score/select-run.png)

Sei reindirizzato alle esecuzioni del corso di formazione **[!UICONTROL Valutazione]** pagina. Nella parte superiore della pagina di valutazione dell’esecuzione dell’apprendimento, seleziona la **[!UICONTROL Esecuzioni punteggio]** per visualizzare un elenco delle esecuzioni di punteggio esistenti.

![pagina di valutazione](../images/models-recipes/score/view_scoring_runs.png)

Quindi, seleziona un’esecuzione di punteggio per visualizzarne i dettagli.

![dettagli esecuzione](../images/models-recipes/score/view_details.png)

Se l’esecuzione del punteggio selezionata ha lo stato &quot;Completato&quot; o &quot;Non riuscito&quot;, il **[!UICONTROL Visualizza registri attività]** è disponibile. Se l’esecuzione di un punteggio non riesce, i registri di esecuzione possono fornire informazioni utili per determinare la causa dell’errore. Per scaricare i registri di esecuzione, seleziona **[!UICONTROL Visualizza registri attività]**.

![Seleziona i registri di visualizzazione](../images/models-recipes/score/view_logs.png)

Il **[!UICONTROL Visualizzare i registri attività]** viene visualizzato popover. Seleziona un URL per scaricare automaticamente i registri associati.

![](../images/models-recipes/score/activity_logs.png)

È inoltre possibile visualizzare i risultati del punteggio selezionando  **[!UICONTROL Anteprima set di dati dei risultati del punteggio]**.

![Seleziona i risultati dell’anteprima](../images/models-recipes/score/view_results.png)

Viene fornita un’anteprima del set di dati di output.

![risultati anteprima](../images/models-recipes/score/preview_results.png)

Per il set completo dei risultati del punteggio, selezionare **[!UICONTROL Set di dati dei risultati del punteggio]** nella colonna di destra.

## Passaggi successivi

Questo tutorial illustra i passaggi necessari per valutare i dati utilizzando un modello addestrato in [!DNL Data Science Workspace]. Segui l’esercitazione su [pubblicazione di un modello come servizio nell’interfaccia utente](./publish-model-service-ui.md) per consentire agli utenti della tua organizzazione di valutare i dati fornendo un facile accesso a un servizio di apprendimento automatico.
