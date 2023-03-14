---
keywords: Experience Platform;pubblicare un modello;Data Science Workspace;argomenti popolari;punteggio un servizio
solution: Experience Platform
title: Pubblicare un modello come servizio nell’interfaccia utente di Data Science Workspace
type: Tutorial
description: Adobe Experience Platform Data Science Workspace consente di pubblicare il modello come servizio addestrato e valutato, consentendo agli utenti della tua organizzazione IMS di valutare i dati senza dover creare i propri modelli.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Pubblicare un modello come servizio nell’interfaccia utente di Data Science Workspace

Adobe Experience Platform Data Science Workspace consente di pubblicare il modello come servizio addestrato e valutato, consentendo agli utenti della tua organizzazione IMS di valutare i dati senza dover creare i propri modelli.

## Introduzione

Per completare questa esercitazione, devi avere accesso a [!DNL Experience Platform]. Se non hai accesso a un’organizzazione IMS in [!DNL Experience Platform], contattare l&#39;amministratore di sistema prima di procedere.

Questo tutorial richiede un modello esistente con un’esecuzione di apprendimento corretta. Se non disponi di un modello pubblicabile, segui la [Addestra e valuta un modello nell’interfaccia utente](./train-evaluate-model-ui.md) prima di continuare.

Se preferisci pubblicare un modello utilizzando le API di apprendimento automatico di Sensei, consulta [Esercitazione API](./publish-model-service-api.md).

## Pubblicare un modello {#publish-a-model}

In Adobe Experience Platform, seleziona **[!UICONTROL Modelli]** nella colonna di navigazione a sinistra, quindi seleziona la **[!UICONTROL Sfoglia]** per elencare tutti i modelli esistenti. Seleziona il nome del modello da pubblicare come servizio.

![](../images/models-recipes/publish-model/browse_model.png)

Seleziona **[!UICONTROL Pubblica]** in alto a destra nella pagina di panoramica del modello per avviare un processo di creazione di un servizio.

![](../images/models-recipes/publish-model/view_training.png)

Immettere un nome desiderato per il servizio e, facoltativamente, fornire una descrizione del servizio, selezionare **[!UICONTROL Successivo]** al termine.

![](../images/models-recipes/publish-model/configure_training.png)

Sono elencate tutte le esecuzioni di addestramento riuscite per il modello. Il nuovo Servizio erediterà le configurazioni di formazione e punteggio dall’esecuzione di formazione selezionata.

![](../images/models-recipes/publish-model/select_training_run.png)

Seleziona **[!UICONTROL Fine]** per creare il Servizio e reindirizzare a **[!UICONTROL Raccolta servizi]** per mostrare tutti i servizi disponibili, incluso il servizio appena creato.

![](../images/models-recipes/publish-model/service_gallery.png)

## Punteggio tramite un servizio {#access-a-service}

In Adobe Experience Platform, seleziona la **[!UICONTROL Servizi]** nella colonna di navigazione a sinistra per accedere al **[!UICONTROL Raccolta servizi]**. Individuare il servizio che si desidera utilizzare e selezionare **[!UICONTROL Apri]**.

![](../images/models-recipes/publish-model/open_service.png)

Nella pagina di panoramica del servizio, seleziona **[!UICONTROL Punteggio]**.

![](../images/models-recipes/publish-model/score_service.png)

Seleziona un set di dati di input appropriato per l’esecuzione del punteggio, quindi seleziona **[!UICONTROL Successivo]**. Ti viene chiesto di eseguire lo stesso passaggio per il set di dati di punteggio. Dopo aver selezionato il set di dati di input e di output, puoi aggiornare le configurazioni.

![](../images/models-recipes/publish-model/select_datasets.png)

Quando viene creato, un servizio eredita le configurazioni di punteggio predefinite. Puoi rivedere queste configurazioni e regolarle in base alle esigenze facendo doppio clic sui valori. Una volta ottenute le configurazioni desiderate, seleziona **[!UICONTROL Fine]** per iniziare l’esecuzione del punteggio.

![](../images/models-recipes/publish-model/scoring_configs.png)

Sul sito del servizio **Panoramica** pagina, vengono visualizzati i dettagli del nuovo processo di punteggio e il relativo avanzamento. Al termine del processo, il **[!UICONTROL Più recente]** intestazione all&#39;interno del **[!UICONTROL Punteggio]** il contenitore è stato aggiornato.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai pubblicato correttamente un modello come servizio accessibile e hai assegnato un punteggio ai dati utilizzando il nuovo servizio tramite il [!UICONTROL Raccolta servizi]. Procedi al tutorial successivo per scoprire come puoi [pianificare l’esecuzione automatica di formazione e punteggio in un servizio](./schedule-models-ui.md).
