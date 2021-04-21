---
keywords: Experience Platform;segnare un modello;Data Science Workspace;argomenti comuni;interfaccia utente;esecuzione del punteggio;risultati del punteggio
solution: Experience Platform
title: Punteggio di un modello nell’interfaccia utente di Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Il punteggio in Adobe Experience Platform Data Science Workspace può essere ottenuto inserendo i dati di input in un modello addestrato esistente. I risultati del punteggio vengono quindi memorizzati e visualizzati in un set di dati di output specificato come nuovo batch.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Punteggio di un modello nell’interfaccia utente di Data Science Workspace

Il punteggio in Adobe Experience Platform [!DNL Data Science Workspace] può essere ottenuto inserendo i dati di input in un modello addestrato esistente. I risultati del punteggio vengono quindi memorizzati e visualizzati in un set di dati di output specificato come nuovo batch.

Questa esercitazione illustra i passaggi necessari per valutare un modello nell&#39; interfaccia utente [!DNL Data Science Workspace] .

## Introduzione

Per completare questa esercitazione, devi disporre dell&#39;accesso a [!DNL Experience Platform]. Se non hai accesso a un&#39;organizzazione IMS in [!DNL Experience Platform], rivolgiti all&#39;amministratore di sistema prima di procedere.

Questa esercitazione richiede un modello addestrato. Se non disponi di un modello addestrato, segui il [treno e valuta un modello nell&#39;esercitazione UI](./train-evaluate-model-ui.md) prima di continuare.

## Crea una nuova esecuzione del punteggio

Un’esecuzione del punteggio viene creata utilizzando configurazioni ottimizzate da un’esecuzione di formazione completata e valutata in precedenza. L&#39;insieme di configurazioni ottimali per un modello viene in genere determinato esaminando le metriche di valutazione dell&#39;esecuzione del corso di formazione.

Trova l’esecuzione di formazione più ottimale per utilizzare le sue configurazioni per il punteggio. Quindi, apri l&#39;esecuzione di formazione desiderata selezionando il collegamento ipertestuale associato al nome.

![Seleziona l’esecuzione della formazione](../images/models-recipes/score/select-run.png)

Dalla scheda dell’esecuzione del corso di formazione **[!UICONTROL Evaluation]** , seleziona **[!UICONTROL Score]** in alto a destra nella schermata. Inizia un nuovo flusso di lavoro di punteggio.

![](../images/models-recipes/score/training_run_overview.png)

Seleziona il set di dati per il punteggio di input e seleziona **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_input.png)

Seleziona il set di dati per il punteggio di output, questo è il set di dati di output dedicato in cui vengono memorizzati i risultati del punteggio. Conferma la selezione e seleziona **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_results.png)

Il passaggio finale nel flusso di lavoro richiede di configurare l’esecuzione del punteggio. Queste configurazioni vengono utilizzate dal modello per l’esecuzione del punteggio.
Non è possibile rimuovere i parametri ereditati impostati durante la creazione dei modelli. Per modificare o ripristinare i parametri non ereditati, fai doppio clic sul valore o seleziona l’icona Ripristina mentre passi il cursore sulla voce.

![configurazione](../images/models-recipes/score/configuration.png)

Rivedi e conferma le configurazioni di punteggio e seleziona **[!UICONTROL Finish]** per creare ed eseguire l’esecuzione del punteggio. Viene visualizzata la scheda **[!UICONTROL Scoring Runs]** e la nuova esecuzione del punteggio con lo stato **[!UICONTROL Pending]** .

![scheda delle esecuzioni del punteggio](../images/models-recipes/score/scoring_runs_tab.png)

Un’esecuzione del punteggio può essere visualizzata con uno dei seguenti stati:
- In sospeso
- Completa
- Non riuscito
- In esecuzione

Gli stati vengono aggiornati automaticamente. Procedi al passaggio successivo se lo stato è **[!UICONTROL Complete]** o **[!UICONTROL Failed]**.

## Visualizza risultati punteggio

Per visualizzare i risultati del punteggio, inizia selezionando un’esecuzione di formazione.

![Seleziona l’esecuzione della formazione](../images/models-recipes/score/select-run.png)

Sei reindirizzato alla pagina dei percorsi di formazione **[!UICONTROL Evaluation]**. Nella parte superiore della pagina di valutazione dell’esecuzione del corso di formazione, seleziona la scheda **[!UICONTROL Scoring Runs]** per visualizzare un elenco delle esecuzioni di punteggio esistenti.

![pagina di valutazione](../images/models-recipes/score/view_scoring_runs.png)

Quindi, seleziona un’esecuzione del punteggio per visualizzare i dettagli dell’esecuzione.

![eseguire i dettagli](../images/models-recipes/score/view_details.png)

Se lo stato dell’esecuzione del punteggio selezionata è &quot;Completato&quot; o &quot;Non riuscito&quot;, il collegamento **[!UICONTROL View Activity Logs]** viene reso disponibile. Se un’esecuzione del punteggio non riesce, i registri di esecuzione possono fornire informazioni utili per determinare il motivo dell’errore. Per scaricare i registri di esecuzione, seleziona **[!UICONTROL View Activity Logs]**.

![Seleziona registri di visualizzazione](../images/models-recipes/score/view_logs.png)

Viene visualizzato il puntatore **[!UICONTROL View activity logs]** . Seleziona un URL per scaricare automaticamente i registri associati.

![](../images/models-recipes/score/activity_logs.png)

Puoi anche visualizzare i risultati del punteggio selezionando **[!UICONTROL Preview scoring results dataset]**.

![Seleziona risultati di anteprima](../images/models-recipes/score/view_results.png)

Viene fornita un’anteprima del set di dati di output.

![risultati dell&#39;anteprima](../images/models-recipes/score/preview_results.png)

Per l’insieme completo dei risultati del punteggio, seleziona il collegamento **[!UICONTROL Scoring Results Dataset]** che si trova nella colonna di destra.

## Passaggi successivi

Questa esercitazione illustra i passaggi necessari per valutare i dati utilizzando un modello addestrato in [!DNL Data Science Workspace]. Segui l&#39;esercitazione su [pubblicazione di un modello come servizio nell&#39;interfaccia utente](./publish-model-service-ui.md) per consentire agli utenti all&#39;interno della tua organizzazione di valutare i dati fornendo un facile accesso a un servizio di apprendimento automatico.
