---
keywords: Experience Platform;importazione di ricetta confezionata;Data Science Workspace;argomenti popolari;ricette;ui;crea motore
solution: Experience Platform
title: Importare una composizione in pacchetto nell’interfaccia utente di Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione fornisce informazioni su come configurare e importare una ricetta in pacchetto utilizzando l'esempio di vendita al dettaglio fornito. Al termine di questa esercitazione, sarai in grado di creare, addestrare e valutare un modello in Adobe Experience Platform Data Science Workspace.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 0%

---

# Importare una ricetta confezionata nell’interfaccia utente di Data Science Workspace

Questa esercitazione fornisce informazioni su come configurare e importare una ricetta in pacchetto utilizzando l&#39;esempio di vendita al dettaglio fornito. Al termine di questa esercitazione, sarai in grado di creare, addestrare e valutare un modello in Adobe Experience Platform [!DNL Data Science Workspace].

## Prerequisiti

Questa esercitazione richiede una ricetta confezionata sotto forma di URL immagine Docker. Per ulteriori informazioni, consulta l’esercitazione su come [creare un pacchetto di file di origine in una composizione](./package-source-files-recipe.md) .

## Flusso di lavoro dell’interfaccia

L&#39;importazione di una ricetta in pacchetto in [!DNL Data Science Workspace] richiede configurazioni specifiche di ricetta, compilate in un singolo file JavaScript Object Notation (JSON), questa compilazione di configurazioni di ricette è definita file di configurazione. Una ricetta confezionata con un particolare insieme di configurazioni è definita un&#39;istanza di ricetta. Una ricetta può essere utilizzata per creare molte istanze di ricette in [!DNL Data Science Workspace].

