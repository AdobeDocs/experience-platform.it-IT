---
keywords: Experience Platform;vendita al dettaglio ricetta;Data Science Workspace;argomenti popolari;ricette
solution: Experience Platform
title: Creare lo schema e il set di dati di vendita al dettaglio
type: Tutorial
description: Questa esercitazione ti fornisce i prerequisiti e le risorse necessari per tutte le altre esercitazioni di Adobe Experience Platform Data Science Workspace. Al termine, lo schema e i set di dati di vendita al dettaglio saranno disponibili per te e per i membri della tua organizzazione a Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 2%

---


# Creare lo schema e il set di dati di vendita al dettaglio

Questo tutorial ti fornisce i prerequisiti e le risorse necessari per tutte le altre esercitazioni di [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Al termine, lo schema e i set di dati di vendita al dettaglio saranno disponibili per te e per i membri della tua organizzazione il [!DNL Experience Platform].

## Introduzione

Prima di avviare questa esercitazione, è necessario disporre dei seguenti prerequisiti:
- Accesso a [!DNL Adobe Experience Platform]. Se non si dispone dell&#39;accesso a un&#39;organizzazione in [!DNL Experience Platform], contattare l&#39;amministratore di sistema prima di procedere.
- Autorizzazione ad effettuare [!DNL Experience Platform] chiamate API. Completa l&#39;esercitazione [Autentica e accedi alle API di Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) per ottenere i seguenti valori al fine di completare questa esercitazione:
   - Autorizzazione: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Segreto client: `{CLIENT_SECRET}`
   - Certificato client: `{PRIVATE_KEY}`
- Dati di esempio e file di origine per [Ricetta vendite al dettaglio](../pre-built-recipes/retail-sales.md). Scarica le risorse necessarie per questa e altre esercitazioni di [!DNL Data Science Workspace] dall&#39;[archivio Git pubblico di Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) e i seguenti [!DNL Python] pacchetti:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Una buona conoscenza dei seguenti concetti utilizzati in questa esercitazione:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Nozioni di base sulla composizione dello schema](../../xdm/schema/field-dictionary.md)

## Crea schema e set di dati di vendita al dettaglio

Lo schema e i set di dati di vendita al dettaglio vengono creati automaticamente utilizzando lo script di avvio fornito. Segui i passaggi seguenti nell’ordine:

### Configurare i file

1. All&#39;interno del pacchetto di risorse dell&#39;esercitazione [!DNL Experience Platform], passare alla directory `bootstrap` e aprire `config.yaml` utilizzando un editor di testo appropriato.
2. Nella sezione `Enterprise` immettere i valori seguenti:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Modifica i valori trovati nella sezione `Platform`, come mostrato di seguito:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: percorso di base per le chiamate API. Non modificare questo valore.
   - `ims_token`: `{ACCESS_TOKEN}` viene reindirizzato qui.
   - `ingest_data`: ai fini di questa esercitazione, imposta questo valore come `"True"` per creare schemi e set di dati di vendita al dettaglio. Un valore di `"False"` creerà solo gli schemi.
   - `build_recipe_artifacts`: ai fini di questa esercitazione, impostare questo valore come `"False"` per impedire che lo script generi un artefatto di ricetta.
   - `kernel_type`: tipo di esecuzione dell&#39;artefatto della ricetta. Lasciare questo valore come `Python` se `build_recipe_artifacts` è impostato come `"False"`, altrimenti specificare il tipo di esecuzione corretto.

4. Nella sezione `Titles`, fornisci le seguenti informazioni in modo appropriato per i dati di esempio di vendita al dettaglio, salva e chiudi il file dopo le modifiche. Esempio mostrato di seguito:

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

### Eseguire lo script di avvio automatico

1. Aprire l&#39;applicazione terminal e passare alla directory delle risorse dell&#39;esercitazione [!DNL Experience Platform].
2. Impostare la directory `bootstrap` come percorso di lavoro corrente ed eseguire lo script `bootstrap.py` [!DNL Python] immettendo il comando seguente:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Lo script potrebbe richiedere alcuni minuti.

## Passaggi successivi

Al completamento dello script di avvio, gli schemi e i set di dati di input e output per la vendita al dettaglio possono essere visualizzati il [!DNL Experience Platform]. Guarda l&#39;esercitazione [anteprima dati schema](./preview-schema-data.md)
per ulteriori informazioni.

Sono stati inoltre acquisiti i dati di esempio di Retail Sales in [!DNL Experience Platform] utilizzando lo script di avvio fornito.

Per continuare a lavorare con i dati acquisiti:
- [Analizza i tuoi dati utilizzando Jupyter Notebook](../jupyterlab/analyze-your-data.md)
   - Utilizza Jupyter Notebooks in Data Science Workspace per accedere, esplorare, visualizzare e comprendere i tuoi dati.
- [Creare pacchetti di file di origine in una ricetta](./package-source-files-recipe.md)
   - Segui questa esercitazione per scoprire come inserire il tuo modello in [!DNL Data Science Workspace] creando un pacchetto dei file di origine in un file di ricetta importabile.
