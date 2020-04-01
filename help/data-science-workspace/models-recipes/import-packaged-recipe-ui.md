---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importare una ricetta in pacchetti (interfaccia utente)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Importare una ricetta in pacchetti (interfaccia utente)

Questa esercitazione fornisce informazioni su come configurare e importare una ricetta in pacchetti utilizzando l&#39;esempio di vendita al dettaglio fornito. Al termine di questa esercitazione, potrai creare, formare e valutare un modello in Adobe Experience Platform Data Science Workspace.

## Prerequisiti

Questa esercitazione richiede una ricetta in pacchetti sotto forma di URL immagine Docker o di file binario. Per ulteriori informazioni, consulta l’esercitazione su come [creare pacchetti di file sorgente in una ricetta](./package-source-files-recipe.md) .

## Flusso di lavoro interfaccia

L&#39;importazione di una ricetta compressa in Data Science Workspace richiede configurazioni di ricette specifiche, compilate in un unico file JSON (JavaScript Object Notation). Questa raccolta di configurazioni di ricette viene definita file **di** configurazione. Una ricetta confezionata con una particolare serie di configurazioni viene definita come un&#39;istanza **di** ricetta. Una ricetta può essere utilizzata per creare molte istanze di ricette in Data Science Workspace.

Il flusso di lavoro per l’importazione di una ricetta di pacchetto comprende i seguenti passaggi:
- [Configurare una ricetta](#configure)
- [Importa ricetta binaria basata su - PySpark](#pyspark)
- [Importa ricetta binaria basata su - Scala Spark](#scala)
- [Ricetta basata sul Docker di importazione - Python](#python)
- [Ricetta basata sul Docker di importazione - R](#r)

### Configurare una ricetta {#configure}

Ogni istanza di ricetta in Data Science Workspace è accompagnata da una serie di configurazioni che adattano l&#39;istanza di ricetta a un particolare caso d&#39;uso. I file di configurazione definiscono i comportamenti predefiniti di formazione e valutazione di un modello creato utilizzando questa istanza di ricetta.

>[!NOTE] I file di configurazione sono specifici per ricetta e caso.

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
| `tenantId` | Stringa | Questo ID garantisce che le risorse create siano inserite correttamente nell’organizzazione IMS. [Segui i passaggi qui](../../xdm/api/getting-started.md#know-your-tenant_id) per trovare l&#39;ID tenant. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Stringa | Lo schema di input utilizzato per la formazione di un modello. Lasciate vuoto questo campo durante l’importazione nell’interfaccia utente, sostituitelo con ID schema formazione durante l’importazione tramite API. |
| `evaluation.labelColumn` | Stringa | Etichetta colonna per le visualizzazioni di valutazione. |
| `evaluation.metrics` | Stringa | Elenco separato da virgole delle metriche di valutazione da utilizzare per la valutazione di un modello. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Stringa | Lo schema di output utilizzato per il punteggio di un modello. Lasciate questo vuoto durante l&#39;importazione nell&#39;interfaccia utente, sostituitelo con l&#39;ID schema punteggio durante l&#39;importazione tramite API. |

Con questa esercitazione puoi lasciare i file di configurazione predefiniti per la ricetta Vendite al dettaglio nella Guida di riferimento dell&#39;area di lavoro di analisi dei dati come sono.

### Importa ricetta binaria basata su - PySpark {#pyspark}

Nei file sorgente [Package in un&#39;esercitazione Recipe](./package-source-files-recipe.md) , è stato creato un file binario **EGG** utilizzando i file sorgente PySpark per le vendite al dettaglio.

1. In [Adobe Experience Platform](https://platform.adobe.com/), trova il pannello di navigazione a sinistra e fai clic su **Flussi di lavoro**. Nell&#39;interfaccia Flussi di lavoro, **avvia** un nuovo processo di **importazione della ricetta dal file** di origine.
   ![](../images/models-recipes/import-package-ui/workflow_ss.png)
2. Immettete un nome appropriato per la ricetta Vendite al dettaglio. Ad esempio, &quot;Ricetta vendita al dettaglio PySpark&quot;. Facoltativamente, potete includere una descrizione della ricetta e un URL della documentazione. Al termine, fate clic su **Avanti** .
   ![](../images/models-recipes/import-package-ui/recipe_info.png)
3. Importare la ricetta Vendite al dettaglio PySpark creata nei file di origine del [pacchetto in un&#39;esercitazione sulla ricetta](./package-source-files-recipe.md) trascinando e rilasciando oppure utilizzare il **browser** del file system. La ricetta confezionata deve essere situata in `experience-platform-dsw-reference/recipes/pyspark/dist`.
Allo stesso modo, potete importare il file di configurazione fornito trascinando e rilasciando oppure utilizzare il **browser** del file system. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/pyspark/pipeline.json`. Fate clic su **Avanti** quando entrambi i file sono stati forniti.
   ![](../images/models-recipes/import-package-ui/recipe_source.png)
4. A questo punto si possono verificare errori. Si tratta di un comportamento normale che deve essere previsto. Selezionare gli schemi di input e output di Vendite al dettaglio nella sezione **Gestisci schemi**, creati utilizzando lo script di avvio fornito nell&#39;esercitazione [Creazione dello schema di vendita al dettaglio e del dataset](../models-recipes/create-retails-sales-dataset.md) .
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
Nella sezione Gestione **** funzioni, fate clic sull&#39;identificazione del tenant nel visualizzatore schema per espandere lo schema di input Vendite al dettaglio. Selezionate le funzioni di input e output evidenziando la funzione desiderata, quindi selezionate Feature **di** input o Feature **di** destinazione nella finestra Proprietà **** campo di destra. Per questa esercitazione, impostate **settimanalmenteSales** come funzione **** Target e tutto il resto come funzione **** Input. Fate clic su **Avanti** per rivedere la nuova ricetta configurata.
5. Esaminate la ricetta, aggiungete, modificate o rimuovete le configurazioni in base alle vostre esigenze. Fate clic su **Fine** per creare la ricetta.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Congratulazioni, hai creato la ricetta Vendite al dettaglio! Passa ai passaggi [](#next-steps) successivi per scoprire come creare un modello in Data Science Workspace utilizzando la ricetta di vendita al dettaglio appena creata.


### Importa ricetta binaria basata su - Scala Spark {#scala}

Nei file sorgente [Package in un&#39;esercitazione Recipe](./package-source-files-recipe.md) , è stato creato un file binario **JAR** utilizzando i file sorgente Scala delle vendite al dettaglio.

1. In [Adobe Experience Platform](https://platform.adobe.com/), trova il pannello di navigazione a sinistra e fai clic su **Flussi di lavoro**. Nell&#39;interfaccia Flussi di lavoro, **avvia** un nuovo processo di **importazione della ricetta dal file** di origine.
   ![](../images/models-recipes/import-package-ui/workflow_ss.png)
2. Immettete un nome appropriato per la ricetta Vendite al dettaglio. Ad esempio, &quot;Ricetta di vendita al dettaglio Scala Spark&quot;. Facoltativamente, potete includere una descrizione della ricetta e un URL della documentazione. Al termine, fate clic su **Avanti** .
   ![](../images/models-recipes/import-package-ui/recipe_info_scala.png)
3. Importare la ricetta Vendite al dettaglio Scala Spark creata nei file sorgente [Package in un&#39;esercitazione Recipe](./package-source-files-recipe.md) trascinando o rilasciando il file system o utilizzando il **browser** del file system. La ricetta confezionata **con dipendenze** si trova in `experience-platform-dsw-reference/recipes/scala/target`. Allo stesso modo, potete importare il file di configurazione fornito trascinando e rilasciando oppure utilizzare il **browser** del file system. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/scala/src/main/resources/pipelineservice.json`. Fate clic su **Avanti** quando entrambi i file sono stati forniti.
   ![](../images/models-recipes/import-package-ui/recipe_source_scala.png)
4. A questo punto si possono verificare errori. Si tratta di un comportamento normale che deve essere previsto. Selezionare gli schemi di input e output di Vendite al dettaglio nella sezione **Gestisci schemi**, creati utilizzando lo script di avvio fornito nell&#39;esercitazione [Creazione dello schema di vendita al dettaglio e del dataset](../models-recipes/create-retails-sales-dataset.md) .
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
Nella sezione Gestione **** funzioni, fate clic sull&#39;identificazione del tenant nel visualizzatore schema per espandere lo schema di input Vendite al dettaglio. Selezionate le funzioni di input e output evidenziando la funzione desiderata, quindi selezionate Feature **di** input o Feature **di** destinazione nella finestra Proprietà **** campo di destra. Per questa esercitazione, impostate **settimanalmenteSales** come funzione **** Target e tutto il resto come funzione **** Input. Fate clic su **Avanti** per rivedere la nuova ricetta configurata.
5. Esaminate la ricetta, aggiungete, modificate o rimuovete le configurazioni in base alle vostre esigenze. Fate clic su **Fine** per creare la ricetta.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Congratulazioni, hai creato la ricetta Vendite al dettaglio! Passa ai passaggi [](#next-steps) successivi per scoprire come creare un modello in Data Science Workspace utilizzando la ricetta di vendita al dettaglio appena creata.

### Ricetta basata sul Docker di importazione - Python {#python}

Nei file di origine del [pacchetto in un&#39;esercitazione sulla ricetta](./package-source-files-recipe.md) , al termine della creazione della ricetta Vendite al dettaglio tramite i file di origine Python è stato fornito un URL Docker.

1. Incollate l&#39;URL Docker corrispondente alla ricetta del pacchetto creata utilizzando i file sorgente Python nel campo URL **** sorgente. Quindi, importate il file di configurazione fornito trascinandolo e rilasciandolo oppure utilizzate il **Browser** del file system. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Fate clic su **Avanti** dopo aver fornito entrambi gli elementi.
   ![](../images/models-recipes/import-package-ui/recipe_source_python.png)
2. Selezionare gli schemi di input e output di Vendite al dettaglio nella sezione **Gestisci schemi**, creati utilizzando lo script di avvio fornito nell&#39;esercitazione [Creazione dello schema di vendita al dettaglio e del dataset](../models-recipes/create-retails-sales-dataset.md) .
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
Nella sezione Gestione **** funzioni, fate clic sull&#39;identificazione del tenant nel visualizzatore schema per espandere lo schema di input Vendite al dettaglio. Selezionate le funzioni di input e output evidenziando la funzione desiderata, quindi selezionate Feature **di** input o Feature **di** destinazione nella finestra Proprietà **** campo di destra. Per questa esercitazione, impostate **settimanalmenteSales** come funzione **** Target e tutto il resto come funzione **** Input. Fate clic su **Avanti** per rivedere la nuova ricetta configurata.
3. Esaminate la ricetta, aggiungete, modificate o rimuovete le configurazioni in base alle vostre esigenze. Fate clic su **Fine** per creare la ricetta.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Congratulazioni, hai creato la ricetta Vendite al dettaglio! Passa ai passaggi [](#next-steps) successivi per scoprire come creare un modello in Data Science Workspace utilizzando la ricetta di vendita al dettaglio appena creata.

### Ricetta basata sul Docker di importazione - R {#r}

Nei file di origine del [pacchetto in un&#39;esercitazione sulla ricetta](./package-source-files-recipe.md) , al termine della creazione della ricetta Vendite al dettaglio tramite i file sorgente R è stato fornito un URL Docker.

1. Incollate l&#39;URL Docker corrispondente alla ricetta del pacchetto creata utilizzando i file sorgente R nel campo URL **** sorgente. Quindi, importate il file di configurazione fornito trascinandolo e rilasciandolo oppure utilizzate il **Browser** del file system. Il file di configurazione fornito si trova in `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Fate clic su **Avanti** dopo aver fornito entrambi gli elementi.
   ![](../images/models-recipes/import-package-ui/recipe_source_R.png)
2. Selezionare gli schemi di input e output di Vendite al dettaglio nella sezione **Gestisci schemi**, creati utilizzando lo script di avvio fornito nell&#39;esercitazione [Creazione dello schema di vendita al dettaglio e del dataset](../models-recipes/create-retails-sales-dataset.md) .
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
Nella sezione Gestione **** funzioni, fate clic sull&#39;identificazione del tenant nel visualizzatore schema per espandere lo schema di input Vendite al dettaglio. Selezionate le funzioni di input e output evidenziando la funzione desiderata, quindi selezionate Feature **di** input o Feature **di** destinazione nella finestra Proprietà **** campo di destra. Per questa esercitazione, impostate **settimanalmenteSales** come funzione **** Target e tutto il resto come funzione **** Input. Fate clic su **Avanti** per rivedere la nuova ricetta configurata.
3. Esaminate la ricetta, aggiungete, modificate o rimuovete le configurazioni in base alle vostre esigenze. Fate clic su **Fine** per creare la ricetta.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Congratulazioni, hai creato la ricetta Vendite al dettaglio! Passa ai passaggi [](#next-steps) successivi per scoprire come creare un modello in Data Science Workspace utilizzando la ricetta di vendita al dettaglio appena creata.

## Passaggi successivi

Questa esercitazione ha fornito informazioni sulla configurazione e l&#39;importazione di una ricetta in Data Science Workspace. Ora puoi creare, formare e valutare un modello utilizzando la ricetta appena creata.

- [Formazione e valutazione di un modello nell’interfaccia utente](./train-evaluate-model-ui.md)
- [Formazione e valutazione di un modello mediante l&#39;API](./train-evaluate-model-api.md)