---
title: Gestire il punteggio predittivo di lead e account in Real-time CDP B2B
type: Documentation
description: Questo documento fornisce informazioni sulla gestione della funzione di valutazione predittiva del lead e del conto in Experience Platform CDP B2B.
source-git-commit: 5ac8e099a6de563371f9a53a8b4816e6cf4d1953
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 2%

---

# Gestire il punteggio predittivo per lead e account in Real-time Customer Data Platform, B2B Edition

>[!NOTE]
>
>Solo gli utenti con autorizzazione Gestisci IA B2B possono creare, modificare ed eliminare gli obiettivi del punteggio.

Questa esercitazione illustra i passaggi necessari per gestire gli obiettivi del punteggio del lead predittivo e del servizio di valutazione dell’account. Gli obiettivi di punteggio possono essere sia per il profilo di persona che per il profilo di account

## Crea un nuovo punteggio

Per creare un nuovo punteggio, seleziona la **[!UICONTROL Servizi]** nella barra laterale e seleziona **[!UICONTROL Crea punteggio]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

La **[!UICONTROL Informazioni di base]** viene visualizzata la schermata che richiede di selezionare un tipo di profilo, di immettere un nome e una descrizione facoltativa. Al termine, seleziona **[!UICONTROL Successivo]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

La **[!UICONTROL Definire l&#39;obiettivo]** viene visualizzata la schermata . Seleziona la freccia a discesa, quindi seleziona un tipo di obiettivo dalla finestra a discesa visualizzata.

![plas-select-a-gol](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

La **[!UICONTROL Specifiche dell’obiettivo]** viene visualizzata la finestra di dialogo . Selezionare la freccia a discesa, quindi selezionare il nome del campo obiettivo dalla finestra a discesa visualizzata.

![plas-select-a-gol-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

La **[!UICONTROL Condizioni dell&#39;obiettivo]** viene visualizzata la selezione. Seleziona la freccia a discesa, quindi seleziona la condizione dalla finestra a discesa visualizzata.

![plas-go-specifiche-condizione](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

La **[!UICONTROL Valore obiettivo]** viene visualizzato il campo . Quindi, configura il [!UICONTROL Specifiche dell’obiettivo]. Seleziona la [!UICONTROL Immetti valore campo] e immetti il valore dell&#39;obiettivo.

>[!NOTE]
>
>È possibile aggiungere più valori di obiettivo.

![plas-gol-specific-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Per aggiungere altri campi, seleziona **[!UICONTROL Aggiungi campo]**.

![plas-gol-specific-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Per configurare l’intervallo temporale di previsione, seleziona la freccia a discesa e seleziona l’intervallo di tempo desiderato.

![arco temporale della previsione di plas](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

Il criterio di unione selezionato determina la modalità di selezione dei valori dei campi di un profilo persona. Utilizzando la freccia a discesa, seleziona il criterio di unione selezionato, quindi seleziona **[!UICONTROL Fine]**.

La **[!UICONTROL Impostazione del punteggio completata]** viene visualizzata la finestra di dialogo che conferma la creazione del nuovo punteggio. Seleziona **[!UICONTROL OK]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Il completamento di ogni processo di punteggio può richiedere fino a 24 ore.

Viene restituito al **[!UICONTROL Servizi]** scheda in cui puoi visualizzare il nuovo punteggio creato nell’elenco dei punteggi.

![plas-score-created](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Seleziona il punteggio per visualizzare i dettagli e le informazioni aggiuntive sull’ultima esecuzione.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Per informazioni più dettagliate sui codici di errore visualizzati nei dettagli dell&#39;ultima esecuzione, consulta la sezione su [codici di errore della pipeline di lead AI](#leads-ai-pipeline-error-codes) in questo documento.

## Modificare un punteggio

Per modificare un punteggio, selezionane uno dal **[!UICONTROL Servizi]** e seleziona **[!UICONTROL Modifica]** dal pannello dei dettagli aggiuntivi sul lato destro dello schermo.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

La **[!UICONTROL Modifica istanza]** viene visualizzata una finestra di dialogo in cui puoi modificare la descrizione del punteggio. Apporta le modifiche desiderate e seleziona **[!UICONTROL Salva]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>Impossibile modificare la configurazione del punteggio, in quanto questo attiverà la riqualificazione del modello e il relativo punteggio. Equivale a eliminare il punteggio e a creare un nuovo punteggio. Per modificare la configurazione del punteggio, è necessario clonare il punteggio o crearne uno nuovo.

Viene restituito al **[!UICONTROL Servizi]** scheda . Seleziona il punteggio per visualizzare i dettagli della descrizione aggiornata nel pannello dei dettagli aggiuntivi sul lato destro dello schermo.

## Clona un punteggio

Per clonare un punteggio, selezionane uno dal **[!UICONTROL Servizi]** e seleziona **[!UICONTROL Clona]** dal pannello dei dettagli aggiuntivi sul lato destro dello schermo.

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

La **[!UICONTROL Informazioni di base]** viene visualizzata la schermata . Il tipo di profilo, il nome e la descrizione vengono clonati dal punteggio originale. Modifica questi dettagli e seleziona **[!UICONTROL Successivo]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

La **[!UICONTROL Definire l&#39;obiettivo]** viene visualizzata la schermata . Completa la sezione obiettivi come faresti per creare un nuovo punteggio e seleziona **[!UICONTROL Fine]**.

Viene restituito al **[!UICONTROL Servizi]** nell’elenco puoi vedere il punteggio appena clonato.

>[!NOTE]
>
>La **[!UICONTROL Definire l&#39;obiettivo]** sezione non clonata dal punteggio originale.

## Elimina un punteggio

Per eliminare un punteggio, selezionane uno dal **[!UICONTROL Servizi]** e seleziona **[!UICONTROL Elimina]** dal pannello dei dettagli aggiuntivi sul lato destro dello schermo.

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

La **[!UICONTROL Elimina documentazione]** viene visualizzata la finestra di dialogo di conferma. Seleziona **[!UICONTROL Elimina]**.

![plas-delete-score-Confirm](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>L’eliminazione della definizione del punteggio comporta anche l’eliminazione di tutti i punteggi previsti sul profilo della persona o sul profilo del conto, ma non del gruppo di campi creato per la definizione del punteggio. Il gruppo di campi verrà lasciato &quot;orfano&quot; nel modello dati.

Viene restituito al **[!UICONTROL Servizi]** in cui non è più possibile visualizzare il punteggio nell’elenco.

## Lead dei codici di errore della pipeline API

| Codice di errore | Messaggio di errore |
| --- | --- |
| 401 | ERRORE 401. Porta la pipeline AI arrestata: account non sufficienti per il punteggio del conto. Conteggio dei conti: {}. |
| 402 | ERRORE 402. Porta la pipeline AI arrestata: contatti non sufficienti per il punteggio del contatto. Conteggio dei contatti: {}. |
| 403 | ERRORE 403. Porta la pipeline AI arrestata: volume di attività insufficiente per l&#39;addestramento dei modelli. Numero eventi: {}. |
| 404 | ERRORE 404. Porta la pipeline AI arrestata: conversioni insufficienti per l&#39;addestramento dei modelli. Numero di conversioni: {}. |
| 405 | ERRORE 405. Porta la pipeline AI arrestata: attività troppo sparse per un valido training sul modello. Solo il {} percento degli account ha un&#39;attività. |
| 406 | ERRORE 406. Porta la pipeline AI arrestata: attività troppo sparse per un valido training sul modello. Solo il {} percento dei contatti ha attività. |
| 407 | ERRORE 407. Porta la pipeline AI arrestata: il punteggio dei tipi di attività dati non corrisponde ai dati di formazione. |
| 408 | ERRORE 408. Porta la pipeline AI arrestata: tasso mancante troppo alto per le funzionalità di attività. Frequenza mancante: {}. |
| 409 | ERRORE 409. Porta la pipeline AI arrestata: l&#39;auc di prova è troppo basso. Test auc: {}. |
| 410 | ERRORE 410. Porta la pipeline AI arrestata: test auc è troppo basso dopo la sintonizzazione dei parametri. Test auc: {}. |
| 411 | ERRORE 411. Porta la pipeline AI arrestata: i dati di formazione non dispongono di conversioni sufficienti per produrre un modello affidabile. Conversioni: {}. |
| 412 | ERRORE 412. Porta la pipeline AI arrestata: i dati di test non hanno alcuna conversione per calcolare AUC-ROC. |

| Codice di avviso/informazioni | Messaggio |
| --- | --- |
| 100 | INFO 100. Lead controllo qualità AI: il conteggio dei conti è il seguente: {}. |
| 101 | INFO 101. Lead controllo qualità AI: il numero di contatti è: {}. |
| 102 | INFO 102. Lead controllo qualità AI: il conteggio delle opportunità è il seguente: {}. |
| 103 | INFO 103. Lead controllo qualità AI: test dell&#39;auc è basso. Avvia la regolazione dei parametri. Test auc: {}. |
| 200 | ATTENZIONE 200. Lead controllo qualità AI: la frequenza mancante delle caratteristiche di firmographic è: {}. |
| 201 | ATTENZIONE 201. Lead controllo qualità AI: il tasso mancante delle funzionalità di attività è: {}. |

## Passaggi successivi

Seguendo questa esercitazione, ora puoi creare e gestire correttamente i punteggi. Per ulteriori informazioni, consulta i seguenti documenti:

* [Punteggio predittivo di lead e account](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Monitorare i processi di valutazione predittivi dei lead e degli account](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
