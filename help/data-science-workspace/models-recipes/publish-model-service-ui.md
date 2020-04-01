---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Pubblicare un modello come servizio (interfaccia utente)
topic: Tutorial
translation-type: tm+mt
source-git-commit: af491361c5c3518e9bcc0af41a5aa79022229a2d

---


# Pubblicare un modello come servizio (interfaccia utente)

Adobe Experience Platform Data Science Workspace consente di pubblicare i modelli formati e valutati come un servizio, consentendo agli utenti all&#39;interno dell&#39;organizzazione IMS di valutare i dati senza la necessità di creare i propri modelli.

Questa esercitazione descrive i passaggi necessari per pubblicare un modello come servizio e per segnare i dati con un servizio tramite *Service Gallery*. È suddiviso nelle seguenti sezioni principali:

- [Pubblicare un modello](#publish-a-model)
- [Punteggio con un servizio](#access-a-service)

## Introduzione

Per completare questa esercitazione, è necessario disporre dell&#39;accesso a Experience Platform. Se non disponete dell&#39;accesso a un&#39;organizzazione IMS in Experience Platform, rivolgetevi al vostro amministratore di sistema prima di continuare.

Questa esercitazione richiede un modello esistente con una corretta esecuzione della formazione. Se non si dispone di un modello pubblicabile, seguire il [treno e valutare un modello nell’esercitazione dell’interfaccia utente](./train-evaluate-model-ui.md) prima di continuare.

Se si preferisce pubblicare un modello utilizzando le API Sensei Machine Learning, fare riferimento all&#39;esercitazione [](./publish-model-service-api.md)API.

## Pubblicare un modello

1. In Adobe Experience Platform, fai clic sul collegamento **Modelli** nella colonna di navigazione a sinistra per elencare tutti i modelli esistenti. Individuate e fate clic sul nome del modello da pubblicare come servizio.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
1. Fate clic su **Pubblica** nella parte superiore destra della pagina Panoramica modello per avviare un processo di creazione del servizio.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
1. Inserisci il nome desiderato per il Servizio e, facoltativamente, fornisci una descrizione del Servizio, fai clic su **Avanti** al termine.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
1. Vengono elencate tutte le esecuzioni di formazione riuscite per l&#39;accesso al modello. Il nuovo Servizio erediterà le configurazioni di formazione e punteggio dall’esecuzione di formazione selezionata.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
1. Fare clic su **Fine** per creare il Servizio e reindirizzare alla Raccolta **** servizi per visualizzare tutti i Servizi disponibili, incluso il Servizio appena creato.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Punteggio con un servizio

1. In Adobe Experience Platform, fai clic sulla scheda **Servizi** presente nella colonna di navigazione a sinistra per accedere a *Service Gallery*. Individuate il servizio che desiderate utilizzare e fate clic su **Valutazione**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
1. Selezionare un set di dati di input appropriato per l&#39;esecuzione del punteggio, quindi fare clic su **Avanti**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
1. Selezionare un set di dati di output appropriato per i risultati del punteggio, quindi fare clic su **Avanti**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
1. Quando viene creato un servizio, eredita le configurazioni di punteggio predefinite. Per rivedere queste configurazioni e regolarle in base alle esigenze, fai doppio clic sui valori. Una volta soddisfatte le configurazioni, fare clic su **Fine** per iniziare l&#39;esecuzione del punteggio.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
1. Nella pagina *Panoramica* del servizio vengono visualizzati i dettagli del nuovo processo di punteggio e del relativo avanzamento. Al termine del processo, il processo di punteggio **più recente** verrà aggiornato.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Passaggi successivi

Seguendo questa esercitazione, hai pubblicato correttamente un modello come servizio accessibile e i dati con punteggio utilizzando il nuovo servizio tramite *Service Gallery*. Seguite l&#39;esercitazione successiva per apprendere come [pianificare l&#39;esecuzione automatica della formazione e del punteggio su un servizio](./schedule-models-ui.md).
