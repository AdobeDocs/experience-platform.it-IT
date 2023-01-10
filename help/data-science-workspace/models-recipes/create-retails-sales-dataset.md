---
keywords: Experience Platform;ricetta vendite al dettaglio;Data Science Workspace;argomenti popolari;ricette
solution: Experience Platform
title: Creare lo schema di vendita al dettaglio e il set di dati
type: Tutorial
description: Questa esercitazione fornisce i prerequisiti e le risorse necessari per tutte le altre esercitazioni di Adobe Experience Platform Data Science Workspace. Al termine, lo schema e i set di dati Vendite al dettaglio saranno disponibili per te e per i membri della tua organizzazione IMS all’Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---


# Creare lo schema e il set di dati di vendita al dettaglio

Questa esercitazione fornisce i prerequisiti e le risorse necessari per tutti gli altri [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] esercitazioni. Al termine, lo schema e i set di dati Vendite al dettaglio saranno disponibili per te e per i membri dell’organizzazione IMS su [!DNL Experience Platform].

## Introduzione

Prima di avviare questa esercitazione, è necessario disporre dei seguenti prerequisiti:
- Accesso a [!DNL Adobe Experience Platform]. Se non hai accesso a un’organizzazione IMS in [!DNL Experience Platform]Prima di procedere, rivolgiti all’amministratore di sistema.
- Autorizzazione a effettuare [!DNL Experience Platform] Chiamate API. Completa il [Autenticazione e accesso alle API Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) per ottenere i seguenti valori al fine di completare correttamente questa esercitazione:
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Segreto client: `{CLIENT_SECRET}`
   - Certificato client: `{PRIVATE_KEY}`
- File di dati di esempio e di origine per [Ricetta vendite al dettaglio](../pre-built-recipes/retail-sales.md). Scarica le risorse necessarie per questo e altri [!DNL Data Science Workspace] esercitazioni dal [Archivio Git pubblico Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2,7](https://www.python.org/downloads/) e quanto segue [!DNL Python] imballaggi:
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

1. Dentro [!DNL Experience Platform] pacchetto di risorse tutorial, accedi alla directory `bootstrap`e apri `config.yaml` utilizzando un editor di testo appropriato.
2. Sotto la `Enterprise` inserire i seguenti valori:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Modifica i valori trovati sotto la `Platform` sezione, Esempio mostrato di seguito:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: Percorso di base per le chiamate API. Non modificare questo valore.
   - `ims_token`: Le `{ACCESS_TOKEN}` vai qui.
   - `ingest_data`: Ai fini di questa esercitazione, imposta questo valore come `"True"` per creare gli schemi e i set di dati di vendita al dettaglio. Un valore di `"False"` crea solo gli schemi.
   - `build_recipe_artifacts`: Ai fini di questa esercitazione, imposta questo valore come `"False"` per impedire che lo script generi un artefatto Ricetta.
   - `kernel_type`: Tipo di esecuzione dell&#39;artifact Ricetta. Lascia questo valore come `Python` if `build_recipe_artifacts` è impostato come `"False"`in caso contrario, specifica il tipo di esecuzione corretto.

4. Sotto la `Titles` fornisci le seguenti informazioni in modo appropriato per i dati di esempio Vendite al dettaglio, salva e chiudi il file dopo aver apportato le modifiche. Esempio mostrato di seguito:

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

1. Apri l&#39;applicazione terminale e passa alla [!DNL Experience Platform] directory delle risorse di esercitazione.
2. Imposta la `bootstrap` come percorso di lavoro corrente ed esegui il `bootstrap.py` [!DNL Python] inserendo il comando seguente:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Il completamento dello script potrebbe richiedere alcuni minuti.

## Passaggi successivi

Al completamento dello script bootstrap, è possibile visualizzare gli schemi di input e output di Retail Sales e i set di dati su [!DNL Experience Platform]. Consulta la sezione [esercitazione sui dati dello schema di anteprima](./preview-schema-data.md)
per ulteriori informazioni.

Inoltre, hai acquisito correttamente i dati di esempio per le vendite al dettaglio in [!DNL Experience Platform] utilizzando lo script bootstrap fornito.

Per continuare a utilizzare i dati acquisiti:
- [Analizzare i dati utilizzando Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Utilizza i notebook Jupyter in Data Science Workspace per accedere, esplorare, visualizzare e comprendere i tuoi dati.
- [Creare pacchetti di file di origine in una composizione](./package-source-files-recipe.md)
   - Segui questa esercitazione per scoprire come inserire il tuo modello in [!DNL Data Science Workspace] impacchettando i file di origine in un file di composizione importabile.
