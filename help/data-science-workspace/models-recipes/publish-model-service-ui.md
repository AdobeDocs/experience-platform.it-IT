---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Pubblicare un modello come servizio (interfaccia utente)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4b0f0dda97f044590f55eaf75a220f631f3313ee
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# Pubblicare un modello come servizio (interfaccia utente)

 Adobe Experience Platform Data Science Workspace consente di pubblicare il modello di formazione e valutazione come servizio, consentendo agli utenti all&#39;interno dell&#39;organizzazione IMS di valutare i dati senza la necessità di creare i propri modelli.

## Introduzione

Per completare questa esercitazione, è necessario avere accesso a [!DNL Experience Platform]. Se non disponete dell&#39;accesso a un&#39;organizzazione IMS in [!DNL Experience Platform], rivolgetevi all&#39;amministratore di sistema prima di procedere.

Questa esercitazione richiede un modello esistente con una corretta esecuzione della formazione. Se non si dispone di un modello pubblicabile, seguire il [treno e valutare un modello nell’esercitazione dell’interfaccia utente](./train-evaluate-model-ui.md) prima di continuare.

Se si preferisce pubblicare un modello utilizzando le API Sensei Machine Learning, fare riferimento all&#39;esercitazione [](./publish-model-service-api.md)API.

## Pubblicare un modello {#publish-a-model}

1. In  Adobe Experience Platform, fare clic sul **[!UICONTROL Models]** collegamento situato nella colonna di navigazione a sinistra per elencare tutti i modelli esistenti. Individuate e fate clic sul nome del modello da pubblicare come servizio.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Fare clic **[!UICONTROL Publish]** in alto a destra nella pagina Panoramica modello per avviare un processo di creazione del servizio.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Inserisci il nome desiderato per il Servizio e, facoltativamente, fornisci una descrizione del Servizio, fai clic su **[!UICONTROL Next]** al termine.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Vengono elencate tutte le esecuzioni di formazione riuscite per l&#39;accesso al modello. Il nuovo Servizio erediterà le configurazioni di formazione e punteggio dall’esecuzione di formazione selezionata.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Fare clic **[!UICONTROL Finish]** per creare il Servizio e reindirizzare al servizio per visualizzare **[!UICONTROL Service Gallery]** tutti i Servizi disponibili, incluso il Servizio appena creato.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Punteggio con un servizio {#access-a-service}

1. In  Adobe Experience Platform, fate clic sulla **[!UICONTROL Services]** scheda situata nella colonna di navigazione a sinistra per accedere al *[!UICONTROL Service Gallery]*. Trova il Servizio che desideri utilizzare e fai clic su **[!UICONTROL Score]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Selezionare un set di dati di input appropriato per l&#39;esecuzione del punteggio, quindi fare clic su **[!UICONTROL Next]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Selezionare un set di dati di output appropriato per i risultati del punteggio, quindi fare clic su **[!UICONTROL Next]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. Quando viene creato un servizio, eredita le configurazioni di punteggio predefinite. Per rivedere queste configurazioni e regolarle in base alle esigenze, fai doppio clic sui valori. Una volta completate le configurazioni, fare clic **[!UICONTROL Finish]** per iniziare l&#39;esecuzione del punteggio.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. Nella pagina *Panoramica* del servizio vengono visualizzati i dettagli del nuovo processo di punteggio e del relativo avanzamento. Al termine del processo, il processo di **[!UICONTROL Most Recent]** punteggio verrà aggiornato.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai pubblicato correttamente un modello come servizio accessibile e i dati con punteggio utilizzando il nuovo servizio tramite *[!UICONTROL Service Gallery]*. Seguite l&#39;esercitazione successiva per apprendere come [pianificare l&#39;esecuzione automatica della formazione e del punteggio su un servizio](./schedule-models-ui.md).
