---
keywords: Experience Platform; importare ricetta confezionata; Data Science Area di lavoro; argomenti popolari; Ricette; Ui; Crea motore
solution: Experience Platform
title: Importa una ricetta confezionata nel Data Science Area di lavoro interfaccia
type: Tutorial
description: Questo tutorial fornisce informazioni su come configurare e importare una composizione in pacchetti utilizzando l’esempio di vendita al dettaglio fornito. Alla fine di questo esercitazione, sarai pronto per creare, addestrare e valutare un modello in Adobe Experience Platform Data Science Area di lavoro.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 0%

---

# Importare una composizione in pacchetti nell’interfaccia utente di Data Science Workspace

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

In questo esercitazione vengono fornite informazione approfondita su come configurare e importare una ricetta confezionata utilizzando l&#39;esempio di vendita al dettaglio fornito. Al termine di questo esercitazione, sarete pronti per creare, addestrare e valutare un modello in Adobe Experience Platform [!DNL Data Science Workspace].

## Prerequisiti

Questo esercitazione richiede una ricetta confezionata sotto forma di immagine Docker URL. Per ulteriori informazioni, consulta l&#39;esercitazione su come impacchettare [i file sorgente in una ricetta](./package-source-files-recipe.md) .

## interfaccia workflow

L&#39;importazione di una ricetta confezionata in [!DNL Data Science Workspace] richiede configurazioni specifiche della ricetta, compilate in un unico file JSON (Object Notation) JavaScript, questa raccolta di configurazioni di ricette viene definita file di configurazione. Una ricetta confezionata con un particolare insieme di configurazioni viene definita ricetta istanza. Una ricetta può essere utilizzata per creare molte istanze di ricette in [!DNL Data Science Workspace].

