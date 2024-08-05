---
keywords: Experience Platform; formare e valutare; Data Science Area di lavoro; argomenti popolari; creare un modello; Creare un'esecuzione training
solution: Experience Platform
title: Eseguire il training e la valutazione di un modello in Data Science Area di lavoro interfaccia
type: Tutorial
description: In Adobe Experience Platform Data Science Area di lavoro viene creato un modello di Machine Learning incorporando una ricetta esistente appropriata per l'intento del modello. Il modello viene quindi addestrato e valutato per ottimizzarne l'efficienza operativa e l'efficacia mettendo a punto gli iperparametri associati. Le ricette sono riutilizzabili, il che significa che più modelli possono essere creati e personalizzati per scopi specifici con una singola ricetta.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# Eseguire il training e la valutazione di un modello in Data Science Area di lavoro interfaccia

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

In Adobe Experience Platform Data Science Area di lavoro viene creato un modello di Machine Learning incorporando una ricetta esistente appropriata per l&#39;intento del modello. Il modello viene quindi addestrato e valutato per ottimizzarne l&#39;efficienza operativa e l&#39;efficacia mettendo a punto gli iperparametri associati. Le ricette sono riutilizzabili, il che significa che più modelli possono essere creati e personalizzati per scopi specifici con una singola ricetta.

In questo esercitazione vengono illustrati i passaggi per creare, addestrare e valutare un modello.

## Introduzione

Per completare questa esercitazione, è necessario disporre di accesso a [!DNL Experience Platform]. Se non si dispone dell&#39;accesso a un&#39;organizzazione in [!DNL Experience Platform], contattare l&#39;amministratore di sistema prima di procedere.

Questo esercitazione richiede una ricetta esistente. Se non hai una ricetta, seguire il [Importa una ricetta confezionata nella interfaccia](./import-packaged-recipe-ui.md) esercitazione prima di continuare.

## Crea un modello

In Experience Platform, seleziona la **[!UICONTROL scheda Modelli]** situata nella navigazione sinistra, quindi seleziona l&#39;scheda Sfoglia per visualizzare i modelli esistenti. Seleziona **[!UICONTROL Crea modello]** in alto a destra della pagina per iniziare un processo di creazione modello.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Sfoglia l&#39;elenco delle ricette esistenti, individua e seleziona la ricetta da utilizzare per creare il modello e seleziona **[!UICONTROL Successivo]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Seleziona un set di dati di input appropriato e seleziona **[!UICONTROL Avanti]**. In questo modo verrà impostato il set di dati di addestramento di input predefinito per il modello.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Fornite un nome per il modello ed esaminate le configurazioni del modello di default. Le configurazioni di default venivano applicate durante la creazione della ricetta, esaminando e modificando i valori di configurazione facendo doppio clic sui valori.

Per fornire un nuovo set di configurazioni, seleziona **[!UICONTROL Carica nuova configurazione]** e trascina un file JSON contenente le configurazioni del modello nella finestra del browser. Selezionare **[!UICONTROL Fine]** per creare il modello.

