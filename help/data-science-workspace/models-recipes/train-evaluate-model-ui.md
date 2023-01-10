---
keywords: Experience Platform;formazione e valutazione;Data Science Workspace;argomenti comuni;creare un modello;creare un'esecuzione di formazione
solution: Experience Platform
title: Formazione e valutazione di un modello nell’interfaccia utente di Data Science Workspace
type: Tutorial
description: In Adobe Experience Platform Data Science Workspace, viene creato un modello di apprendimento automatico incorporando una composizione esistente appropriata per l'intento del modello. Il modello viene quindi addestrato e valutato per ottimizzarne l'efficienza operativa e l'efficacia, regolando con precisione i relativi Hyperparameters associati. Le ricette sono riutilizzabili, il che significa che è possibile creare più modelli e personalizzarli per scopi specifici con un'unica ricetta.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 1%

---

# Formazione e valutazione di un modello nell’interfaccia utente di Data Science Workspace

In Adobe Experience Platform Data Science Workspace, viene creato un modello di apprendimento automatico incorporando una composizione esistente appropriata per l&#39;intento del modello. Il modello viene quindi addestrato e valutato per ottimizzarne l&#39;efficienza operativa e l&#39;efficacia, regolando con precisione i relativi Hyperparameters associati. Le ricette sono riutilizzabili, il che significa che è possibile creare più modelli e personalizzarli per scopi specifici con un&#39;unica ricetta.

Questa esercitazione descrive i passaggi necessari per creare, addestrare e valutare un modello.

## Introduzione

Per completare questa esercitazione, devi disporre dell’accesso a [!DNL Experience Platform]. Se non hai accesso a un’organizzazione IMS in [!DNL Experience Platform]Prima di procedere, rivolgiti all’amministratore di sistema.

Questa esercitazione richiede una composizione esistente. Se non hai una Ricetta, segui la [Importare una composizione in pacchetto nell’interfaccia utente](./import-packaged-recipe-ui.md) esercitazione prima di continuare.

## Creare un modello

In Experience Platform, seleziona la **[!UICONTROL Modelli]** nella barra di navigazione a sinistra, quindi seleziona la scheda Sfoglia per visualizzare i modelli esistenti. Seleziona **[!UICONTROL Crea modello]** in alto a destra della pagina per iniziare un processo di creazione del modello.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Sfogliare l&#39;elenco delle ricette esistenti, trovare e selezionare la ricetta da utilizzare per creare il modello e selezionare **[!UICONTROL Successivo]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Seleziona un set di dati di input appropriato e seleziona **[!UICONTROL Successivo]**. Questo imposta il set di dati di formazione di input predefinito per il modello.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Fornisci un nome per il modello e controlla le configurazioni del modello di default. Le configurazioni predefinite sono state applicate durante la creazione della composizione, rivedi e modifica i valori di configurazione facendo doppio clic sui valori.

Per fornire un nuovo set di configurazioni, seleziona **[!UICONTROL Carica nuova configurazione]** e trascinare un file JSON contenente configurazioni del modello nella finestra del browser. Seleziona **[!UICONTROL Fine]** per creare il modello.

