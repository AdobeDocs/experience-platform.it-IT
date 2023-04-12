---
keywords: Experience Platform;pubblicare un modello;Data Science Workspace;argomenti comuni;valutare un servizio
solution: Experience Platform
title: Pubblicare un modello come servizio nell’interfaccia utente di Data Science Workspace
type: Tutorial
description: Adobe Experience Platform Data Science Workspace consente di pubblicare il modello addestrato e valutato come servizio, consentendo agli utenti all’interno della tua organizzazione di valutare i dati senza la necessità di creare modelli personalizzati.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Pubblicare un modello come servizio nell’interfaccia utente di Data Science Workspace

Adobe Experience Platform Data Science Workspace consente di pubblicare il modello addestrato e valutato come servizio, consentendo agli utenti all’interno della tua organizzazione di valutare i dati senza la necessità di creare modelli personalizzati.

## Introduzione

Per completare questa esercitazione, devi disporre dell’accesso a [!DNL Experience Platform]. Se non hai accesso a un&#39;organizzazione in [!DNL Experience Platform]Prima di procedere, rivolgiti all’amministratore di sistema.

Questa esercitazione richiede un modello esistente con una corretta esecuzione della formazione. Se non disponi di un modello pubblicabile, segui la [Formazione e valutazione di un modello nell’interfaccia utente](./train-evaluate-model-ui.md) esercitazione prima di continuare.

Se preferisci pubblicare un modello utilizzando le API di apprendimento automatico di Sensei, consulta [Esercitazione API](./publish-model-service-api.md).

## Pubblicare un modello {#publish-a-model}

In Adobe Experience Platform, seleziona **[!UICONTROL Modelli]** situato nella colonna di navigazione a sinistra, seleziona la **[!UICONTROL Sfoglia]** scheda per elencare tutti i modelli esistenti. Selezionare il nome del modello da pubblicare come servizio.

![](../images/models-recipes/publish-model/browse_model.png)

Seleziona **[!UICONTROL Pubblica]** in alto a destra della pagina Panoramica modello per avviare un processo di creazione del servizio.

![](../images/models-recipes/publish-model/view_training.png)

Inserisci un nome desiderato per il Servizio e, facoltativamente, fornisci una descrizione del Servizio, seleziona **[!UICONTROL Successivo]** una volta finito.

![](../images/models-recipes/publish-model/configure_training.png)

Vengono elencate tutte le esecuzioni di formazione riuscite per il modello . Il nuovo servizio erediterà le configurazioni di formazione e valutazione dall’esecuzione di formazione selezionata.

![](../images/models-recipes/publish-model/select_training_run.png)

Seleziona **[!UICONTROL Fine]** per creare il servizio e reindirizzare al **[!UICONTROL Raccolta servizi]** mostrare tutti i servizi disponibili, compreso il servizio appena creato.

![](../images/models-recipes/publish-model/service_gallery.png)

## Punteggio con un servizio {#access-a-service}

In Adobe Experience Platform, seleziona la **[!UICONTROL Servizi]** scheda situata nella colonna di navigazione a sinistra per accedere al **[!UICONTROL Raccolta servizi]**. Trova il servizio che desideri utilizzare e seleziona **[!UICONTROL Apri]**.

![](../images/models-recipes/publish-model/open_service.png)

Nella pagina della panoramica del servizio, seleziona **[!UICONTROL Punteggio]**.

![](../images/models-recipes/publish-model/score_service.png)

Seleziona un set di dati di input appropriato per l’esecuzione del punteggio, quindi seleziona **[!UICONTROL Successivo]**. Viene richiesto di eseguire lo stesso passaggio per il set di dati di punteggio. Dopo aver selezionato il set di dati di input e output, puoi aggiornare le configurazioni.

![](../images/models-recipes/publish-model/select_datasets.png)

Quando un servizio viene creato, eredita le configurazioni di punteggio predefinite. Puoi rivedere queste configurazioni e regolarle in base alle esigenze facendo doppio clic sui valori. Una volta completate le configurazioni, seleziona **[!UICONTROL Fine]** per iniziare l&#39;esecuzione del punteggio.

![](../images/models-recipes/publish-model/scoring_configs.png)

Sul servizio **Panoramica** vengono visualizzati i dettagli del nuovo processo di punteggio e il relativo avanzamento. Una volta completato il lavoro, il **[!UICONTROL Più recente]** intestazione **[!UICONTROL Punteggio]** Il contenitore viene aggiornato.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai pubblicato correttamente un Modello come servizio accessibile e hai ottenuto un punteggio dei dati utilizzando il nuovo Servizio tramite il [!UICONTROL Raccolta servizi]. Procedi all’esercitazione successiva per scoprire come [programmare l&#39;addestramento automatico e l&#39;esecuzione del punteggio su un servizio](./schedule-models-ui.md).
