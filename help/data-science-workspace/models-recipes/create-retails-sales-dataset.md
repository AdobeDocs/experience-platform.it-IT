---
keywords: Experience Platform ;ricetta di vendita al dettaglio;Data Science Workspace;argomenti popolari;ricette
solution: Experience Platform
title: Creare lo schema di vendita al dettaglio e il dataset
topic: tutorial
type: Tutorial
description: Questa esercitazione fornisce i prerequisiti e le risorse richiesti per tutte le altre esercitazioni di Adobe Experience Platform Data Science Workspace. Al termine, lo schema Vendite al dettaglio e i set di dati saranno disponibili per voi e per i membri dell'organizzazione IMS  Experience Platform.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Creare lo schema di vendita al dettaglio e il dataset

Questa esercitazione fornisce i prerequisiti e le risorse richiesti per tutte le altre esercitazioni [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Al termine, lo schema Vendite al dettaglio e i set di dati saranno disponibili per voi e per i membri dell&#39;organizzazione IMS su [!DNL Experience Platform].

## Introduzione

Prima di iniziare questa esercitazione, è necessario disporre dei seguenti prerequisiti:
- Accesso a [!DNL Adobe Experience Platform]. Se non disponete dell&#39;accesso a un&#39;organizzazione IMS in [!DNL Experience Platform], rivolgetevi all&#39;amministratore di sistema prima di procedere.
- Autorizzazione a effettuare chiamate API [!DNL Experience Platform]. Completate l&#39;esercitazione [Authenticate e accedete alle API Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) per ottenere i seguenti valori al fine di completare correttamente l&#39;esercitazione:
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Segreto cliente: `{CLIENT_SECRET}`
   - Certificato client: `{PRIVATE_KEY}`
- Dati di esempio e file di origine per la [Ricetta vendite al dettaglio](../pre-built-recipes/retail-sales.md). Scaricate le risorse necessarie per questa e altre [!DNL Data Science Workspace] esercitazioni dal [archivio pubblico  Adobe Git](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7 ](https://www.python.org/downloads/) e i seguenti  [!DNL Python] pacchetti:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Conoscenza approfondita dei seguenti concetti utilizzati in questa esercitazione:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Nozioni di base sulla composizione dello schema](../../xdm/schema/field-dictionary.md)

## Crea schema vendite al dettaglio e dataset

Lo schema Vendite al dettaglio e i set di dati vengono creati automaticamente utilizzando lo script di avvio fornito. Seguite i passaggi indicati di seguito nell&#39;ordine seguente:

### Configurare i file

1. All&#39;interno del pacchetto di risorse per l&#39;esercitazione [!DNL Experience Platform], andate alla directory `bootstrap` e aprite `config.yaml` utilizzando un editor di testo appropriato.
2. Nella sezione `Enterprise`, inserire i seguenti valori:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Modificate i valori trovati sotto la sezione `Platform`, Esempio riportato di seguito:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : Percorso di base per le chiamate API. Non modificate questo valore.
   - `ims_token` : La tua  `{ACCESS_TOKEN}` va qui.
   - `ingest_data` : Ai fini di questa esercitazione, impostare questo valore come  `"True"` per creare gli schemi di vendita al dettaglio e i set di dati. Il valore `"False"` crea solo gli schemi.
   - `build_recipe_artifacts` : Con questa esercitazione, impostare questo valore in modo  `"False"` da impedire che lo script generi un artefatto Recipe.
   - `kernel_type` : Il tipo di esecuzione dell&#39;artifact della ricetta. Lasciate questo valore come `Python` se `build_recipe_artifacts` è impostato come `"False"`, altrimenti specificate il tipo di esecuzione corretto.

4. Nella sezione `Titles`, fornite le seguenti informazioni appropriate per i dati di esempio Vendite al dettaglio, salvate e chiudete il file dopo che sono state apportate le modifiche. Esempio riportato di seguito:

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### Eseguire lo script bootstrap

1. Aprite l&#39;applicazione terminale e andate alla directory delle risorse di esercitazione [!DNL Experience Platform].
2. Impostate la directory `bootstrap` come percorso di lavoro corrente ed eseguite lo script `bootstrap.py` [!DNL Python] immettendo il comando seguente:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Il completamento dello script potrebbe richiedere alcuni minuti.

## Passaggi successivi

Al completamento dello script di avvio, gli schemi di input e output di Vendita al dettaglio e i set di dati possono essere visualizzati su [!DNL Experience Platform]. Vedere l&#39; [esercitazione sui dati dello schema di anteprima](./preview-schema-data.md)
per ulteriori informazioni.

È stato anche acquisito con successo i dati di esempio Vendite al dettaglio in [!DNL Experience Platform] utilizzando lo script di avvio fornito.

Per continuare a utilizzare i dati acquisiti:
- [Analizzare i dati utilizzando i notebook Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilizza i notebook Jupyter in Data Science Workspace per accedere, esplorare, visualizzare e comprendere i tuoi dati.
- [Creare pacchetti di file sorgente in una casella](./package-source-files-recipe.md)
   - Segui questa esercitazione per apprendere come portare il tuo modello in [!DNL Data Science Workspace] creando pacchetti di file sorgente in un file Recipe importabile.