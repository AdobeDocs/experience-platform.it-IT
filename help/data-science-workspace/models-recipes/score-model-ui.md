---
keywords: Experience Platform;score a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Punteggio di un modello (interfaccia utente)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# Punteggio di un modello (interfaccia utente)

Il punteggio nel Adobe Experience Platform  [!DNL Data Science Workspace] può essere ottenuto inserendo i dati in un modello già preparato. I risultati del punteggio vengono quindi memorizzati e visualizzati in un set di dati di output specificato come nuovo batch.

Questa esercitazione illustra i passaggi necessari per segnare un modello nell&#39;interfaccia [!DNL Data Science Workspace] utente.

## Introduzione

Per completare questa esercitazione, è necessario avere accesso a [!DNL Experience Platform]. Se non disponete dell&#39;accesso a un&#39;organizzazione IMS in [!DNL Experience Platform], rivolgetevi all&#39;amministratore di sistema prima di procedere.

Questa esercitazione richiede un modello qualificato. Se non si dispone di un modello qualificato, seguire il [treno e valutare un modello nell’esercitazione dell’interfaccia utente](./train-evaluate-model-ui.md) prima di continuare.

## Creazione di una nuova esecuzione del punteggio

Un’esecuzione del punteggio viene creata utilizzando configurazioni ottimizzate partendo da un’esecuzione di formazione precedentemente completata e valutata. L&#39;insieme di configurazioni ottimali per un modello viene in genere determinato analizzando le metriche di valutazione dell&#39;esecuzione della formazione.

1. Trovate l&#39;esecuzione di formazione ottimale per utilizzare le relative configurazioni per il punteggio. Aprite l’esecuzione della formazione desiderata facendo clic sul suo nome.

2. Dalla scheda Esecuzione formazione **[!UICONTROL Evaluation]** , fate clic sul **[!UICONTROL Score]** pulsante in alto a destra dello schermo. Verrà avviato un nuovo flusso di lavoro *Esegui punteggio* .
   ![](../images/models-recipes/score/training_run_overview.png)

3. Selezionare il set di dati per il punteggio di input e fare clic su **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_input.png)

4. Selezionare il set di dati per il punteggio di output. Si tratta del set di dati di output dedicato in cui sono memorizzati i risultati del punteggio. Confermate la selezione e fate clic **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_results.png)

5. Il passaggio finale del flusso di lavoro richiede di configurare l’esecuzione del punteggio. Queste configurazioni vengono utilizzate dal modello per l&#39;esecuzione del punteggio.
Non sarà possibile rimuovere i parametri ereditati impostati durante la creazione del modello. Per modificare o ripristinare i parametri non ereditati, fai doppio clic sul valore o fai clic sull’icona di ripristino mentre passi il cursore sulla voce.
   ![](../images/models-recipes/score/configuration.png)
Rivedete e confermate le configurazioni di punteggio e fate clic **[!UICONTROL Finish]** per creare ed eseguire l&#39;esecuzione del punteggio. Vengono indirizzati alla scheda Esecuzione *punteggio* e viene visualizzato uno stato nella nuova esecuzione del punteggio.
   ![](../images/models-recipes/score/scoring_runs_tab.png)
Un&#39;esecuzione del punteggio visualizzerà uno dei quattro stati seguenti: In sospeso, Completato, Non riuscito o In esecuzione e vengono aggiornati automaticamente. Procedete con il passaggio successivo se lo stato è &quot;Completato&quot; o &quot;Non riuscito&quot;.

## Visualizza risultati punteggio

1. Individuate l’esecuzione della formazione utilizzata per l’esecuzione del punteggio e fate clic sul nome per visualizzarne la **[!UICONTROL Evaluation]** pagina.

2. Nella parte superiore della pagina di valutazione dell’esecuzione della formazione, fate clic sulla **[!UICONTROL Scoring Runs]** scheda per visualizzare un elenco delle esecuzioni di valutazione esistenti. Fare clic sull&#39;elenco dei punteggi per visualizzarne i dettagli nella colonna a destra.
   ![](../images/models-recipes/score/view_details.png)

3. Se l’esecuzione del punteggio selezionata ha lo stato &quot;Completato&quot; o &quot;Non riuscito&quot;, il **[!UICONTROL View Activity Logs]** collegamento trovato nella colonna destra sarà attivo. Fate clic sul collegamento per visualizzare o scaricare i registri di esecuzione. Se un&#39;esecuzione del punteggio non è riuscita, i log di esecuzione possono fornire informazioni utili per determinare il motivo dell&#39;errore.
   ![](../images/models-recipes/score/activity_logs.png)

4. Fate clic sul **[!UICONTROL Preview Scoring Results Dataset]** collegamento presente nella colonna di destra. Sarà possibile visualizzare un&#39;anteprima del set di dati di output dall&#39;esecuzione del punteggio.
   ![](../images/models-recipes/score/preview_results.png)

5. Per l&#39;insieme completo dei risultati del punteggio, fai clic sul **[!UICONTROL Scoring Results Dataset]** collegamento presente nella colonna a destra.

## Passaggi successivi

Questa esercitazione illustra i passaggi necessari per eseguire la valutazione dei dati utilizzando un Modello addestrato in [!DNL Data Science Workspace]. Seguite l&#39;esercitazione sulla [pubblicazione di un modello come servizio nell&#39;interfaccia utente](./publish-model-service-ui.md) per consentire agli utenti all&#39;interno dell&#39;organizzazione di valutare i dati fornendo un accesso semplice a un servizio di machine learning.
