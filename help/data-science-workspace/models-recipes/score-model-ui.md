---
keywords: Experience Platform;valutare un modello;Data Science Workspace;argomenti popolari;ui;punteggio esecuzione;punteggio risultati
solution: Experience Platform
title: Punteggio di un modello nell’interfaccia utente di Data Science Workspace
type: Tutorial
description: Il punteggio in Adobe Experience Platform Data Science Workspace può essere ottenuto inserendo i dati di input in un modello addestrato esistente. I risultati del punteggio vengono quindi memorizzati e visualizzabili in un set di dati di output specificato come nuovo batch.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 1%

---

# Punteggio di un modello nell’interfaccia utente di Data Science Workspace

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

Il punteggio in Adobe Experience Platform [!DNL Data Science Workspace] può essere ottenuto inserendo i dati di input in un modello addestrato esistente. I risultati del punteggio vengono quindi memorizzati e visualizzabili in un set di dati di output specificato come nuovo batch.

Questo tutorial illustra i passaggi necessari per assegnare un punteggio a un modello nell&#39;interfaccia utente [!DNL Data Science Workspace].

## Introduzione

Per completare questa esercitazione, devi avere accesso a [!DNL Experience Platform]. Se non si dispone dell&#39;accesso a un&#39;organizzazione in [!DNL Experience Platform], contattare l&#39;amministratore di sistema prima di procedere.

Questo tutorial richiede un modello addestrato. Se non disponi di un modello addestrato, segui l&#39;esercitazione [addestrare e valutare un modello nell&#39;interfaccia utente](./train-evaluate-model-ui.md) prima di continuare.

## Creare una nuova esecuzione di punteggio

Un’esecuzione di punteggio viene creata utilizzando configurazioni ottimizzate da un’esecuzione di apprendimento precedentemente completata e valutata. L’insieme di configurazioni ottimali per un modello viene in genere determinato esaminando le metriche di valutazione dell’esecuzione dell’addestramento.

Trova l’esecuzione di apprendimento più ottimale per utilizzare le sue configurazioni per il punteggio. Aprire quindi l&#39;esercitazione desiderata selezionando il collegamento ipertestuale associato al nome.

![Seleziona esecuzione apprendimento](../images/models-recipes/score/select-run.png)

Dalla scheda dell&#39;esecuzione del training **[!UICONTROL Evaluation]**, seleziona **[!UICONTROL Score]** che si trova in alto a destra dello schermo. Viene avviato un nuovo flusso di lavoro di assegnazione del punteggio.

![](../images/models-recipes/score/training_run_overview.png)

Selezionare il set di dati di punteggio di input e selezionare **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_input.png)

Seleziona il set di dati di punteggio di output, ovvero il set di dati di output dedicato in cui vengono memorizzati i risultati del punteggio. Conferma la selezione e seleziona **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_results.png)

Nell’ultimo passaggio del flusso di lavoro viene richiesto di configurare l’esecuzione del punteggio. Queste configurazioni vengono utilizzate dal modello per l’esecuzione del punteggio.
Non è possibile rimuovere i parametri ereditati impostati durante la creazione dei modelli. Puoi modificare o ripristinare i parametri non ereditati facendo doppio clic sul valore o selezionando l’icona Ripristina mentre passi il puntatore sulla voce.

![configurazione](../images/models-recipes/score/configuration.png)

Rivedere e confermare le configurazioni di punteggio e selezionare **[!UICONTROL Finish]** per creare ed eseguire l&#39;esecuzione del punteggio. Si è indirizzati alla scheda **[!UICONTROL Scoring Runs]** e viene visualizzata la nuova esecuzione del punteggio con lo stato **[!UICONTROL Pending]**.

![scheda esecuzioni punteggio](../images/models-recipes/score/scoring_runs_tab.png)

È possibile visualizzare un’esecuzione di punteggio con uno dei seguenti stati:

- In sospeso
- Completa
- Non riuscito
- Esecuzione in corso

Gli stati vengono aggiornati automaticamente. Procedere al passaggio successivo se lo stato è **[!UICONTROL Complete]** o **[!UICONTROL Failed]**.

## Visualizzare i risultati del punteggio

Per visualizzare i risultati del punteggio, inizia selezionando un’esecuzione di apprendimento.

![Seleziona esecuzione apprendimento](../images/models-recipes/score/select-run.png)

Sei stato reindirizzato alla pagina dei corsi di formazione **[!UICONTROL Evaluation]**. Nella parte superiore della pagina di valutazione dell&#39;esecuzione del training, selezionare la scheda **[!UICONTROL Scoring Runs]** per visualizzare una lista delle esecuzioni di punteggio esistenti.

![pagina di valutazione](../images/models-recipes/score/view_scoring_runs.png)

Quindi, seleziona un’esecuzione di punteggio per visualizzarne i dettagli.

![esegui dettagli](../images/models-recipes/score/view_details.png)

Se lo stato dell&#39;esecuzione del punteggio selezionata è &quot;Completato&quot; o &quot;Non riuscito&quot;, il collegamento **[!UICONTROL View Activity Logs]** verrà reso disponibile. Se l’esecuzione di un punteggio non riesce, i registri di esecuzione possono fornire informazioni utili per determinare la causa dell’errore. Per scaricare i registri di esecuzione, selezionare **[!UICONTROL View Activity Logs]**.

![Seleziona i registri di visualizzazione](../images/models-recipes/score/view_logs.png)

Verrà visualizzato il popover **[!UICONTROL View activity logs]**. Seleziona un URL per scaricare automaticamente i registri associati.

![](../images/models-recipes/score/activity_logs.png)

È inoltre possibile visualizzare i risultati del punteggio selezionando **[!UICONTROL Preview scoring results dataset]**.

![Seleziona risultati anteprima](../images/models-recipes/score/view_results.png)

Viene fornita un’anteprima del set di dati di output.

![risultati anteprima](../images/models-recipes/score/preview_results.png)

Per il set completo dei risultati del punteggio, selezionare il collegamento **[!UICONTROL Scoring Results Dataset]** nella colonna di destra.

## Passaggi successivi

Questo tutorial illustra i passaggi necessari per valutare i dati utilizzando un modello addestrato in [!DNL Data Science Workspace]. Segui l&#39;esercitazione su [pubblicazione di un modello come servizio nell&#39;interfaccia utente](./publish-model-service-ui.md) per consentire agli utenti della tua organizzazione di valutare i dati fornendo un facile accesso a un servizio di machine learning.
