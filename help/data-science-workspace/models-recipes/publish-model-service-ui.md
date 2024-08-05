---
keywords: Experience Platform;pubblicare un modello;Data Science Workspace;argomenti popolari;punteggio un servizio
solution: Experience Platform
title: Publish a Model as a Service nell’interfaccia utente di Data Science Workspace
type: Tutorial
description: Adobe Experience Platform Data Science Workspace consente di pubblicare il modello come servizio addestrato e valutato, consentendo agli utenti della tua organizzazione di valutare i dati senza dover creare i propri modelli.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 4%

---

# Pubblicare un modello come servizio nell’interfaccia utente di Data Science Workspace {#publish-a-model-as-a-service}

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

>[!CONTEXTUALHELP]
>id="platform_intelligentservices_publishmodel"
>title="Pubblicare un modello come servizio"
>abstract=""

Adobe Experience Platform Data Science Workspace consente di pubblicare il modello come servizio addestrato e valutato, consentendo agli utenti della tua organizzazione di valutare i dati senza dover creare i propri modelli.

## Introduzione

Per completare questa esercitazione, devi avere accesso a [!DNL Experience Platform]. Se non si dispone dell&#39;accesso a un&#39;organizzazione in [!DNL Experience Platform], contattare l&#39;amministratore di sistema prima di procedere.

Questo tutorial richiede un modello esistente con un’esecuzione di apprendimento corretta. Se non disponi di un modello pubblicabile, segui l&#39;esercitazione [Addestra e valuta un modello nell&#39;interfaccia utente](./train-evaluate-model-ui.md) prima di continuare.

Se preferisci pubblicare un modello utilizzando le API di apprendimento automatico di Sensei, consulta l&#39;[esercitazione API](./publish-model-service-api.md).

## Publish a Model {#publish-a-model}

In Adobe Experience Platform, seleziona **[!UICONTROL Modelli]** nella colonna di navigazione a sinistra, quindi seleziona la scheda **[!UICONTROL Sfoglia]** per elencare tutti i modelli esistenti. Seleziona il nome del modello da pubblicare come servizio.

![](../images/models-recipes/publish-model/browse_model.png)

Seleziona **[!UICONTROL Publish]** in alto a destra nella pagina di panoramica del modello per avviare un processo di creazione del servizio.

![](../images/models-recipes/publish-model/view_training.png)

Immettere il nome desiderato per il servizio e, se si desidera, fornire una descrizione del servizio. Al termine, selezionare **[!UICONTROL Avanti]**.

![](../images/models-recipes/publish-model/configure_training.png)

Sono elencate tutte le esecuzioni di addestramento riuscite per il modello. Il nuovo Servizio erediterà le configurazioni di formazione e punteggio dall’esecuzione di formazione selezionata.

![](../images/models-recipes/publish-model/select_training_run.png)

Selezionare **[!UICONTROL Fine]** per creare il servizio e reindirizzare alla **[!UICONTROL Raccolta servizi]** per visualizzare tutti i servizi disponibili, incluso il servizio appena creato.

![](../images/models-recipes/publish-model/service_gallery.png)

## Punteggio tramite un servizio {#access-a-service}

In Adobe Experience Platform, seleziona la scheda **[!UICONTROL Servizi]** nella colonna di navigazione a sinistra per accedere alla **[!UICONTROL Raccolta servizi]**. Individuare il servizio che si desidera utilizzare e selezionare **[!UICONTROL Apri]**.

![](../images/models-recipes/publish-model/open_service.png)

Nella pagina di panoramica del servizio, seleziona **[!UICONTROL Punteggio]**.

![](../images/models-recipes/publish-model/score_service.png)

Seleziona un set di dati di input appropriato per l&#39;esecuzione del punteggio, quindi seleziona **[!UICONTROL Successivo]**. Ti viene chiesto di eseguire lo stesso passaggio per il set di dati di punteggio. Dopo aver selezionato il set di dati di input e di output, puoi aggiornare le configurazioni.

![](../images/models-recipes/publish-model/select_datasets.png)

Quando viene creato, un servizio eredita le configurazioni di punteggio predefinite. Puoi rivedere queste configurazioni e regolarle in base alle esigenze facendo doppio clic sui valori. Una volta completate le configurazioni, selezionare **[!UICONTROL Fine]** per iniziare l&#39;esecuzione del punteggio.

![](../images/models-recipes/publish-model/scoring_configs.png)

Nella pagina **Panoramica** del servizio vengono visualizzati i dettagli del nuovo processo di punteggio e il relativo avanzamento. Al termine del processo, l&#39;intestazione **[!UICONTROL Most Recent]** all&#39;interno del contenitore **[!UICONTROL Scoring]** viene aggiornata.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, è stato pubblicato un modello come servizio accessibile e sono stati assegnati dei punteggi ai dati utilizzando il nuovo servizio tramite la [!UICONTROL Galleria servizi]. Continua con l&#39;esercitazione successiva per scoprire come [pianificare l&#39;esecuzione di formazione automatizzata e punteggio in un servizio](./schedule-models-ui.md).
