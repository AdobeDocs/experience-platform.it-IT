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
ht-degree: 1%

---

# Punteggio di un modello nell’interfaccia utente di Data Science Workspace

Il punteggio in Adobe Experience Platform [!DNL Data Science Workspace] può essere ottenuto inserendo i dati di input in un modello addestrato esistente. I risultati del punteggio vengono quindi memorizzati e visualizzabili in un set di dati di output specificato come nuovo batch.

Questo tutorial illustra i passaggi necessari per assegnare un punteggio a un modello nell&#39;interfaccia utente [!DNL Data Science Workspace].

## Introduzione

Per completare questa esercitazione, devi avere accesso a [!DNL Experience Platform]. Se non si dispone dell&#39;accesso a un&#39;organizzazione in [!DNL Experience Platform], contattare l&#39;amministratore di sistema prima di procedere.

Questo tutorial richiede un modello addestrato. Se non disponi di un modello addestrato, segui l&#39;esercitazione [addestrare e valutare un modello nell&#39;interfaccia utente](./train-evaluate-model-ui.md) prima di continuare.

## Creare una nuova esecuzione di punteggio

Un’esecuzione di punteggio viene creata utilizzando configurazioni ottimizzate da un’esecuzione di apprendimento precedentemente completata e valutata. L’insieme di configurazioni ottimali per un modello viene in genere determinato esaminando le metriche di valutazione dell’esecuzione dell’addestramento.

Trova l’esecuzione di apprendimento più ottimale per utilizzare le sue configurazioni per il punteggio. Aprire quindi l&#39;esercitazione desiderata selezionando il collegamento ipertestuale associato al nome.

![Seleziona esecuzione apprendimento](../images/models-recipes/score/select-run.png)

Dalla scheda dell&#39;esecuzione della formazione **[!UICONTROL Valutazione]**, seleziona **[!UICONTROL Punteggio]** in alto a destra dello schermo. Viene avviato un nuovo flusso di lavoro di assegnazione del punteggio.

![](../images/models-recipes/score/training_run_overview.png)

Seleziona il set di dati di punteggio di input e seleziona **[!UICONTROL Avanti]**.

![](../images/models-recipes/score/scoring_input.png)

Seleziona il set di dati di punteggio di output, ovvero il set di dati di output dedicato in cui vengono memorizzati i risultati del punteggio. Conferma la selezione e seleziona **[!UICONTROL Avanti]**.

![](../images/models-recipes/score/scoring_results.png)

Nell’ultimo passaggio del flusso di lavoro viene richiesto di configurare l’esecuzione del punteggio. Queste configurazioni vengono utilizzate dal modello per l’esecuzione del punteggio.
Non è possibile rimuovere i parametri ereditati impostati durante la creazione dei modelli. Puoi modificare o ripristinare i parametri non ereditati facendo doppio clic sul valore o selezionando l’icona Ripristina mentre passi il puntatore sulla voce.

![configurazione](../images/models-recipes/score/configuration.png)

Rivedi e conferma le configurazioni di punteggio e seleziona **[!UICONTROL Fine]** per creare ed eseguire l&#39;esecuzione del punteggio. Sei indirizzato alla scheda **[!UICONTROL Esecuzioni punteggio]** e viene visualizzata la nuova esecuzione punteggio con lo stato **[!UICONTROL In sospeso]**.

![scheda esecuzioni punteggio](../images/models-recipes/score/scoring_runs_tab.png)

È possibile visualizzare un’esecuzione di punteggio con uno dei seguenti stati:
- In sospeso
- Completo
- Non riuscito
- Esecuzione in corso

Gli stati vengono aggiornati automaticamente. Procedi al passaggio successivo se lo stato è **[!UICONTROL Completo]** o **[!UICONTROL Non riuscito]**.

## Visualizzare i risultati del punteggio

Per visualizzare i risultati del punteggio, inizia selezionando un’esecuzione di apprendimento.

![Seleziona esecuzione apprendimento](../images/models-recipes/score/select-run.png)

Sei stato reindirizzato alla pagina delle esecuzioni del corso di formazione **[!UICONTROL Valutazione]**. Nella parte superiore della pagina di valutazione dell&#39;esecuzione dell&#39;apprendimento, selezionare la scheda **[!UICONTROL Esecuzioni punteggio]** per visualizzare una lista delle esecuzioni punteggio esistenti.

![pagina di valutazione](../images/models-recipes/score/view_scoring_runs.png)

Quindi, seleziona un’esecuzione di punteggio per visualizzarne i dettagli.

![esegui dettagli](../images/models-recipes/score/view_details.png)

Se lo stato dell&#39;esecuzione del punteggio selezionato è &quot;Completato&quot; o &quot;Non riuscito&quot;, viene reso disponibile il collegamento **[!UICONTROL Visualizza registri attività]**. Se l’esecuzione di un punteggio non riesce, i registri di esecuzione possono fornire informazioni utili per determinare la causa dell’errore. Per scaricare i registri di esecuzione, selezionare **[!UICONTROL Visualizza registri attività]**.

![Seleziona i registri di visualizzazione](../images/models-recipes/score/view_logs.png)

Viene visualizzato il popover **[!UICONTROL Visualizza registri attività]**. Seleziona un URL per scaricare automaticamente i registri associati.

![](../images/models-recipes/score/activity_logs.png)

È inoltre possibile visualizzare i risultati del punteggio selezionando **[!UICONTROL Anteprima set di dati dei risultati del punteggio]**.

![Seleziona risultati anteprima](../images/models-recipes/score/view_results.png)

Viene fornita un’anteprima del set di dati di output.

![risultati anteprima](../images/models-recipes/score/preview_results.png)

Per il set completo dei risultati del punteggio, seleziona il collegamento **[!UICONTROL Set di dati dei risultati del punteggio]** nella colonna di destra.

## Passaggi successivi

Questo tutorial illustra i passaggi necessari per valutare i dati utilizzando un modello addestrato in [!DNL Data Science Workspace]. Segui l&#39;esercitazione su [pubblicazione di un modello come servizio nell&#39;interfaccia utente](./publish-model-service-ui.md) per consentire agli utenti della tua organizzazione di valutare i dati fornendo un facile accesso a un servizio di machine learning.
