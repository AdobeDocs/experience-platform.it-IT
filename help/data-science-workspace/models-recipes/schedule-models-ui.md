---
keywords: Experience Platform;pianificare un modello;Data Science Workspace;argomenti comuni;pianificare il punteggio;programmare l'addestramento
solution: Experience Platform
title: Pianificare un modello nell’interfaccia utente di Data Science Workspace
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace consente di configurare le esecuzioni programmate di punteggio e formazione su un servizio di apprendimento automatico. L'automazione del processo di formazione e valutazione può contribuire a mantenere e migliorare l'efficienza del Servizio nel tempo, mantenendo al passo i pattern all'interno dei tuoi dati.
translation-type: tm+mt
source-git-commit: 8f5b7018a52d4c5860e03cec3108435ede8815f1
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# Pianificare un modello nell’interfaccia utente di Data Science Workspace

Adobe Experience Platform [!DNL Data Science Workspace] consente di impostare le esecuzioni programmate di punteggio e formazione su un servizio di apprendimento automatico. L&#39;automazione del processo di formazione e valutazione può contribuire a mantenere e migliorare l&#39;efficienza del servizio nel tempo, tenendo il passo con i modelli all&#39;interno dei tuoi dati.

Questa esercitazione descrive i passaggi necessari per configurare le pianificazioni di formazione e valutazione per un servizio esistente tramite [!UICONTROL Service Gallery]. È suddiviso nelle seguenti sezioni principali:

- [Configurare il punteggio pianificato](#configure-scheduled-scoring)
- [Configurare l’addestramento pianificato](#configure-scheduled-training)

## Introduzione

Per completare questa esercitazione, devi disporre dell&#39;accesso a [!DNL Experience Platform]. Se non hai accesso a un&#39;organizzazione IMS in [!DNL Experience Platform], rivolgiti all&#39;amministratore di sistema prima di procedere.

Questa esercitazione richiede un servizio esistente. Se non disponi di un servizio accessibile con cui lavorare, puoi crearne uno seguendo l&#39;esercitazione per [pubblicare un modello come servizio](./publish-model-service-ui.md).

## Configura il punteggio pianificato {#configure-scheduled-scoring}

Il punteggio del modello può essere configurato in modo da essere un processo automatizzato su base pianificata. Una volta creato un servizio, puoi seguire i passaggi seguenti per configurare e applicare una pianificazione del punteggio:

In Adobe Experience Platform, seleziona la scheda **[!UICONTROL Services]** situata nella colonna di navigazione a sinistra per accedere a **[!DNL Service Gallery]**. Trova il servizio su cui desideri pianificare le esecuzioni del punteggio e seleziona **[!UICONTROL Open]** per visualizzare la relativa pagina **[!UICONTROL Overview]**.

![](../images/models-recipes/schedule/select_service.png)

Nella pagina Panoramica sono visualizzate le informazioni sul punteggio del servizio. Seleziona il collegamento **[!UICONTROL Update Schedule]** per configurare una pianificazione del punteggio.

![](../images/models-recipes/schedule/update_scoring.png)

Configura la frequenza, la data di inizio, la data di fine, il set di dati di input e il set di dati di output per la pianificazione del punteggio. Una volta completate le configurazioni, selezionare **[!UICONTROL Create]** per aggiornare la pianificazione del punteggio del servizio.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

La pianificazione del punteggio aggiornata viene visualizzata nella pagina **[!UICONTROL Overview]** del servizio.

![](../images/models-recipes/schedule/scoring_set.png)

## Configurare la formazione pianificata {#configure-scheduled-training}

La configurazione dell’addestramento pianificato viene eseguita su un servizio, in modo che il modello di apprendimento automatico venga aggiornato ai pattern di dati più recenti. Ogni volta che un&#39;esecuzione di formazione programmata viene completata, il modello di formazione risultante viene utilizzato per alimentare il servizio fino alla successiva esecuzione di formazione programmata.

Una volta creato un servizio, puoi seguire i passaggi seguenti per configurare e applicare una pianificazione del corso di formazione:

In Adobe Experience Platform, seleziona la scheda **[!UICONTROL Services]** situata nella colonna di navigazione a sinistra per accedere a **[!UICONTROL Service Gallery]**. Trova il servizio su cui desideri pianificare le esecuzioni dei corsi di formazione e seleziona **[!UICONTROL Open]** per visualizzare la relativa pagina **[!UICONTROL Overview]**.

![](../images/models-recipes/schedule/select_service.png)

Nella pagina Panoramica sono visualizzate le informazioni di formazione del servizio. Seleziona il collegamento **[!UICONTROL Update Schedule]** per configurare una pianificazione della formazione.

![](../images/models-recipes/schedule/update_training.png)

Configura la frequenza, la data di inizio, la data di fine e il set di dati di input utilizzati per la pianificazione della formazione. Una volta completate le configurazioni, selezionare **[!UICONTROL Create]** per aggiornare la pianificazione della formazione del servizio.

![](../images/models-recipes/schedule/set_training_schedule.png)

Il programma di formazione aggiornato viene visualizzato nella pagina **[!UICONTROL Overview]** del servizio.

![](../images/models-recipes/schedule/training_set.png)

## Passaggi successivi

Seguendo questa esercitazione, hai pianificato con successo l&#39;esecuzione di corsi e valutazioni automatizzati su un servizio e hai completato il flusso di lavoro dell&#39;interfaccia utente tutorial [!DNL Data Science Workspace] . Se non lo hai già fatto, considera [il riavvio dell&#39;esercitazione](./create-retails-sales-dataset.md) e segui il flusso di lavoro API per creare, addestrare, valutare e pubblicare un modello.
