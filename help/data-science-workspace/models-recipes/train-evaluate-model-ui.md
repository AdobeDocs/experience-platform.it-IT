---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: Formazione e valutazione di un modello (interfaccia utente)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---


# Formazione e valutazione di un modello (interfaccia utente)

In  Adobe Experience Platform Data Science Workspace, un modello di apprendimento automatico viene creato incorporando una Ricetta esistente adatta all&#39;intento del modello. Il modello viene quindi addestrato e valutato per ottimizzare l&#39;efficienza operativa e l&#39;efficacia, affinando i relativi Hyperparameters associati. Le ricette sono riutilizzabili, il che significa che più modelli possono essere creati e personalizzati a scopi specifici con un&#39;unica ricetta.

Questa esercitazione descrive i passaggi necessari per creare, formare e valutare un modello.

## Introduzione

Per completare questa esercitazione, è necessario avere accesso a [!DNL Experience Platform]. Se non disponete dell&#39;accesso a un&#39;organizzazione IMS in [!DNL Experience Platform], rivolgetevi all&#39;amministratore di sistema prima di procedere.

Questa esercitazione richiede una composizione esistente. Se non disponete di una ricetta, seguite l&#39;esercitazione [Importa una ricetta in un pacchetto nell&#39;interfaccia utente](./import-packaged-recipe-ui.md) prima di continuare.

## Creare un modello