Il workflow per l&#39;importazione di una ricetta di pacchetto consiste nei seguenti passaggi:
- [Configura una ricetta](#configure)
- [Importa ricetta basata su Docker - Python](#python)
- [Importa ricetta basata su Docker - R](#r)
- [Importa ricetta basata su Docker - PySpark](#pyspark)
- [Importa ricetta basata su Docker - Scala](#scala)

### Configurare una ricetta {#configure}

Ogni istanza di ricetta in [!DNL Data Science Workspace] è accompagnata da un set di configurazioni che adattano l&#39;istanza di ricetta a un caso d&#39;uso particolare. I file di configurazione definiscono i comportamenti predefiniti di apprendimento e punteggio di un modello creato utilizzando questa istanza di ricetta.

>[!NOTE]
>
>I file di configurazione sono specifici per ricetta e caso.

Di seguito è riportato un file di configurazione di esempio che mostra i comportamenti predefiniti di formazione e punteggio per la ricetta di vendita al dettaglio.

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| Chiave parametro | Tipo | Descrizione |
| ----- | ----- | ----- |
| `learning_rate` | Numero | Scalare per la moltiplicazione del gradiente. |
| `n_estimators` | Numero | Numero di alberi nella foresta per Classificatore Foresta casuale. |
| `max_depth` | Numero | Profondità massima di un albero nel classificatore Foresta casuale. |
| `ACP_DSW_INPUT_FEATURES` | Stringa | Elenco di attributi dello schema di input separati da virgole. |
| `ACP_DSW_TARGET_FEATURES` | Stringa | Elenco di attributi dello schema di output separati da virgola. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se le funzioni di input e output sono modificabili |
| `tenantId` | Stringa | Questo ID garantisce che le risorse create abbiano uno spazio dei nomi corretto e siano contenute all’interno dell’organizzazione. [Segui questi passaggi](../../xdm/api/getting-started.md#know-your-tenant_id) per trovare il tuo ID tenant. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Stringa | Schema di input utilizzato per l’apprendimento di un modello. Lasciare vuoto quando si importa in interfaccia, sostituirlo con training SchemaID quando si esegue l&#39;importazione tramite API. |
| `evaluation.labelColumn` | Stringa | Etichetta di colonna per le visualizzazioni di valutazione. |
| `evaluation.metrics` | Stringa | Elenco separato da virgole delle metriche di valutazione da utilizzare per la valutazione di un modello. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Stringa | Schema di output utilizzato per il punteggio di un modello. Lascia vuoto questo campo durante l’importazione nell’interfaccia utente, sostituisci con SchemaID con punteggio durante l’importazione tramite API. |

Ai fini di questa esercitazione, è possibile lasciare i file di configurazione predefiniti per la ricetta di vendita al dettaglio nel riferimento [!DNL Data Science Workspace] nel modo in cui sono.

### Importa ricetta basata su Docker - [!DNL Python] {#python}

Iniziare navigando e selezionando **[!UICONTROL Flussi di lavoro]** che si trovano in alto a sinistra nell&#39;interfaccia utente [!DNL Platform]. Quindi, seleziona **Importa ricetta** e seleziona **[!UICONTROL Avvia]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configura** per il flusso di lavoro **Importa ricetta**. Inserisci un nome e una descrizione per la ricetta, quindi seleziona **[!UICONTROL Successivo]** nell&#39;angolo in alto a destra.

![configura flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nell&#39;esercitazione di [Creazione di pacchetti di file di origine in una ricetta](./package-source-files-recipe.md), è stato fornito un URL Docker al termine della creazione della ricetta di vendita al dettaglio utilizzando i file di origine Python.

Una volta nella pagina **Seleziona origine**, incolla l&#39;URL Docker corrispondente alla composizione inserita creata utilizzando [!DNL Python] file di origine nel campo **[!UICONTROL URL Source]**. Quindi, importare il file di configurazione fornito trascinandolo o utilizzare il file system **Browser**. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Selezionare **[!UICONTROL Python]** nel menu a discesa **Runtime** e **[!UICONTROL Classification]** nel menu a discesa **Type**. Una volta compilato tutto, seleziona **[!UICONTROL Successivo]** nell&#39;angolo in alto a destra per procedere a Gestisci **schemi**.

>[!NOTE]
>
> Il tipo supporta **[!UICONTROL la classificazione]** e **[!UICONTROL la regressione]**. Se il modello non rientra in uno di questi tipi, selezionare **[!UICONTROL Personalizzato]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Successivo, selezionare gli schemi di input e output delle vendite al dettaglio nella sezione **Gestisci schemi**, sono stati creati utilizzando lo script di bootstrap fornito nella [esercitazione Crea schema e set di](../models-recipes/create-retails-sales-dataset.md) dati per le vendite al dettaglio.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Nella sezione **Gestione delle funzionalità**, seleziona l&#39;identificazione del tenant nel visualizzatore di schema per espandere lo schema di input Retail Sales. Selezionare le funzionalità di input e output evidenziando la funzionalità desiderata e selezionando **[!UICONTROL Funzionalità di input]** o **[!UICONTROL Funzionalità di destinazione]** nella finestra **[!UICONTROL Proprietà campo]** a destra. Ai fini di questa esercitazione, imposta **[!UICONTROL weeklySales]** come **[!UICONTROL funzionalità di destinazione]** e tutto il resto come **[!UICONTROL funzionalità di input]**. Seleziona **[!UICONTROL Successivo]** per rivedere la nuova ricetta configurata.

Rivedi la ricetta, aggiungi, modifica o rimuovi le configurazioni in base alle esigenze. Selezionare **[!UICONTROL Fine]** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Procedi ai [passaggi](#next-steps) successivi per scoprire come creare un modello utilizzando [!DNL Data Science Workspace] la ricetta di vendita al dettaglio appena creata.

### Importa Ricetta basata su Docker - R {#r}

Inizia navigando e selezionando **[!UICONTROL Flussi di]** lavoro in alto a sinistra nel [!DNL Platform] interfaccia. Successivo, seleziona **Importa ricetta** e seleziona **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la **pagina Configura** per la **workflow ricetta Importa** . Inserisci un nome e una descrizione per la ricetta, quindi seleziona **[!UICONTROL Successivo]** nell&#39;angolo in alto a destra.

![configurare workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nei file di origine del [pacchetto in un esercitazione ricetta](./package-source-files-recipe.md) è stato fornito un URL Docker al termine della creazione della ricetta di vendita al dettaglio utilizzando i file di origine R.

Nella pagina Seleziona **origine è necessario incollare il** URL Docker corrispondente alla ricetta confezionata creata utilizzando i **[!UICONTROL file di origine R nel campo Origine URL]**. Successivo, importare il file di configurazione fornito trascinandolo oppure utilizzare il browser del file system ****. Il file di configurazione fornito è disponibile in `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Selezionare **[!UICONTROL R nell&#39;elenco** a discesa Runtime **e**[!UICONTROL  Classificazione nell&#39;elenco a **discesa Tipo]****.]** Una volta compilato tutto, seleziona **[!UICONTROL Avanti]** nell&#39;angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> *Tipo* supporta **[!UICONTROL Classificazione]** e **[!UICONTROL Regressione]**. Se il modello non rientra in uno di questi tipi, seleziona **[!UICONTROL Personalizzato]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Quindi, seleziona gli schemi di input e output per la vendita al dettaglio nella sezione **Gestisci schemi**. Sono stati creati utilizzando lo script di avvio fornito nell&#39;esercitazione [crea lo schema e il set di dati per la vendita al dettaglio](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Nella sezione *Gestione delle funzionalità*, seleziona l&#39;identificazione del tenant nel visualizzatore di schema per espandere lo schema di input Retail Sales. Selezionare le funzionalità di input e output evidenziando la funzionalità desiderata e selezionando **[!UICONTROL Funzionalità di input]** o **[!UICONTROL Funzionalità di destinazione]** nella finestra **[!UICONTROL Proprietà campo]** a destra. Ai fini di questa esercitazione, imposta **[!UICONTROL weeklySales]** come **[!UICONTROL funzionalità di destinazione]** e tutto il resto come **[!UICONTROL funzionalità di input]**. Seleziona **[!UICONTROL Successivo]** per rivedere la nuova ricetta configurata.

Rivedi la ricetta, aggiungi, modifica o rimuovi le configurazioni come necessario. Seleziona **Fine** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Procedi ai [passaggi successivi](#next-steps) per scoprire come creare un modello in [!DNL Data Science Workspace] utilizzando la ricetta di vendita al dettaglio appena creata.

### Importa ricetta basata su Docker - PySpark {#pyspark}

Iniziare navigando e selezionando **[!UICONTROL Flussi di lavoro]** che si trovano in alto a sinistra nell&#39;interfaccia utente [!DNL Platform]. Quindi, seleziona **Importa ricetta** e seleziona **[!UICONTROL Avvia]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configura** per il flusso di lavoro **Importa ricetta**. Inserisci un nome e una descrizione per la ricetta, quindi seleziona **[!UICONTROL Successivo]** nell&#39;angolo in alto a destra per procedere.

![configura flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nell&#39;esercitazione [Creare pacchetti di file di origine in una ricetta](./package-source-files-recipe.md) è stato fornito un URL Docker al termine della creazione della ricetta di vendita al dettaglio utilizzando i file di origine PySpark.

Una volta nella pagina **Seleziona origine**, incolla l&#39;URL Docker corrispondente alla composizione inserita creata utilizzando i file di origine PySpark nel campo **[!UICONTROL URL Source]**. Quindi, importare il file di configurazione fornito trascinandolo o utilizzare il file system **Browser**. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Seleziona **[!UICONTROL PySpark]** nel menu a discesa **Runtime**. Una volta selezionato il runtime PySpark, l&#39;artefatto predefinito viene automaticamente popolato in **[!UICONTROL Docker]**. Quindi, seleziona **[!UICONTROL Classificazione]** nel menu a discesa **Tipo**. Una volta compilato tutto, seleziona **[!UICONTROL Avanti]** nell&#39;angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> *Tipo* supporta **[!UICONTROL Classificazione]** e **[!UICONTROL Regressione]**. Se il modello non rientra in uno di questi tipi, seleziona **[!UICONTROL Personalizzato]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Successivo, selezionare gli schemi di input e output delle vendite al dettaglio utilizzando la **selettore Gestisci schemi** , gli schemi sono stati creati utilizzando lo script di bootstrap fornito nella [esercitazione Crea schema e set di dati](../models-recipes/create-retails-sales-dataset.md) delle vendite al dettaglio.

![gestire schemi](../images/models-recipes/import-package-ui/manage-schemas.png)

Nella sezione **Gestione delle funzionalità**, seleziona l&#39;identificazione del tenant nel visualizzatore di schema per espandere lo schema di input Retail Sales. Selezionare le funzionalità di input e output evidenziando la funzionalità desiderata e selezionando **[!UICONTROL Funzionalità di input]** o **[!UICONTROL Funzionalità di destinazione]** nella finestra **[!UICONTROL Proprietà campo]** a destra. Ai fini di questa esercitazione, imposta **[!UICONTROL weeklySales]** come **[!UICONTROL funzionalità di destinazione]** e tutto il resto come **[!UICONTROL funzionalità di input]**. Seleziona **[!UICONTROL Successivo]** per rivedere la nuova ricetta configurata.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Rivedi la ricetta, aggiungi, modifica o rimuovi le configurazioni come necessario. Seleziona **[!UICONTROL Fine]** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Procedi ai [passaggi successivi](#next-steps) per scoprire come creare un modello in [!DNL Data Science Workspace] utilizzando la ricetta di vendita al dettaglio appena creata.

### Importa ricetta basata su Docker - Scala {#scala}

Iniziare navigando e selezionando **[!UICONTROL Flussi di lavoro]** che si trovano in alto a sinistra nell&#39;interfaccia utente [!DNL Platform]. Quindi, seleziona **Importa ricetta** e seleziona **[!UICONTROL Avvia]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configura** per il flusso di lavoro **Importa ricetta**. Inserisci un nome e una descrizione per la ricetta, quindi seleziona **[!UICONTROL Successivo]** nell&#39;angolo in alto a destra per procedere.

![configura flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nell&#39;esercitazione [Creazione di pacchetti di file di origine in una ricetta](./package-source-files-recipe.md) è stato fornito un URL Docker al termine della creazione della ricetta di vendita al dettaglio utilizzando i file di origine Scala ([!DNL Spark]).

Una volta nella pagina **Seleziona origine**, incolla l&#39;URL Docker corrispondente alla composizione del pacchetto creata utilizzando i file di origine Scala nel campo URL Source. Quindi, importa il file di configurazione fornito trascinandolo e rilasciandolo oppure utilizza il browser del file system. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Seleziona **[!UICONTROL Spark]** nel menu a discesa **Runtime**. Una volta selezionato il runtime [!DNL Spark], l&#39;artefatto predefinito viene automaticamente popolato in **[!UICONTROL Docker]**. Selezionare **[!UICONTROL Regressione]** dal menu a discesa **Tipo**. Una volta compilato tutto, seleziona **[!UICONTROL Avanti]** nell&#39;angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> Il tipo supporta **[!UICONTROL Classificazione]** e **[!UICONTROL Regressione]**. Se il modello non rientra in uno di questi tipi, seleziona **[!UICONTROL Personalizzato]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Quindi, seleziona gli schemi di input e output per la vendita al dettaglio utilizzando il selettore **Gestisci schemi**. Gli schemi sono stati creati utilizzando lo script di avvio fornito nell&#39;esercitazione [Crea schema e set di dati per la vendita al dettaglio](../models-recipes/create-retails-sales-dataset.md).

![gestisci schemi](../images/models-recipes/import-package-ui/manage-schemas.png)

Nella sezione **Gestione delle funzionalità**, seleziona l&#39;identificazione del tenant nel visualizzatore di schema per espandere lo schema di input Retail Sales. Selezionare le funzionalità di input e output evidenziando la funzionalità desiderata e selezionando **[!UICONTROL Funzionalità di input]** o **[!UICONTROL Funzionalità di destinazione]** nella finestra **[!UICONTROL Proprietà campo]** a destra. Ai fini di questa esercitazione, impostare &quot;[!UICONTROL weeklySales]&quot; come **[!UICONTROL funzionalità di destinazione]** e tutto il resto come **[!UICONTROL funzionalità di input]**. Seleziona **[!UICONTROL Successivo]** per rivedere la nuova ricetta configurata.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Rivedi la ricetta, aggiungi, modifica o rimuovi le configurazioni come necessario. Seleziona **[!UICONTROL Fine]** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Procedi ai [passaggi](#next-steps) successivi per scoprire come creare un modello utilizzando [!DNL Data Science Workspace] la ricetta di vendita al dettaglio appena creata.

## Passaggi successivi {#next-steps}

Questo esercitazione fornito informazione approfondita sulla configurazione e l&#39;importazione di una ricetta in [!DNL Data Science Workspace]. Ora puoi creare, addestrare e valutare un modello utilizzando la ricetta appena creata.

- [Addestra e valuta un modello nell’interfaccia utente](./train-evaluate-model-ui.md)
- [Formazione e valutazione di un modello tramite l’API](./train-evaluate-model-api.md)