Il flusso di lavoro per l’importazione di una ricetta di pacchetto è costituito dai seguenti passaggi:
- [Configurare una ricetta](#configure)
- [Ricetta basata su Docker di importazione - Python](#python)
- [Ricetta basata su Docker di importazione - R](#r)
- [Ricetta basata su Docker di importazione - PySpark](#pyspark)
- [Ricetta basata su Docker di importazione - Scala](#scala)

### Configura una ricetta {#configure}

Ogni istanza di ricetta in [!DNL Data Science Workspace] è accompagnata da una serie di configurazioni che adattano l&#39;istanza di ricetta a un particolare caso d&#39;uso. I file di configurazione definiscono i comportamenti di formazione e valutazione predefiniti di un modello creato utilizzando questa istanza di ricetta.

>[!NOTE]
>
>I file di configurazione sono specifici per ricetta e caso.

Di seguito è riportato un esempio di file di configurazione che mostra i comportamenti di formazione e valutazione predefiniti per la ricetta Vendite al dettaglio.

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
| `ACP_DSW_INPUT_FEATURES` | Stringa | Elenco degli attributi dello schema di input separati da virgole. |
| `ACP_DSW_TARGET_FEATURES` | Stringa | Elenco degli attributi dello schema di output separati da virgole. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se le funzioni di input e output sono modificabili |
| `tenantId` | Stringa | Questo ID assicura che le risorse create siano spuntate correttamente e contenute all’interno dell’organizzazione IMS. [Segui i passaggi ](../../xdm/api/getting-started.md#know-your-tenant_id) per trovare l’ID tenant. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Stringa | Lo schema di input utilizzato per la formazione di un modello. Lascia vuoto questo campo durante l’importazione nell’interfaccia utente, sostituisci con ID schema di formazione durante l’importazione tramite API. |
| `evaluation.labelColumn` | Stringa | Etichetta colonna per le visualizzazioni di valutazione. |
| `evaluation.metrics` | Stringa | Elenco separato da virgole delle metriche di valutazione da utilizzare per la valutazione di un modello. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Stringa | Lo schema di output utilizzato per il punteggio di un modello. Lascia vuoto questo campo durante l’importazione nell’interfaccia utente, sostituiscilo con il punteggio SchemaID durante l’importazione tramite API. |

Ai fini di questa esercitazione, puoi lasciare i file di configurazione predefiniti per la ricetta Vendite al dettaglio in [!DNL Data Science Workspace] Riferimento nel modo in cui sono.

### Ricetta basata su Docker di importazione - [!DNL Python] {#python}

Per iniziare, vai e seleziona **[!UICONTROL Workflows]** in alto a sinistra nell’ interfaccia utente di [!DNL Platform] . Quindi, seleziona **Ricetta importazione** e seleziona **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configura** per il flusso di lavoro **Ricetta importazione** . Inserisci un nome e una descrizione per la ricetta, quindi seleziona **[!UICONTROL Next]** nell’angolo in alto a destra.

![configurare il flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nel [Crea un pacchetto di file di origine in un tutorial Recipe](./package-source-files-recipe.md), al termine della creazione della ricetta di vendita al dettaglio tramite i file di origine Python è stato fornito un URL Docker.

Una volta nella pagina **Seleziona origine**, incolla l&#39;URL Docker corrispondente alla composizione del pacchetto generato utilizzando i file di origine [!DNL Python] nel campo **[!UICONTROL Source URL]** . Quindi, importa il file di configurazione fornito trascinandolo e rilasciandolo oppure utilizza il file system **Browser**. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Seleziona **[!UICONTROL Python]** nel menu a discesa **Runtime** e **[!UICONTROL Classification]** nel menu a discesa **Tipo** . Una volta compilato tutto, seleziona **[!UICONTROL Next]** nell’angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> Il tipo supporta **[!UICONTROL Classification]** e **[!UICONTROL Regression]**. Se il modello non rientra in uno di questi tipi, selezionare **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Quindi, seleziona gli schemi di input e output di vendita al dettaglio nella sezione **Gestisci schemi**, sono stati creati utilizzando lo script di avvio fornito nell&#39;esercitazione [creare lo schema di vendita al dettaglio e il set di dati](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Nella sezione **Gestione funzioni**, seleziona l’identificazione del tenant nel visualizzatore schema per espandere lo schema di input Vendite al dettaglio. Seleziona le funzioni di input e output evidenziando la funzione desiderata e seleziona **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** nella finestra **[!UICONTROL Field Properties]** a destra. Ai fini di questa esercitazione, imposta **[!UICONTROL weeklySales]** come **[!UICONTROL Target Feature]** e tutto il resto come **[!UICONTROL Input Feature]**. Seleziona **[!UICONTROL Next]** per rivedere la tua nuova ricetta configurata.

Esamina la ricetta, aggiungi, modifica o rimuovi le configurazioni in base alle necessità. Seleziona **[!UICONTROL Finish]** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Procedi ai [passaggi successivi](#next-steps) per scoprire come creare un modello in [!DNL Data Science Workspace] utilizzando la ricetta vendite al dettaglio appena creata.

### Ricetta basata su Docker di importazione - R {#r}

Per iniziare, vai e seleziona **[!UICONTROL Workflows]** in alto a sinistra nell’ interfaccia utente di [!DNL Platform] . Quindi, seleziona **Ricetta importazione** e seleziona **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configura** per il flusso di lavoro **Ricetta importazione** . Inserisci un nome e una descrizione per la ricetta, quindi seleziona **[!UICONTROL Next]** nell’angolo in alto a destra.

![configurare il flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nel [Crea un pacchetto di file di origine in un tutorial Recipe](./package-source-files-recipe.md) , al termine della creazione della ricetta Vendite al dettaglio utilizzando i file di origine R è stato fornito un URL Docker.

Una volta nella pagina **Seleziona origine**, incolla l&#39;URL Docker corrispondente alla composizione del pacchetto generato utilizzando i file di origine R nel campo **[!UICONTROL Source URL]** . Quindi, importa il file di configurazione fornito trascinandolo e rilasciandolo oppure utilizza il file system **Browser**. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Seleziona **[!UICONTROL R]** nel menu a discesa **Runtime** e **[!UICONTROL Classification]** nel menu a discesa **Tipo** . Una volta compilato tutto, seleziona **[!UICONTROL Next]** nell’angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> ** Typesupport  **[!UICONTROL Classification]** e  **[!UICONTROL Regression]**. Se il modello non rientra in uno di questi tipi, selezionare **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Quindi, seleziona gli schemi di input e output di vendita al dettaglio nella sezione **Gestisci schemi**, sono stati creati utilizzando lo script di avvio fornito nell&#39;esercitazione [creare lo schema di vendita al dettaglio e il set di dati](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Nella sezione *Gestione funzioni*, seleziona l’identificazione del tenant nel visualizzatore schema per espandere lo schema di input Vendite al dettaglio. Seleziona le funzioni di input e output evidenziando la funzione desiderata e seleziona **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** nella finestra **[!UICONTROL Field Properties]** a destra. Ai fini di questa esercitazione, imposta **[!UICONTROL weeklySales]** come **[!UICONTROL Target Feature]** e tutto il resto come **[!UICONTROL Input Feature]**. Seleziona **[!UICONTROL Next]** per rivedere la tua nuova ricetta configurata.

Esamina la ricetta, aggiungi, modifica o rimuovi le configurazioni in base alle necessità. Seleziona **Fine** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Procedi ai [passaggi successivi](#next-steps) per scoprire come creare un modello in [!DNL Data Science Workspace] utilizzando la ricetta vendite al dettaglio appena creata.

### Ricetta basata su Docker di importazione - PySpark {#pyspark}

Per iniziare, vai e seleziona **[!UICONTROL Workflows]** in alto a sinistra nell’ interfaccia utente di [!DNL Platform] . Quindi, seleziona **Ricetta importazione** e seleziona **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configura** per il flusso di lavoro **Ricetta importazione** . Inserisci un nome e una descrizione per la ricetta, quindi seleziona **[!UICONTROL Next]** nell’angolo in alto a destra per proseguire.

![configurare il flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nel [Crea un pacchetto di file di origine in un tutorial Recipe](./package-source-files-recipe.md) , al termine della creazione della ricetta di vendita al dettaglio tramite i file di origine PySpark è stato fornito un URL Docker.

Una volta nella pagina **Seleziona origine**, incolla l&#39;URL Docker corrispondente alla ricetta in pacchetto creata utilizzando i file di origine PySpark nel campo **[!UICONTROL Source URL]** . Quindi, importa il file di configurazione fornito trascinandolo e rilasciandolo oppure utilizza il file system **Browser**. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Seleziona **[!UICONTROL PySpark]** nel menu a discesa **Runtime** . Una volta selezionato il runtime PySpark, l’artefatto predefinito si popola automaticamente su **[!UICONTROL Docker]**. Quindi, seleziona **[!UICONTROL Classification]** nel menu a discesa **Tipo** . Una volta compilato tutto, seleziona **[!UICONTROL Next]** nell’angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> ** Typesupport  **[!UICONTROL Classification]** e  **[!UICONTROL Regression]**. Se il modello non rientra in uno di questi tipi, selezionare **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Quindi, seleziona gli schemi di input e output di vendita al dettaglio utilizzando il selettore **Gestisci schemi**, gli schemi sono stati creati utilizzando lo script di avvio fornito nell&#39;esercitazione [creare lo schema di vendita al dettaglio e il set di dati](../models-recipes/create-retails-sales-dataset.md).

![gestire gli schemi](../images/models-recipes/import-package-ui/manage-schemas.png)

Nella sezione **Gestione funzioni**, seleziona l’identificazione del tenant nel visualizzatore schema per espandere lo schema di input Vendite al dettaglio. Seleziona le funzioni di input e output evidenziando la funzione desiderata e seleziona **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** nella finestra **[!UICONTROL Field Properties]** a destra. Ai fini di questa esercitazione, imposta **[!UICONTROL weeklySales]** come **[!UICONTROL Target Feature]** e tutto il resto come **[!UICONTROL Input Feature]**. Seleziona **[!UICONTROL Next]** per rivedere la tua nuova ricetta configurata.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Esamina la ricetta, aggiungi, modifica o rimuovi le configurazioni in base alle necessità. Seleziona **[!UICONTROL Finish]** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Procedi ai [passaggi successivi](#next-steps) per scoprire come creare un modello in [!DNL Data Science Workspace] utilizzando la ricetta vendite al dettaglio appena creata.

### Ricetta basata su Docker di importazione - Scala {#scala}

Per iniziare, vai e seleziona **[!UICONTROL Workflows]** in alto a sinistra nell’ interfaccia utente di [!DNL Platform] . Quindi, seleziona **Ricetta importazione** e seleziona **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configura** per il flusso di lavoro **Ricetta importazione** . Inserisci un nome e una descrizione per la ricetta, quindi seleziona **[!UICONTROL Next]** nell’angolo in alto a destra per proseguire.

![configurare il flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nel [Crea un pacchetto di file di origine in un tutorial Recipe](./package-source-files-recipe.md), al termine della creazione della ricetta di vendita al dettaglio tramite file di origine Scala ([!DNL Spark]) è stato fornito un URL Docker.

Una volta nella pagina **Seleziona origine**, incolla l&#39;URL Docker corrispondente alla composizione del pacchetto generato utilizzando i file di origine Scala nel campo URL sorgente. Quindi, importare il file di configurazione fornito trascinandolo e rilasciandolo oppure utilizzare il browser del file system. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Seleziona **[!UICONTROL Spark]** nel menu a discesa **Runtime** . Una volta che il runtime [!DNL Spark] è selezionato, l’artefatto predefinito si popola automaticamente su **[!UICONTROL Docker]**. Quindi, seleziona **[!UICONTROL Regression]** dal menu a discesa **Tipo** . Una volta compilato tutto, seleziona **[!UICONTROL Next]** nell’angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> Il tipo supporta **[!UICONTROL Classification]** e **[!UICONTROL Regression]**. Se il modello non rientra in uno di questi tipi, selezionare **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Quindi, seleziona gli schemi di input e output di vendita al dettaglio utilizzando il selettore **Gestisci schemi**, gli schemi sono stati creati utilizzando lo script di avvio fornito nell&#39;esercitazione [creare lo schema di vendita al dettaglio e il set di dati](../models-recipes/create-retails-sales-dataset.md).

![gestire gli schemi](../images/models-recipes/import-package-ui/manage-schemas.png)

Nella sezione **Gestione funzioni**, seleziona l’identificazione del tenant nel visualizzatore schema per espandere lo schema di input Vendite al dettaglio. Seleziona le funzioni di input e output evidenziando la funzione desiderata e seleziona **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** nella finestra **[!UICONTROL Field Properties]** a destra. Ai fini di questa esercitazione, imposta &quot;[!UICONTROL weeklySales]&quot; come **[!UICONTROL Target Feature]** e tutto il resto come **[!UICONTROL Input Feature]**. Seleziona **[!UICONTROL Next]** per rivedere la tua nuova ricetta configurata.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Esamina la ricetta, aggiungi, modifica o rimuovi le configurazioni in base alle necessità. Seleziona **[!UICONTROL Finish]** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Procedi ai [passaggi successivi](#next-steps) per scoprire come creare un modello in [!DNL Data Science Workspace] utilizzando la ricetta vendite al dettaglio appena creata.

## Passaggi successivi {#next-steps}

Questa esercitazione ha fornito informazioni sulla configurazione e l&#39;importazione di una ricetta in [!DNL Data Science Workspace]. È ora possibile creare, addestrare e valutare un modello utilizzando la ricetta appena creata.

- [Formazione e valutazione di un modello nell’interfaccia utente](./train-evaluate-model-ui.md)
- [Addestrare e valutare un modello utilizzando l’API](./train-evaluate-model-api.md)
