---
keywords: ' Experience Platform;importazione di ricetta confezionata;Data Science Workspace;argomenti più comuni;ricette;ui;creare motore'
solution: Experience Platform
title: Importare una ricetta in pacchetto nell’interfaccia utente di Data Science Workspace
topic: tutorial
type: Tutorial
description: Questa esercitazione fornisce informazioni su come configurare e importare una ricetta in pacchetti utilizzando l'esempio di vendita al dettaglio fornito. Al termine di questa esercitazione, sarà possibile creare, formare e valutare un modello in Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 0%

---


# Importare una ricetta preassemblata nell’interfaccia utente di Data Science Workspace

Questa esercitazione fornisce informazioni su come configurare e importare una ricetta in pacchetti utilizzando l&#39;esempio di vendita al dettaglio fornito. Al termine di questa esercitazione, sarà possibile creare, formare e valutare un modello in Adobe Experience Platform [!DNL Data Science Workspace].

## Prerequisiti

Questa esercitazione richiede una ricetta in pacchetti sotto forma di URL immagine Docker. Per ulteriori informazioni, consulta l&#39;esercitazione su come [Creare pacchetti di file sorgente in un file Recipe](./package-source-files-recipe.md).

## Flusso di lavoro interfaccia

L&#39;importazione di una ricetta in pacchetti in [!DNL Data Science Workspace] richiede specifiche configurazioni di ricette, compilate in un unico file JSON (JavaScript Object Notation), questa raccolta di configurazioni di ricette viene definita file di configurazione. Una ricetta confezionata con una particolare serie di configurazioni viene definita come un&#39;istanza di ricetta. Una ricetta può essere utilizzata per creare molte istanze di ricette in [!DNL Data Science Workspace].

