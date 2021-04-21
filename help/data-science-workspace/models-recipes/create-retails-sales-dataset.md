---
keywords: Experience Platform;ricetta vendite al dettaglio;Data Science Workspace;argomenti popolari;ricette
solution: Experience Platform
title: Creare lo schema di vendita al dettaglio e il set di dati
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione fornisce i prerequisiti e le risorse necessari per tutte le altre esercitazioni di Adobe Experience Platform Data Science Workspace. Al termine, lo schema e i set di dati Vendite al dettaglio saranno disponibili per te e per i membri della tua organizzazione IMS all’Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Creare lo schema e il set di dati di vendita al dettaglio

Questa esercitazione fornisce i prerequisiti e le risorse necessari per tutte le altre esercitazioni [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] . Al termine, lo schema e i set di dati Vendite al dettaglio saranno disponibili per te e per i membri dell’organizzazione IMS su [!DNL Experience Platform].

## Introduzione

Prima di avviare questa esercitazione, è necessario disporre dei seguenti prerequisiti:
- Accesso a [!DNL Adobe Experience Platform]. Se non hai accesso a un&#39;organizzazione IMS in [!DNL Experience Platform], rivolgiti all&#39;amministratore di sistema prima di procedere.
- Autorizzazione a effettuare chiamate API [!DNL Experience Platform]. Completa il tutorial [Autentica e accedi alle API Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) per ottenere i seguenti valori al fine di completare correttamente questa esercitazione:
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Segreto client: `{CLIENT_SECRET}`
   - Certificato client: `{PRIVATE_KEY}`
- Dati di esempio e file di origine per la [Ricetta vendite al dettaglio](../pre-built-recipes/retail-sales.md). Scarica le risorse necessarie per questa e altre esercitazioni [!DNL Data Science Workspace] dall’ [archivio Git pubblico Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) e i seguenti  [!DNL Python] pacchetti:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dittatore](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Informazioni sui seguenti concetti utilizzati in questa esercitazione:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Nozioni di base sulla composizione dello schema](../../xdm/schema/field-dictionary.md)

## Creare schema e set di dati per vendite al dettaglio

Lo schema e i set di dati Vendite al dettaglio vengono creati automaticamente utilizzando lo script bootstrap fornito. Segui i passaggi riportati di seguito per ordinare:

### Configurare i file

1. All&#39;interno del pacchetto di risorse per l&#39;esercitazione [!DNL Experience Platform] , naviga nella directory `bootstrap` e apri `config.yaml` utilizzando un editor di testo appropriato.
2. Nella sezione `Enterprise` , inserisci i seguenti valori:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Modifica i valori trovati sotto la sezione `Platform`, Esempio mostrato di seguito:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : Percorso di base per le chiamate API. Non modificare questo valore.
   - `ims_token` : Il tuo  `{ACCESS_TOKEN}` va qui.
   - `ingest_data` : Ai fini di questa esercitazione, imposta questo valore come  `"True"` per creare gli schemi e i set di dati di vendita al dettaglio. Il valore `"False"` crea solo gli schemi.
   - `build_recipe_artifacts` : Ai fini di questa esercitazione, imposta questo valore  `"False"` per impedire che lo script generi un artefatto Ricetta.
   - `kernel_type` : Tipo di esecuzione dell&#39;artifact Ricetta. Lascia questo valore come `Python` se `build_recipe_artifacts` è impostato come `"False"`, altrimenti specifica il tipo di esecuzione corretto.

4. Nella sezione `Titles` , fornisci le seguenti informazioni in modo appropriato per i dati di esempio Vendite al dettaglio, salva e chiudi il file dopo aver apportato le modifiche. Esempio mostrato di seguito:

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

### Esegui lo script bootstrap

1. Apri l&#39;applicazione terminale e passa alla directory delle risorse di esercitazione [!DNL Experience Platform] .
2. Imposta la directory `bootstrap` come percorso di lavoro corrente ed esegui lo script `bootstrap.py` [!DNL Python] immettendo il seguente comando:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Il completamento dello script potrebbe richiedere alcuni minuti.

## Passaggi successivi

Al completamento dello script bootstrap, è possibile visualizzare gli schemi di input e output di Retail Sales e i set di dati su [!DNL Experience Platform]. Consulta l’ [esercitazione sui dati dello schema di anteprima](./preview-schema-data.md)
per ulteriori informazioni.

Hai anche acquisito i dati di esempio Vendite al dettaglio in [!DNL Experience Platform] utilizzando lo script di avvio fornito.

Per continuare a utilizzare i dati acquisiti:
- [Analizzare i dati utilizzando Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Utilizza i notebook Jupyter in Data Science Workspace per accedere, esplorare, visualizzare e comprendere i tuoi dati.
- [Creare pacchetti di file di origine in una composizione](./package-source-files-recipe.md)
   - Segui questa esercitazione per scoprire come portare il tuo modello in [!DNL Data Science Workspace] creando pacchetti di file sorgente in un file Ricetta importabile.
