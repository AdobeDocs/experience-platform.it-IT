---
keywords: Experience Platform; programmare un modello; Data Science Area di lavoro; argomenti popolari; programmare il punteggio; programmare training
solution: Experience Platform
title: Pianificare un modello in Data Science Area di lavoro interfaccia
type: Tutorial
description: Adobe Experience Platform Data Science Area di lavoro consente di impostare punteggi pianificati ed training vengono eseguiti su un servizio di Machine Learning. L'automazione del processo di training e punteggio può aiutare a mantenere e migliorare l'efficienza di un Servizio nel tempo tenendo il passo con i modelli all'interno dei dati.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Pianificare un modello in Data Science Area di lavoro interfaccia

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

Adobe Experience Platform [!DNL Data Science Workspace] consente di impostare il punteggio pianificato e le esecuzioni di formazione su un servizio di apprendimento automatico. L’automazione del processo di formazione e valutazione consente di mantenere e migliorare l’efficienza di un servizio nel tempo, tenendo il passo con i modelli all’interno dei dati.

Questo tutorial illustra i passaggi necessari per configurare le pianificazioni di formazione e punteggio su un servizio esistente tramite la [!UICONTROL Galleria servizi]. È suddiviso nelle seguenti sezioni principali:

- [Configurare il punteggio pianificato](#configure-scheduled-scoring)
- [Configurare l’apprendimento pianificato](#configure-scheduled-training)

## Introduzione

Per completare questa esercitazione, è necessario disporre di accesso a [!DNL Experience Platform]. Se non si dispone di accesso a un&#39;organizzazione in [!DNL Experience Platform], si prega di parlare con l&#39;amministratore di sistema prima di procedere.

Questo esercitazione richiede un servizio esistente. Se non si dispone di un servizio accessibile con cui lavorare, è possibile crearne uno seguendo la esercitazione per [la pubblicazione di un modello come servizio](./publish-model-service-ui.md).

## Configurare il punteggio pianificato {#configure-scheduled-scoring}

Il punteggio modello può essere configurato per essere un processo automatizzato su base pianificata. Dopo aver creato un servizio, puoi seguire i passaggi seguenti per configurare e applicare una pianificazione di punteggio:

In Adobe Experience Platform, selezionare la scheda **[!UICONTROL Servizi]** nella colonna di navigazione a sinistra per accedere a **[!DNL Service Gallery]**. Trova il servizio su cui vuoi pianificare l&#39;esecuzione del punteggio e seleziona **[!UICONTROL Apri]** per visualizzarne la pagina **[!UICONTROL Panoramica]**.

![](../images/models-recipes/schedule/select_service.png)

Nella pagina Panoramica vengono visualizzate le informazioni sul punteggio del servizio. Seleziona il collegamento **[!UICONTROL Aggiorna pianificazione]** per configurare una pianificazione di punteggio.

![](../images/models-recipes/schedule/update_scoring.png)

Configura la frequenza, la data di inizio, la data di fine, il set di dati di input e il set di dati di output per la pianificazione di punteggio. Una volta completate le configurazioni, selezionare **[!UICONTROL Crea]** per aggiornare la pianificazione del punteggio del servizio.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

La pianificazione del punteggio aggiornata viene visualizzata nella pagina **[!UICONTROL Panoramica]** del servizio.

![](../images/models-recipes/schedule/scoring_set.png)

## Configurare training pianificate {#configure-scheduled-training}

La configurazione delle training pianificate eseguite in un servizio garantisce che il modello di Machine Learning venga aggiornato ai modelli di dati più recenti. Ogni volta che viene completata un&#39;esecuzione di training pianificata, il modello addestrato risultante viene utilizzato per alimentare il servizio fino alla successiva esecuzione di training pianificata.

Una volta creato un servizio, è possibile seguire i passaggi seguenti per configurare e applicare un training programmare:

In Adobe Experience Platform, seleziona la scheda **[!UICONTROL Servizi]** nella colonna di navigazione a sinistra per accedere alla **[!UICONTROL Raccolta servizi]**. Trova il servizio su cui vuoi pianificare l&#39;esecuzione del corso di formazione e seleziona **[!UICONTROL Apri]** per visualizzarne la pagina **[!UICONTROL Panoramica]**.

![](../images/models-recipes/schedule/select_service.png)

Nella pagina Panoramica vengono visualizzate le informazioni sulla formazione del servizio. Seleziona il collegamento **[!UICONTROL Aggiorna pianificazione]** per configurare una pianificazione di formazione.

![](../images/models-recipes/schedule/update_training.png)

Configura la frequenza, la data di inizio, la data di fine e il set di dati di input utilizzati per la pianificazione dell’apprendimento. Una volta completate le configurazioni, selezionare **[!UICONTROL Crea]** per aggiornare la pianificazione di formazione del servizio.

![](../images/models-recipes/schedule/set_training_schedule.png)

La pianificazione aggiornata dei corsi di formazione è visualizzata nella pagina **[!UICONTROL Panoramica]** del servizio.

![](../images/models-recipes/schedule/training_set.png)

## Passaggi successivi

Seguendo questa esercitazione, si sono pianificate correttamente le training automatizzate e le esecuzioni di punteggio su un servizio e completato il [!DNL Data Science Workspace] esercitazione interfaccia workflow. Se non l&#39;hai già fatto, prendi in considerazione [il riavvio del esercitazione](./create-retails-sales-dataset.md) e seguire l&#39;API workflow per creare, addestrare, assegnare un punteggio e pubblicare un modello.