Il flusso di lavoro per l’importazione di una ricetta di pacchetto comprende i seguenti passaggi:
- [Configurare una ricetta](#configure)
- [Ricetta basata sul Docker di importazione - Python](#python)
- [Ricetta basata sul Docker di importazione - R](#r)
- [Ricetta basata sul Docker di importazione - PySpark](#pyspark)
- [Ricetta basata sul Docker di importazione - Scala](#scala)

### Configurare una ricetta {#configure}

Ogni istanza di ricetta in [!DNL Data Science Workspace] è accompagnata da una serie di configurazioni che adattano l&#39;istanza di ricetta a un caso d&#39;uso particolare. I file di configurazione definiscono i comportamenti predefiniti di formazione e valutazione di un modello creato utilizzando questa istanza di ricetta.

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
| `learning_rate` | Numero | Scalare per la moltiplicazione della sfumatura. |
| `n_estimators` | Numero | Numero di alberi nella foresta per il classificatore casuale della foresta. |
| `max_depth` | Numero | Profondità massima di un albero in Classificatore Foresta casuale. |
| `ACP_DSW_INPUT_FEATURES` | Stringa | Elenco degli attributi dello schema di input separati da virgola. |
| `ACP_DSW_TARGET_FEATURES` | Stringa | Elenco degli attributi dello schema di output separati da virgola. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se le funzioni di input e output sono modificabili |
| `tenantId` | Stringa | Questo ID garantisce che le risorse create siano inserite correttamente nell’organizzazione IMS. [Segui i passaggi ](../../xdm/api/getting-started.md#know-your-tenant_id) per trovare l&#39;ID tenant. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Stringa | Lo schema di input utilizzato per la formazione di un modello. Lasciate vuoto questo campo durante l’importazione nell’interfaccia utente, sostituitelo con ID schema formazione durante l’importazione tramite API. |
| `evaluation.labelColumn` | Stringa | Etichetta colonna per le visualizzazioni di valutazione. |
| `evaluation.metrics` | Stringa | Elenco separato da virgole delle metriche di valutazione da utilizzare per la valutazione di un modello. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Stringa | Lo schema di output utilizzato per il punteggio di un modello. Lasciate questo vuoto durante l&#39;importazione nell&#39;interfaccia utente, sostituitelo con l&#39;ID schema punteggio durante l&#39;importazione tramite API. |

Per questa esercitazione, puoi lasciare i file di configurazione predefiniti per la ricetta Vendite al dettaglio nella [!DNL Data Science Workspace] Guida di riferimento come sono.

### Ricetta basata su Docker di importazione - [!DNL Python] {#python}

Iniziate navigando e selezionando **[!UICONTROL Workflows]** in alto a sinistra nell&#39;interfaccia [!DNL Platform]. Quindi, selezionare **Importa ricetta** e fare clic su **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configure** per il flusso di lavoro **Import recipe**. Immettete un nome e una descrizione per la ricetta, quindi selezionate **[!UICONTROL Next]** nell&#39;angolo in alto a destra.

![configura flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nei file sorgente [Pacchetto in un&#39;esercitazione Recipe](./package-source-files-recipe.md) è stato fornito un URL Docker alla fine della creazione della ricetta Vendite al dettaglio utilizzando i file sorgente Python.

Una volta che vi trovate sulla pagina **Seleziona origine**, incollate l&#39;URL Docker corrispondente alla ricetta del pacchetto creato utilizzando i file sorgente [!DNL Python] nel campo **[!UICONTROL Source URL]**. Quindi, importare il file di configurazione fornito trascinando e rilasciando oppure utilizzare il file system **Browser**. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Selezionare **[!UICONTROL Python]** nel menu a discesa **Runtime** e **[!UICONTROL Classification]** nel menu a discesa **Type**. Una volta compilato, fare clic su **[!UICONTROL Next]** nell&#39;angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> Il tipo supporta **[!UICONTROL Classification]** e **[!UICONTROL Regression]**. Se il modello non rientra in uno di questi tipi, selezionare **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Successivamente, selezionare gli schemi di input e output di Vendite al dettaglio nella sezione **Gestisci schemi**, creati utilizzando lo script di avvio fornito nell&#39;esercitazione [creare lo schema di vendita al dettaglio e il dataset](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Nella sezione **Gestione funzioni**, fare clic sull&#39;identificazione del tenant nel visualizzatore schema per espandere lo schema di immissione Vendite al dettaglio. Selezionare le funzioni di input e output evidenziando la funzione desiderata e selezionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** nella finestra **[!UICONTROL Field Properties]** a destra. Per questa esercitazione, impostare **[!UICONTROL weeklySales]** come **[!UICONTROL Target Feature]** e tutto il resto come **[!UICONTROL Input Feature]**. Fate clic su **[!UICONTROL Next]** per rivedere la nuova ricetta configurata.

Esaminate la ricetta, aggiungete, modificate o rimuovete le configurazioni in base alle vostre esigenze. Fate clic su **[!UICONTROL Finish]** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passate alla [fase successiva](#next-steps) per scoprire come creare un modello in [!DNL Data Science Workspace] utilizzando la ricetta vendite al dettaglio appena creata.

### Ricetta basata su Docker di importazione - R {#r}

Iniziate navigando e selezionando **[!UICONTROL Workflows]** in alto a sinistra nell&#39;interfaccia [!DNL Platform]. Quindi, selezionare **Importa ricetta** e fare clic su **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configure** per il flusso di lavoro **Import recipe**. Immettete un nome e una descrizione per la ricetta, quindi selezionate **[!UICONTROL Next]** nell&#39;angolo in alto a destra.

![configura flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nei file sorgente [Pacchetto in un&#39;esercitazione Recipe](./package-source-files-recipe.md), al termine della creazione della ricetta Vendite al dettaglio tramite file sorgente R è stato fornito un URL Docker.

Una volta che vi trovate sulla pagina **Seleziona origine**, incollate l&#39;URL Docker corrispondente alla ricetta del pacchetto creata utilizzando i file sorgente R nel campo **[!UICONTROL Source URL]**. Quindi, importare il file di configurazione fornito trascinando e rilasciando oppure utilizzare il file system **Browser**. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Selezionare **[!UICONTROL R]** nel menu a discesa **Runtime** e **[!UICONTROL Classification]** nel menu a discesa **Tipo**. Una volta compilato, fare clic su **[!UICONTROL Next]** nell&#39;angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> ** Typesupport  **[!UICONTROL Classification]** e  **[!UICONTROL Regression]**. Se il modello non rientra in uno di questi tipi, selezionare **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Successivamente, selezionare gli schemi di input e output di Vendite al dettaglio nella sezione **Gestisci schemi**, creati utilizzando lo script di avvio fornito nell&#39;esercitazione [creare lo schema di vendita al dettaglio e il dataset](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Nella sezione *Gestione funzioni*, fare clic sull&#39;identificazione del tenant nel visualizzatore schema per espandere lo schema di immissione Vendite al dettaglio. Selezionare le funzioni di input e output evidenziando la funzione desiderata e selezionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** nella finestra **[!UICONTROL Field Properties]** a destra. Per questa esercitazione, impostare **[!UICONTROL weeklySales]** come **[!UICONTROL Target Feature]** e tutto il resto come **[!UICONTROL Input Feature]**. Fate clic su **[!UICONTROL Next]** per rivedere la nuova ricetta configurata.

Esaminate la ricetta, aggiungete, modificate o rimuovete le configurazioni in base alle vostre esigenze. Fare clic su **Fine** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passate alla [fase successiva](#next-steps) per scoprire come creare un modello in [!DNL Data Science Workspace] utilizzando la ricetta vendite al dettaglio appena creata.

### Ricetta basata su Docker di importazione - PySpark {#pyspark}

Iniziate navigando e selezionando **[!UICONTROL Workflows]** in alto a sinistra nell&#39;interfaccia [!DNL Platform]. Quindi, selezionare **Importa ricetta** e fare clic su **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configure** per il flusso di lavoro **Import recipe**. Immettete un nome e una descrizione per la ricetta, quindi selezionate **[!UICONTROL Next]** nell&#39;angolo in alto a destra per proseguire.

![configura flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nei file sorgente [Pacchetto in un&#39;esercitazione Recipe](./package-source-files-recipe.md) è stato fornito un URL Docker alla fine della creazione della ricetta Vendite al dettaglio utilizzando i file sorgente PySpark.

Una volta che vi trovate sulla pagina **Seleziona origine**, incollate l&#39;URL Docker corrispondente alla ricetta del pacchetto creata utilizzando i file sorgente PySpark nel campo **[!UICONTROL Source URL]**. Quindi, importare il file di configurazione fornito trascinando e rilasciando oppure utilizzare il file system **Browser**. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Selezionare **[!UICONTROL PySpark]** nel menu a discesa **Runtime**. Una volta selezionato il runtime PySpark, l&#39;artifact predefinito viene automaticamente popolato in **[!UICONTROL Docker]**. Selezionare quindi **[!UICONTROL Classification]** nel menu a discesa **Tipo**. Una volta compilato, fare clic su **[!UICONTROL Next]** nell&#39;angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> ** Typesupport  **[!UICONTROL Classification]** e  **[!UICONTROL Regression]**. Se il modello non rientra in uno di questi tipi, selezionare **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Successivamente, selezionare gli schemi di input e output di Vendite al dettaglio nella sezione **Gestisci schemi**, creati utilizzando lo script di avvio fornito nell&#39;esercitazione [creare lo schema di vendita al dettaglio e il dataset](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Nella sezione **Gestione funzioni**, fare clic sull&#39;identificazione del tenant nel visualizzatore schema per espandere lo schema di immissione Vendite al dettaglio. Selezionare le funzioni di input e output evidenziando la funzione desiderata e selezionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** nella finestra **[!UICONTROL Field Properties]** a destra. Per questa esercitazione, impostare **[!UICONTROL weeklySales]** come **[!UICONTROL Target Feature]** e tutto il resto come **[!UICONTROL Input Feature]**. Fate clic su **[!UICONTROL Next]** per rivedere la nuova ricetta configurata.

Esaminate la ricetta, aggiungete, modificate o rimuovete le configurazioni in base alle vostre esigenze. Fate clic su **[!UICONTROL Finish]** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passate alla [fase successiva](#next-steps) per scoprire come creare un modello in [!DNL Data Science Workspace] utilizzando la ricetta vendite al dettaglio appena creata.

### Ricetta basata sul Docker di importazione - Scala {#scala}

Iniziate navigando e selezionando **[!UICONTROL Workflows]** in alto a sinistra nell&#39;interfaccia [!DNL Platform]. Quindi, selezionare **Importa ricetta** e fare clic su **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Viene visualizzata la pagina **Configure** per il flusso di lavoro **Import recipe**. Immettete un nome e una descrizione per la ricetta, quindi selezionate **[!UICONTROL Next]** nell&#39;angolo in alto a destra per proseguire.

![configura flusso di lavoro](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nei file sorgente [Pacchetto in un&#39;esercitazione Recipe](./package-source-files-recipe.md) è stato fornito un URL Docker alla fine della creazione della ricetta Vendite al dettaglio utilizzando file sorgente Scala ([!DNL Spark]).

Una volta che vi trovate sulla pagina **Seleziona origine**, incollate l&#39;URL Docker corrispondente alla ricetta del pacchetto creato utilizzando i file sorgente Scala nel campo URL sorgente. Quindi, importate il file di configurazione fornito trascinandolo e rilasciandolo oppure utilizzate il browser del file system. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Selezionare **[!UICONTROL Spark]** nel menu a discesa **Runtime**. Una volta selezionato il runtime [!DNL Spark], l&#39;artifact predefinito viene automaticamente popolato in **[!UICONTROL Docker]**. Selezionare quindi **[!UICONTROL Regression]** dal menu a discesa **Tipo**. Una volta compilato, fare clic su **[!UICONTROL Next]** nell&#39;angolo in alto a destra per passare a **Gestisci schemi**.

>[!NOTE]
>
> Il tipo supporta **[!UICONTROL Classification]** e **[!UICONTROL Regression]**. Se il modello non rientra in uno di questi tipi, selezionare **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Successivamente, selezionare gli schemi di input e output di Vendite al dettaglio nella sezione **Gestisci schemi**, creati utilizzando lo script di avvio fornito nell&#39;esercitazione [creare lo schema di vendita al dettaglio e il dataset](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Nella sezione **Gestione funzioni**, fare clic sull&#39;identificazione del tenant nel visualizzatore schema per espandere lo schema di immissione Vendite al dettaglio. Selezionare le funzioni di input e output evidenziando la funzione desiderata e selezionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** nella finestra **[!UICONTROL Field Properties]** a destra. Per questa esercitazione, impostare &quot;[!UICONTROL weeklySales]&quot; come **[!UICONTROL Target Feature]** e tutto il resto come **[!UICONTROL Input Feature]**. Fate clic su **[!UICONTROL Next]** per rivedere la nuova ricetta configurata.

Esaminate la ricetta, aggiungete, modificate o rimuovete le configurazioni in base alle vostre esigenze. Fate clic su **[!UICONTROL Finish]** per creare la ricetta.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passate alla [fase successiva](#next-steps) per scoprire come creare un modello in [!DNL Data Science Workspace] utilizzando la ricetta vendite al dettaglio appena creata.

## Passaggi successivi {#next-steps}

Questa esercitazione ha fornito informazioni sulla configurazione e l&#39;importazione di una ricetta in [!DNL Data Science Workspace]. Ora puoi creare, formare e valutare un modello utilizzando la ricetta appena creata.

- [Formazione e valutazione di un modello nell’interfaccia utente](./train-evaluate-model-ui.md)
- [Formazione e valutazione di un modello mediante l&#39;API](./train-evaluate-model-api.md)