>[!NOTE]
>
>Le configurazioni sono uniche e specifiche per la loro ricetta prevista, questo significa che le configurazioni per la ricetta di vendita al dettaglio non funzioneranno per il prodotto Raccomandazioni la ricetta. Vedere la [sezione di riferimento](#reference) per un elenco delle configurazioni delle ricette di vendita al dettaglio.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Crea un&#39;esecuzione training

In Experience Platform, seleziona la **[!UICONTROL scheda Modelli]** situata nella navigazione sinistra, quindi seleziona l&#39;scheda Sfoglia per visualizzare i modelli esistenti. Trova e seleziona il collegamento ipertestuale allegato al nome del modello che desideri addestrare.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Vengono elencate tutte le esecuzioni di training esistenti con stato training corrente. Per i modelli creati utilizzando l&#39;interfaccia [!DNL Data Science Workspace] utente, viene generata ed eseguita automaticamente una training esecuzione utilizzando le configurazioni predefinite e l&#39;input training set di dati.

Crea una nuova training selezionando **[!UICONTROL Treno]** in alto a destra nella pagina di panoramica del modello.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Seleziona il set di dati di input training per l&#39;esecuzione training, quindi seleziona **[!UICONTROL Successivo]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

Vengono mostrate le configurazioni predefinite fornite durante la creazione del modello, modificarle e modificarle di conseguenza facendo doppio clic sui valori. Selezionare **[!UICONTROL Fine]** per creare ed eseguire la training esecuzione.

>[!NOTE]
>
>Le configurazioni sono uniche e specifiche per la loro ricetta prevista, questo significa che le configurazioni per la ricetta di vendita al dettaglio non funzioneranno per il prodotto Raccomandazioni la ricetta. Vedere la [sezione di riferimento](#reference) per un elenco delle configurazioni delle ricette di vendita al dettaglio.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Valutare il modello

Ad Experience Platform, seleziona la scheda **[!UICONTROL Modelli]** nell&#39;area di navigazione a sinistra, quindi seleziona la scheda Sfoglia per visualizzare i modelli esistenti. Trova e seleziona il collegamento ipertestuale associato al nome del Modello che desideri valutare.

![Seleziona modello](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Vengono elencate tutte le esecuzioni di training esistenti con stato training corrente. Con più esecuzioni di training completate, le metriche di valutazione possono essere confrontate tra diverse esecuzioni di training nella tabella di valutazione del modello. Seleziona una metrica di valutazione utilizzando l&#39;elenco a discesa sopra il grafico.

La metrica MAPE (Mean Absolute Percent Errore) esprime la precisione come percentuale dell&#39;errore. Viene utilizzato per identificare l’esperimento con le prestazioni migliori. Più basso è il MAPE, meglio è.

![panoramica delle esecuzioni di addestramento](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

La metrica &quot;Precisione&quot; descrive la percentuale di istanze rilevanti rispetto al totale di *istanze recuperate*. La precisione può essere vista come la probabilità che un risultato selezionato casualmente sia corretto.

![esecuzione di più esecuzioni](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Se si seleziona un&#39;esecuzione di training specifica, vengono forniti i dettagli di tale esecuzione aprendo la pagina di valutazione. Questa operazione può essere eseguita lineare prima che l&#39;esecuzione sia stata completata. Nella pagina di valutazione è possibile visualizzare altre metriche di valutazione, parametri di configurazione e visualizzazioni specifiche per l&#39;esecuzione training.

![Registri di anteprima](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

Puoi anche scaricare i registri delle attività per visualizzare i dettagli dell&#39;esecuzione. I registri sono particolarmente utili per le esecuzioni non riuscite per vedere cosa è andato storto.

![registri delle attività](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Gli iperparametri non possono essere addestrati e un modello deve essere ottimizzato testando diverse combinazioni di iperparametri. Ripetete questa training del modello e il processo di valutazione fino a quando non avrete ottenuto un modello ottimizzato.

## Passaggi successivi

Questo esercitazione ti ha guidato attraverso la creazione, l&#39;training e la valutazione di un modello in [!DNL Data Science Workspace]. Una volta ottenuto un modello ottimizzato, è possibile utilizzare il modello sottoposto a training per generare informazioni dettagliate seguendo il punteggio di [un modello nella esercitazione interfaccia](./score-model-ui.md) .

## Riferimenti {#reference}

### Configurazioni ricetta vendita al dettaglio

Gli iperparametri determinano il comportamento di addestramento del modello, la modifica degli iperparametri influisce sulla precisione e sull&#39;accuratezza del modello:

| Hyperparameter | Descrizione | Intervallo consigliato |
| --- | --- | --- |
| tasso_di_apprendimento | Il tasso di apprendimento riduce il contributo di ogni albero di learning_rate. Esiste un compromesso tra learning_rate e n_estimators. | 0,1 |
| n_estimators | Il numero di fasi di potenziamento da eseguire. L&#39;aumento del gradiente è abbastanza robusto o over-fitting, quindi un numero elevato di solito si traduce in prestazioni migliori. | 100 |
| max_depth | Profondità massima dei singoli stimatori di regressione. La profondità massima limita il numero di nodi nell&#39;albero. Regola questo parametro per ottenere le migliori prestazioni; Il valore migliore dipende dall&#39;interazione delle variabili di input. | 3 |

Ulteriori parametri determinano le proprietà tecniche del modello:

| Chiave parametro | Tipo | Descrizione |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Stringa | Elenco di attributi dello schema di input separati da virgola. |
| `ACP_DSW_TARGET_FEATURES` | Stringa | Elenco di attributi dello schema di output separati da virgole. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se le funzioni di input e output sono modificabili |
| `tenantId` | Stringa | Questo ID garantisce che le risorse create abbiano uno spazio dei nomi corretto e siano contenute all’interno dell’organizzazione. [Seguire i passaggi descritti di seguito](../../xdm/api/getting-started.md#know-your-tenant_id) per trovare l&#39;ID tenant. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Stringa | Lo schema di input utilizzato per training un modello. |
| `evaluation.labelColumn` | Stringa | Etichetta di colonna per le visualizzazioni di valutazione. |
| `evaluation.metrics` | Stringa | Elenco separato da virgole delle metriche di valutazione da utilizzare per la valutazione di un modello. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Stringa | Lo schema di output utilizzato per assegnare un punteggio a un Model. |
