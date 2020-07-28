---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Creare lo schema di vendita al dettaglio e il dataset
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Creare lo schema di vendita al dettaglio e il dataset

Questa esercitazione fornisce i prerequisiti e le risorse richiesti per tutte le altre [!DNL Adobe Experience Platform][!DNL Data Science Workspace] esercitazioni. Al termine, lo schema Vendite al dettaglio e i set di dati saranno disponibili per voi e per i membri dell&#39;organizzazione IMS in [!DNL Experience Platform].

## Introduzione

Prima di iniziare questa esercitazione, è necessario disporre dei seguenti prerequisiti:
- Accesso a [!DNL Adobe Experience Platform]. Se non disponete dell&#39;accesso a un&#39;organizzazione IMS in [!DNL Experience Platform], rivolgetevi all&#39;amministratore di sistema prima di procedere.
- Autorizzazione per effettuare chiamate [!DNL Experience Platform] API. Completate l&#39;esercitazione [Authenticate e accedete  API](../../tutorials/authentication.md) Adobe Experience Platform per ottenere i seguenti valori al fine di completare con successo l&#39;esercitazione:
   - Autorizzazione: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Segreto cliente: `{CLIENT_SECRET}`
   - Certificato client: `{PRIVATE_KEY}`
- Dati di esempio e file sorgente per la Ricetta vendite [al dettaglio](../pre-built-recipes/retail-sales.md). Scaricate le risorse necessarie per questa e altre [!DNL Data Science Workspace] esercitazioni dall’archivio [Git pubblico del Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) e i seguenti [!DNL Python] pacchetti:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Conoscenza approfondita dei seguenti concetti utilizzati in questa esercitazione:
   - [!DNL Experience Data Model (XDM)](../../xdm/home.md)
   - [Nozioni di base sulla composizione dello schema](../../xdm/schema/field-dictionary.md)

## Crea schema vendite al dettaglio e dataset

Lo schema Vendite al dettaglio e i set di dati vengono creati automaticamente utilizzando lo script di avvio fornito. Seguite i passaggi indicati di seguito nell&#39;ordine seguente:

### Configurare i file

1. All’interno del pacchetto di risorse per l’ [!DNL Experience Platform] esercitazione, andate alla directory `bootstrap`e aprite `config.yaml` utilizzando un editor di testo appropriato.
2. Nella sezione `Enterprise` immettere i seguenti valori:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Modificate i valori trovati sotto la `Platform` sezione, Esempio riportato di seguito:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : Percorso di base per le chiamate API. Non modificate questo valore.
   - `ims_token` : La tua `{ACCESS_TOKEN}` va qui.
   - `ingest_data` : Ai fini di questa esercitazione, impostare questo valore come `"True"` per creare gli schemi di vendita al dettaglio e i set di dati. Un valore di `"False"` verrà creato solo per gli schemi.
   - `build_recipe_artifacts` : Con questa esercitazione, impostare questo valore in modo `"False"` da impedire che lo script generi un artefatto Recipe.
   - `kernel_type` : Il tipo di esecuzione dell&#39;artifact della ricetta. Lasciate questo valore come `Python` se `build_recipe_artifacts` fosse impostato come `"False"`, altrimenti specificate il tipo di esecuzione corretto.

4. Nella sezione `Titles` , fornite le seguenti informazioni appropriate per i dati di esempio Vendite al dettaglio, salvate e chiudete il file dopo aver apportato le modifiche. Esempio riportato di seguito:

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

1. Aprite l’applicazione terminale e accedete alla directory delle risorse di [!DNL Experience Platform] esercitazione.
2. Impostate la `bootstrap` directory come percorso di lavoro corrente ed eseguite lo `bootstrap.py` [!DNL Python] script immettendo il seguente comando:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE] Il completamento dello script potrebbe richiedere alcuni minuti.

## Passaggi successivi

Al completamento dello script di avvio, è possibile visualizzare gli schemi di input e output di Vendita al dettaglio e i set di dati [!DNL Experience Platform]. Per ulteriori informazioni, vedere l&#39;esercitazione [sullo schema di](./preview-schema-data.md)anteprima.

Sono stati inoltre acquisiti con successo i dati di esempio Vendite al dettaglio [!DNL Experience Platform] utilizzando lo script di avvio fornito.

Per continuare a utilizzare i dati acquisiti:
- [Analizzare i dati utilizzando i notebook Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilizza i notebook Jupyter in Data Science Workspace per accedere, esplorare, visualizzare e comprendere i tuoi dati.
- [Creare pacchetti di file sorgente in una composizione](./package-source-files-recipe.md)
   - Segui questa esercitazione per scoprire come inserire un modello personalizzato [!DNL Data Science Workspace] creando pacchetti di file sorgente in un file Recipe importabile.