---
keywords: Experience Platform; ricetta di vendita al dettaglio; Data Science Area di lavoro; argomenti popolari; Ricette
solution: Experience Platform
title: Crea lo schema e il set di dati delle vendite al dettaglio
type: Tutorial
description: In questo esercitazione vengono forniti i prerequisiti e le risorse necessari per tutte le altre esercitazioni di Adobe Experience Platform Data Science Area di lavoro. Al termine, lo schema e i set di dati delle vendite al dettaglio saranno disponibili per te e per i membri della tua organizzazione in Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---


# Creare lo schema e il set di dati di vendita al dettaglio

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

Questo tutorial ti fornisce i prerequisiti e le risorse necessari per tutte le altre esercitazioni di [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Al termine, lo schema e i set di dati delle vendite al dettaglio saranno disponibili per te e per i membri della tua organizzazione il [!DNL Experience Platform].

## Introduzione

Prima di iniziare questa esercitazione, è necessario disporre dei seguenti prerequisiti:
- Accesso a [!DNL Adobe Experience Platform]. Se non si dispone dell&#39;accesso a un&#39;organizzazione in [!DNL Experience Platform], contattare l&#39;amministratore di sistema prima di procedere.
- Autorizzazione ad effettuare [!DNL Experience Platform] chiamate API. Completa l&#39;esercitazione [Autentica e accedi alle API di Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) per ottenere i seguenti valori al fine di completare questa esercitazione:
   - Autorizzazione: `{ACCESS_TOKEN}`
   - X-API-Key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Segreto client: `{CLIENT_SECRET}`
   - Certificato client: `{PRIVATE_KEY}`
- Dati di esempio e file di origine per la ricetta](../pre-built-recipes/retail-sales.md) delle [vendite al dettaglio. Scarica le risorse necessarie per questa e altre [!DNL Data Science Workspace] esercitazioni dal [Adobe Systems pubblico Git archivio](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) e i seguenti [!DNL Python] pacchetti:
   - [stelletta](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dittatore](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Una comprensione operativa dei seguenti concetti utilizzati in questo esercitazione:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Nozioni di base sulla composizione dello schema](../../xdm/schema/field-dictionary.md)

## Crea schema e set di dati di vendita al dettaglio

Lo schema delle vendite al dettaglio e i set di dati vengono creati automaticamente tramite lo script di bootstrap fornito. Segui i passaggi riportati di seguito nell&#39;ordine indicato:

### Configurare i file

1. All&#39;interno del [!DNL Experience Platform] pacchetto di risorse esercitazione, passare alla directory `bootstrap`e aprire `config.yaml` utilizzando un editor di testo appropriato.
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
   - `build_recipe_artifacts`: ai fini di questo esercitazione, imposta questo valore in modo da `"False"` impedire allo script di generare un artefatto della ricetta.
   - `kernel_type`: tipo di esecuzione dell&#39;artefatto Ricetta. Lasciare questo valore come `Python` se `build_recipe_artifacts` fosse impostato come `"False"`, altrimenti specificare il tipo di esecuzione corretto.

4. `Titles` Nella sezione, fornire le seguenti informazioni in modo appropriato per i dati di esempio delle vendite al dettaglio, salvare e chiudere il file dopo che le modifiche sono state inserite. Esempio mostrato di seguito:

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

### Eseguire lo script di bootstrap

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
   - Segui questa esercitazione per scoprire come inserire il tuo modello confezionando [!DNL Data Science Workspace] i file sorgente in un file di ricette importabile.