>[!NOTE]
>
>Le configurazioni sono univoche e specifiche per la composizione prevista, il che significa che le configurazioni per la ricetta vendite al dettaglio non funzioneranno per la ricetta Recommendations prodotto. Consulta la sezione [riferimento](#reference) per un elenco delle configurazioni Ricetta vendite al dettaglio.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Creare un’esecuzione di formazione

In Experience Platform, seleziona la **[!UICONTROL Modelli]** nella barra di navigazione a sinistra, quindi seleziona la scheda Sfoglia per visualizzare i modelli esistenti. Individuare e selezionare il collegamento ipertestuale collegato al nome del modello che si desidera addestrare.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Vengono elencate tutte le esecuzioni di formazione esistenti con i relativi stati di formazione correnti. Per i modelli creati utilizzando [!DNL Data Science Workspace] interfaccia utente, un’esecuzione di formazione viene generata automaticamente ed eseguita utilizzando le configurazioni predefinite e il set di dati di formazione per l’input.

Crea una nuova esecuzione di formazione selezionando **[!UICONTROL Treno]** in alto a destra della pagina di panoramica Modello .

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Seleziona il set di dati di input di formazione per l’esecuzione della formazione, quindi seleziona **[!UICONTROL Successivo]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

Vengono visualizzate le configurazioni predefinite fornite durante la creazione del modello, modificate e modificate di conseguenza facendo doppio clic sui valori. Seleziona **[!UICONTROL Fine]** per creare ed eseguire l’esecuzione del corso di formazione.

>[!NOTE]
>
>Le configurazioni sono univoche e specifiche per la composizione prevista, il che significa che le configurazioni per la ricetta vendite al dettaglio non funzioneranno per la ricetta Recommendations prodotto. Consulta la sezione [riferimento](#reference) per un elenco delle configurazioni Ricetta vendite al dettaglio.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Valutare il modello

In Experience Platform, seleziona la **[!UICONTROL Modelli]** nella barra di navigazione a sinistra, quindi seleziona la scheda Sfoglia per visualizzare i modelli esistenti. Individuare e selezionare il collegamento ipertestuale collegato al nome del modello da valutare.

![seleziona modello](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Vengono elencate tutte le esecuzioni di formazione esistenti con i relativi stati di formazione correnti. Con più esecuzioni di formazione completate, le metriche di valutazione possono essere confrontate tra diverse esecuzioni di formazione nel grafico di valutazione del modello. Seleziona una metrica di valutazione utilizzando l’elenco a discesa sopra il grafico.

La metrica Media Absolute Percent Error (MAPE) (Errore percentuale assoluto medio) esprime precisione come percentuale dell’errore. Viene utilizzato per identificare l’esperimento con le prestazioni migliori. Più basso è il MAPE, meglio è.

![panoramica dei corsi di formazione](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

La metrica &quot;precisione&quot; descrive la percentuale di istanze rilevanti rispetto al totale *recuperato* Istanze. La precisione può essere vista come la probabilità che un risultato selezionato in modo casuale sia corretto.

![esecuzione di più esecuzioni](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Quando si seleziona un’esecuzione di formazione specifica, vengono descritti i dettagli dell’esecuzione aprendo la pagina di valutazione. Questa operazione può essere eseguita anche prima del completamento dell’esecuzione. Nella pagina di valutazione puoi vedere altre metriche di valutazione, parametri di configurazione e visualizzazioni specifiche dell’esecuzione del corso di formazione.

![registri di anteprima](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

Puoi anche scaricare i registri attività per visualizzare i dettagli dell’esecuzione. I registri sono particolarmente utili per le esecuzioni non riuscite per vedere cosa è andato storto.

![registri attività](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Non è possibile addestrare i parametri ipertestuali e un modello deve essere ottimizzato testando diverse combinazioni di Hyperparameters. Ripeti questo processo di formazione e valutazione del modello fino a quando non avrai raggiunto un modello ottimizzato.

## Passaggi successivi

Questa esercitazione illustra come creare, addestrare e valutare un modello in [!DNL Data Science Workspace]. Una volta arrivati a un modello ottimizzato, puoi utilizzare il modello addestrato per generare informazioni seguendo [Punteggio di un modello nell’interfaccia utente](./score-model-ui.md) esercitazione.

## Riferimenti {#reference}

### Configurazioni ricetta vendite al dettaglio

I parametri ipertestuali determinano il comportamento di formazione del Modello, la modifica di Hyperparameters influenzerà la precisione e la precisione del Modello:

| Iperparametro | Descrizione | Intervallo consigliato |
| --- | --- | --- |
| learning_rate | Il tasso di apprendimento riduce il contributo di ogni albero tramite learning_rate. C&#39;è un compromesso tra learning_rate e n_estimatori. | 0.1 |
| n_estimatori | Numero di fasi di incremento da eseguire. Il miglioramento della sfumatura è abbastanza robusto per l&#39;installazione eccessiva, quindi un numero elevato di solito si traduce in prestazioni migliori. | 100 |
| max_depth | Profondità massima dei singoli stimatori di regressione. La profondità massima limita il numero di nodi nella struttura. Sintonizza questo parametro per ottenere prestazioni migliori; il valore migliore dipende dall’interazione delle variabili di input. | 3 |

I parametri aggiuntivi determinano le proprietà tecniche del modello:

| Chiave parametro | Tipo | Descrizione |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Stringa | Elenco degli attributi dello schema di input separati da virgole. |
| `ACP_DSW_TARGET_FEATURES` | Stringa | Elenco degli attributi dello schema di output separati da virgole. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se le funzioni di input e output sono modificabili |
| `tenantId` | Stringa | Questo ID assicura che le risorse create siano spuntate correttamente e contenute all’interno dell’organizzazione IMS. [Segui i passaggi qui](../../xdm/api/getting-started.md#know-your-tenant_id) per trovare l’ID tenant. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Stringa | Lo schema di input utilizzato per la formazione di un modello. |
| `evaluation.labelColumn` | Stringa | Etichetta colonna per le visualizzazioni di valutazione. |
| `evaluation.metrics` | Stringa | Elenco separato da virgole delle metriche di valutazione da utilizzare per la valutazione di un modello. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Stringa | Lo schema di output utilizzato per il punteggio di un modello. |
