---
keywords: Experience Platform;vendita al dettaglio ricetta;Data Science Workspace;argomenti popolari;ricette
solution: Experience Platform
title: Creare lo schema e il set di dati di vendita al dettaglio
type: Tutorial
description: Questa esercitazione ti fornisce i prerequisiti e le risorse necessari per tutte le altre esercitazioni di Adobe Experience Platform Data Science Workspace. Al termine, lo schema e i set di dati di vendita al dettaglio saranno disponibili, a Experience Platform, per te e per i membri della tua organizzazione IMS.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---


# Creare lo schema e il set di dati di vendita al dettaglio

Questa esercitazione ti fornisce i prerequisiti e le risorse necessari per tutte le altre [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] esercitazioni. Al termine, lo schema e i set di dati di vendita al dettaglio saranno disponibili per te e per i membri della tua organizzazione IMS il [!DNL Experience Platform].

## Introduzione

Prima di avviare questa esercitazione, è necessario disporre dei seguenti prerequisiti:
- Accesso a [!DNL Adobe Experience Platform]. Se non hai accesso a un’organizzazione IMS in [!DNL Experience Platform], contattare l&#39;amministratore di sistema prima di procedere.
- Autorizzazione ad effettuare [!DNL Experience Platform] Chiamate API. Completa il [Autenticazione e accesso alle API di Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) esercitazione per ottenere i seguenti valori per completare correttamente questa esercitazione:
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Segreto client: `{CLIENT_SECRET}`
   - Certificato client: `{PRIVATE_KEY}`
- Dati di esempio e file di origine per [Ricetta vendita al dettaglio](../pre-built-recipes/retail-sales.md). Scarica le risorse necessarie per questo e altri [!DNL Data Science Workspace] tutorial da [Adobe archivio Git pubblico](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2,7](https://www.python.org/downloads/) e i seguenti [!DNL Python] pacchetti:
   - [pip](https://pypi.org/project/pip/)
   - [YAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Una buona conoscenza dei seguenti concetti utilizzati in questa esercitazione:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Nozioni di base sulla composizione dello schema](../../xdm/schema/field-dictionary.md)

## Crea schema e set di dati di vendita al dettaglio

Lo schema e i set di dati di vendita al dettaglio vengono creati automaticamente utilizzando lo script di avvio fornito. Segui i passaggi seguenti nell’ordine:

### Configurare i file

1. All&#39;interno del [!DNL Experience Platform] pacchetto di risorse tutorial, passa alla directory `bootstrap`, e aperto `config.yaml` utilizzando un editor di testo appropriato.
2. Sotto `Enterprise` , immetti i seguenti valori:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Modifica i valori trovati sotto `Platform` sezione, Esempio mostrato di seguito:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: percorso di base per le chiamate API. Non modificare questo valore.
   - `ims_token`: il tuo `{ACCESS_TOKEN}` va qui.
   - `ingest_data`: ai fini della presente esercitazione, imposta questo valore come `"True"` per creare schemi e set di dati di vendita al dettaglio. Un valore di `"False"` crea solo gli schemi.
   - `build_recipe_artifacts`: ai fini della presente esercitazione, imposta questo valore come `"False"` per impedire che lo script generi un artefatto di ricetta.
   - `kernel_type`: tipo di esecuzione dell’artefatto della ricetta. Lascia questo valore come `Python` se `build_recipe_artifacts` è impostato come `"False"`, altrimenti specifica il tipo di esecuzione corretto.

4. Sotto `Titles` , fornire le seguenti informazioni in modo appropriato per i dati di esempio di vendita al dettaglio, salvare e chiudere il file dopo le modifiche. Esempio mostrato di seguito:

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

1. Apri l’applicazione terminale e passa alla [!DNL Experience Platform] directory delle risorse del tutorial.
2. Imposta il `bootstrap` come percorso di lavoro corrente ed esegui la `bootstrap.py` [!DNL Python] immettendo il comando seguente:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Lo script potrebbe richiedere alcuni minuti.

## Passaggi successivi

Una volta completato con successo lo script di avvio, gli schemi e i set di dati di input e output per la vendita al dettaglio possono essere visualizzati su [!DNL Experience Platform]. Consulta la [tutorial sull’anteprima dei dati dello schema](./preview-schema-data.md)
per ulteriori informazioni.

Inoltre, hai acquisito correttamente i dati di esempio delle vendite al dettaglio in [!DNL Experience Platform] utilizzando lo script bootstrap fornito.

Per continuare a lavorare con i dati acquisiti:
- [Analizzare i dati utilizzando Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Utilizza Jupyter Notebooks in Data Science Workspace per accedere ai tuoi dati, esplorarli, visualizzarli e comprenderli.
- [Creare pacchetti di file di origine in una ricetta](./package-source-files-recipe.md)
   - Segui questa esercitazione per scoprire come inserire un modello personalizzato in [!DNL Data Science Workspace] creando pacchetti di file di origine in un file di composizione importabile.