1. In  Adobe Experience Platform, fare clic sul **[!UICONTROL Models]** collegamento situato nella colonna di navigazione a sinistra per elencare tutti i modelli esistenti. Fare clic **[!UICONTROL Create Model]** vicino all&#39;angolo superiore destro della pagina per avviare il processo di creazione di un modello.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Sfogliate l&#39;elenco delle ricette esistenti, individuate e selezionate la Ricetta da utilizzare per creare il modello e fate clic **[!UICONTROL Next]**.
   ![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

3. Selezionare un set di dati di input appropriato e fare clic su **[!UICONTROL Next]**. Questo imposta il dataset di formazione di input predefinito per il modello.
   ![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

4. Specificare un nome per il modello e rivedere le configurazioni del modello predefinito. Le configurazioni predefinite sono state applicate durante la creazione di ricette, la revisione e la modifica dei valori di configurazione facendo doppio clic sui valori. Per fornire un nuovo set di configurazioni, fai clic **[!UICONTROL Upload New Config]** e trascina nella finestra del browser un file JSON contenente le configurazioni del modello. Fare clic **[!UICONTROL Finish]** per creare il modello.
   >[!NOTE]Le configurazioni sono univoche e specifiche per la Ricetta prevista, il che significa che le configurazioni per la Ricetta vendite al dettaglio non funzioneranno per la Ricetta raccomandazioni prodotto. Consulta la sezione di [riferimento](#reference) per un elenco delle configurazioni di Ricetta vendite al dettaglio.

   ![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Creazione di un&#39;esecuzione di formazione

1. In  Adobe Experience Platform, fare clic sul **[!UICONTROL Models]** collegamento situato nella colonna di navigazione a sinistra per elencare tutti i modelli esistenti. Trovare e fare clic sul nome del modello da addestrare.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Vengono elencate tutte le esecuzioni di formazione esistenti con i rispettivi stati di formazione correnti. Per i modelli creati utilizzando l&#39;interfaccia [!DNL Data Science Workspace] utente, un&#39;esecuzione di formazione viene generata automaticamente e eseguita utilizzando le configurazioni predefinite e il dataset di formazione di input.
   ![](../images/models-recipes/train-evaluate-ui/model_overview.png)

3. Per creare una nuova esecuzione della formazione, fai clic **[!UICONTROL Train]** in alto a destra nella pagina Panoramica del modello.
   ![](../images/models-recipes/train-evaluate-ui/training_input.png)

4. Selezionate il set di dati di input della formazione per l’esecuzione della formazione e fate clic su **[!UICONTROL Next]**.
   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

5. Le configurazioni predefinite fornite durante la creazione del modello vengono visualizzate, modificate e modificate di conseguenza facendo doppio clic sui valori. Fate clic **[!UICONTROL Finish]** per creare ed eseguire l&#39;esecuzione della formazione.
   >[!NOTE]Le configurazioni sono univoche e specifiche per la Ricetta prevista, il che significa che le configurazioni per la Ricetta vendite al dettaglio non funzioneranno per la Ricetta raccomandazioni prodotto. Consulta la sezione di [riferimento](#reference) per un elenco delle configurazioni di Ricetta vendite al dettaglio.

   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

## Valutazione del modello

1. In  Adobe Experience Platform, fare clic sul **[!UICONTROL Models]** collegamento situato nella colonna di navigazione a sinistra per elencare tutti i modelli esistenti. Individuare e fare clic sul nome del modello da valutare.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Vengono elencate tutte le esecuzioni di formazione esistenti con i rispettivi stati di formazione correnti. Con più esecuzioni di formazione completate, le metriche di valutazione possono essere confrontate tra diverse esecuzioni di formazione nel grafico di valutazione del modello, selezionate una metrica di valutazione utilizzando l&#39;elenco a discesa sopra il grafico.

   La metrica Errore percentuale assoluta medio (MAPE, Mean Absolute Percent Error) esprime la precisione come percentuale dell&#39;errore. Questo viene utilizzato per identificare l&#39;esperimento con le migliori prestazioni. Più bassa è la MAPE, meglio è.

   ![](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

   La metrica &quot;Precisione&quot; descrive la percentuale di istanze rilevanti rispetto al totale delle istanze *recuperate* . La precisione può essere vista come la probabilità che un risultato selezionato in modo casuale sia corretto.
   ![](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

   Fate clic su una specifica esecuzione di formazione per visualizzare i dettagli di tale esecuzione. Questa operazione può essere eseguita anche prima del completamento dell&#39;esecuzione. Nella pagina dei dettagli di esecuzione, puoi vedere altre metriche di valutazione, parametri di configurazione e visualizzazioni specifiche per l’esecuzione della formazione. Potete anche scaricare i registri attività per visualizzare i dettagli dell&#39;esecuzione. I registri sono particolarmente utili per le esecuzioni non riuscite per vedere cosa è andato storto.
   ![](../images/models-recipes/train-evaluate-ui/activity_logs.png)

3. I parametri ipertestuali non possono essere addestrati e un modello deve essere ottimizzato verificando diverse combinazioni di Hyperparameters. Ripetete questo processo di formazione e valutazione del modello fino a quando non arriverete a un modello ottimizzato.

## Passaggi successivi

Questa esercitazione illustra come creare, addestrare e valutare un modello in [!DNL Data Science Workspace]. Una volta raggiunto un modello ottimizzato, è possibile utilizzare il modello preparato per generare informazioni seguendo l&#39;esercitazione [Punteggio a Model (Punteggio a Model) nell&#39;esercitazione dell&#39;interfaccia utente](./score-model-ui.md) .

## Riferimenti {#reference}

### Configurazioni Ricetta vendite al dettaglio

I parametri ipertestuali determinano il comportamento di formazione del Modello, la modifica dei Parametri ipertestuali influisce sulla precisione e precisione del Modello:

| Hyperparameter | Descrizione | Intervallo consigliato |
--- | --- | ---
| learning_rate | Il tasso di apprendimento riduce il contributo di ogni albero mediante learning_rate. Esiste un compromesso tra learning_rate e n_estimatori. | 0.1 | [2 - 10] / numero di stimatori |
| n_estimatori | Numero di fasi di incremento da eseguire. L&#39;incremento della sfumatura è abbastanza robusto per l&#39;installazione eccessiva, quindi un numero elevato di volte si traduce in prestazioni migliori. | 100 | 100 - 1000 |
| max_deep | Profondità massima dei singoli stimatori di regressione. La profondità massima limita il numero di nodi nella struttura. Ottimizzate questo parametro per ottenere prestazioni ottimali; il valore migliore dipende dall&#39;interazione delle variabili di input. | 3 | 4 - 10 |

I parametri aggiuntivi determinano le proprietà tecniche del modello:

| Chiave parametro | Tipo | Descrizione |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Stringa | Elenco degli attributi dello schema di input separati da virgola. |
| `ACP_DSW_TARGET_FEATURES` | Stringa | Elenco degli attributi dello schema di output separati da virgola. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se le funzioni di input e output sono modificabili |
| `tenantId` | Stringa | Questo ID garantisce che le risorse create siano inserite correttamente nell’organizzazione IMS. [Segui i passaggi qui](../../xdm/api/getting-started.md#know-your-tenant_id) per trovare l&#39;ID tenant. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Stringa | Lo schema di input utilizzato per la formazione di un modello. |
| `evaluation.labelColumn` | Stringa | Etichetta colonna per le visualizzazioni di valutazione. |
| `evaluation.metrics` | Stringa | Elenco separato da virgole delle metriche di valutazione da utilizzare per la valutazione di un modello. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Stringa | Lo schema di output utilizzato per il punteggio di un modello. |