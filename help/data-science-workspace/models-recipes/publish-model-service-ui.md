---
keywords: Experience Platform;pubblicare un modello;Data Science Workspace;argomenti comuni;valutare un servizio
solution: Experience Platform
title: Pubblicare un modello come servizio nell’interfaccia utente di Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace consente di pubblicare il modello addestrato e valutato come servizio, consentendo agli utenti all’interno della tua organizzazione IMS di valutare i dati senza la necessità di creare i propri Modelli.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Pubblicare un modello come servizio nell’interfaccia utente di Data Science Workspace

Adobe Experience Platform Data Science Workspace consente di pubblicare il modello addestrato e valutato come servizio, consentendo agli utenti all’interno della tua organizzazione IMS di valutare i dati senza la necessità di creare i propri Modelli.

## Introduzione

Per completare questa esercitazione, devi disporre dell&#39;accesso a [!DNL Experience Platform]. Se non hai accesso a un&#39;organizzazione IMS in [!DNL Experience Platform], rivolgiti all&#39;amministratore di sistema prima di procedere.

Questa esercitazione richiede un modello esistente con una corretta esecuzione della formazione. Se non disponi di un modello pubblicabile, segui il [Treno e valuta un modello nell&#39;esercitazione UI](./train-evaluate-model-ui.md) prima di continuare.

Se preferisci pubblicare un modello utilizzando le API di apprendimento automatico Sensei, fai riferimento al tutorial [API](./publish-model-service-api.md).

## Pubblicare un modello {#publish-a-model}

In Adobe Experience Platform, seleziona **[!UICONTROL Models]** nella colonna di navigazione a sinistra, quindi seleziona la scheda **[!UICONTROL Browse]** per elencare tutti i modelli esistenti. Selezionare il nome del modello da pubblicare come servizio.

![](../images/models-recipes/publish-model/browse_model.png)

Seleziona **[!UICONTROL Publish]** in alto a destra della pagina Panoramica modello per avviare un processo di creazione del servizio.

![](../images/models-recipes/publish-model/view_training.png)

Inserisci un nome desiderato per il Servizio e facoltativamente fornisci una descrizione del Servizio, seleziona **[!UICONTROL Next]** al termine.

![](../images/models-recipes/publish-model/configure_training.png)

Vengono elencate tutte le esecuzioni di formazione riuscite per il modello . Il nuovo servizio erediterà le configurazioni di formazione e valutazione dall’esecuzione di formazione selezionata.

![](../images/models-recipes/publish-model/select_training_run.png)

Seleziona **[!UICONTROL Finish]** per creare il servizio ed effettuare il reindirizzamento a **[!UICONTROL Service Gallery]** per mostrare tutti i servizi disponibili, incluso il servizio appena creato.

![](../images/models-recipes/publish-model/service_gallery.png)

## Punteggio con un servizio {#access-a-service}

In Adobe Experience Platform, seleziona la scheda **[!UICONTROL Services]** situata nella colonna di navigazione a sinistra per accedere a **[!UICONTROL Service Gallery]**. Trova il servizio che desideri utilizzare e seleziona **[!UICONTROL Open]**.

![](../images/models-recipes/publish-model/open_service.png)

Nella pagina della panoramica del servizio, seleziona **[!UICONTROL Score]**.

![](../images/models-recipes/publish-model/score_service.png)

Seleziona un set di dati di input appropriato per l’esecuzione del punteggio, quindi seleziona **[!UICONTROL Next]**. Viene richiesto di eseguire lo stesso passaggio per il set di dati di punteggio. Dopo aver selezionato il set di dati di input e output, puoi aggiornare le configurazioni.

![](../images/models-recipes/publish-model/select_datasets.png)

Quando un servizio viene creato, eredita le configurazioni di punteggio predefinite. Puoi rivedere queste configurazioni e regolarle in base alle esigenze facendo doppio clic sui valori. Una volta completate le configurazioni, selezionare **[!UICONTROL Finish]** per iniziare l’esecuzione del punteggio.

![](../images/models-recipes/publish-model/scoring_configs.png)

Nella pagina **Panoramica** del servizio vengono visualizzati i dettagli del nuovo processo di valutazione e del relativo avanzamento. Al termine del processo, l’intestazione **[!UICONTROL Most Recent]** all’interno del contenitore **[!UICONTROL Scoring]** viene aggiornata.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai pubblicato correttamente un modello come servizio accessibile e hai effettuato il punteggio dei dati utilizzando il nuovo servizio tramite [!UICONTROL Service Gallery]. Continua con l&#39;esercitazione successiva per scoprire come [pianificare l&#39;esecuzione automatica dei corsi di formazione e valutazione su un servizio](./schedule-models-ui.md).
