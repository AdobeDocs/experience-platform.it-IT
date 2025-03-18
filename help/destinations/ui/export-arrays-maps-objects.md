---
title: Esportazione di array, mappe e oggetti da Real-Time CDP a destinazioni di archiviazione cloud
type: Tutorial
description: Scopri come esportare array, mappe e oggetti da Real-Time CDP a destinazioni di archiviazione cloud.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 99093e0bbcd3c3560ebe201fdac72e83e67dae43
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 16%

---

# Esportazione di array, mappe e oggetti da Real-Time CDP a destinazioni di archiviazione cloud {#export-arrays-cloud-storage}

>[!AVAILABILITY]
>
>La funzionalità per esportare array e altri oggetti complessi nelle destinazioni di archiviazione cloud è generalmente disponibile per le seguenti destinazioni: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md),

Scopri come esportare array, mappe e oggetti da Real-Time CDP in [destinazioni di archiviazione cloud](/help/destinations/catalog/cloud-storage/overview.md). Leggi questo documento per comprendere il flusso di lavoro di esportazione, i casi d’uso abilitati da questa funzionalità e le limitazioni note.

Considera questa pagina come il tuo punto di riferimento per tutto ciò che desideri sapere sull’esportazione di array, mappe e altri tipi di oggetti da Experience Platform.

## In basso in alto davanti

Ottieni le informazioni più importanti sulle funzionalità in questa sezione e continua di seguito con le altre sezioni del documento per informazioni dettagliate.

* La possibilità di esportare array, mappe e oggetti dipende dalla selezione dell&#39;interruttore **Esporta array, mappe, oggetti**. Ulteriori informazioni [più in basso nella pagina](#export-arrays-maps-objects-toggle).
* È possibile esportare array, mappe e oggetti solo nelle destinazioni di archiviazione cloud, in `JSON` e `Parquet` file. Sono supportati gli utenti e i potenziali tipi di pubblico, ma non i tipi di pubblico dell’account.
* *è possibile* esportare matrici, mappe e oggetti in file CSV, ma solo utilizzando la funzionalità dei campi calcolati e concatenandoli in una stringa utilizzando la funzione `array_to_string`.

## Array e altri tipi di oggetti in Platform {#arrays-strings-other-objects}

In Experience Platform puoi utilizzare [schemi XDM](/help/xdm/home.md) per gestire diversi tipi di campi. Prima di aggiungere il supporto per le esportazioni di array, era possibile esportare campi di tipo coppia chiave-valore semplici, come le stringhe, da Experience Platform nelle destinazioni desiderate. Un esempio di questo campo precedentemente supportato per l&#39;esportazione è `personalEmail.address`:`johndoe@acme.org`.

Altri tipi di campo in Experience Platform includono i campi array. Ulteriori informazioni sulla gestione dei campi array nell&#39;interfaccia utente di Experience Platform ](/help/xdm/ui/fields/array.md). [ È ora possibile esportare oggetti array come nell’esempio seguente.

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

Oltre agli array, puoi anche esportare mappe e oggetti da Experience Platform alla destinazione di archiviazione cloud desiderata. Ulteriori informazioni su [mappe](/help/xdm/ui/fields/map.md) e [oggetti](/help/xdm/ui/fields/object.md) in Experience Platform.

## Prerequisiti {#prerequisites}

[Connetti](/help/destinations/ui/connect-destination.md) a una destinazione di archiviazione cloud desiderata, segui i [passaggi di attivazione per le destinazioni di archiviazione cloud](/help/destinations/ui/activate-batch-profile-destinations.md) e procedi al passaggio [mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping). Quando ti connetti alla destinazione cloud desiderata, devi selezionare l&#39;opzione **[!UICONTROL Esporta array, mappe, oggetti]**. Per ulteriori informazioni, consulta la sezione seguente.

## Pulsante di attivazione per esportazione di array, mappe e oggetti {#export-arrays-maps-objects-toggle}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_maps_objects"
>title="Esportare array, mappe e oggetti"
>abstract="<p> <b>Attiva</b> questa impostazione per abilitare l’esportazione di array, mappe e oggetti in file JSON o Parquet. Puoi selezionare questi tipi di oggetto nella visualizzazione del campo di origine del passaggio della mappatura. Con l’impostazione attivata, non puoi utilizzare l’opzione dei campi calcolati nel passaggio di mappatura.</p><p>Con questa impostazione <b>disattivata</b>, puoi utilizzare l’opzione dei campi calcolati e applicare varie funzioni di trasformazione dei dati durante l’attivazione dei tipi di pubblico. Tuttavia, è possibile <i>non</i> esportare array, mappe e oggetti in file JSON o Parquet e, a tale scopo, è necessario configurare una destinazione separata.</p>"

Quando ti connetti a una destinazione di archiviazione cloud, puoi impostare l&#39;attivazione o la disattivazione di **[!UICONTROL Esporta array, mappe, oggetti]**.

![Esporta array, mappe, oggetti con un&#39;impostazione di attivazione o disattivazione ed evidenzia la finestra a comparsa.](/help/destinations/assets/ui/export-arrays-calculated-fields/export-objects-toggle.gif)

**Attiva** questa impostazione per abilitare l’esportazione di array, mappe e oggetti in file JSON o Parquet. È possibile selezionare questi tipi di oggetto nella visualizzazione del campo di origine del [passaggio di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) durante l&#39;attivazione dei tipi di pubblico nelle destinazioni dell&#39;archiviazione cloud. Tuttavia, con questa impostazione attivata, non è possibile utilizzare l’opzione dei campi calcolati per trasformare i dati all’attivazione.

Con questa impostazione **disattivata**, puoi utilizzare l’opzione dei campi calcolati e applicare varie funzioni di trasformazione dei dati durante l’attivazione dei tipi di pubblico. Tuttavia, non è possibile esportare array, mappe e oggetti in file JSON o Parquet e a tale scopo è necessario configurare una destinazione separata.

## Esporta array, mappe, oggetti *su* {#export-arrays-maps-objects-toggle-on}

Attivando questa impostazione, è possibile esportare interi oggetti (ad esempio `person.name`) e array selezionandoli tramite il selettore del campo di origine nel passaggio di mappatura del flusso di lavoro di attivazione.

![Selezionare gli oggetti tramite il selettore del campo di origine nel passaggio di mappatura del flusso di lavoro di attivazione.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-object.gif)

Selezionando questa opzione, l&#39;interfaccia utente blocca l&#39;utilizzo dei campi calcolati e il controllo **[!UICONTROL Aggiungi campi calcolati]** è disabilitato, come illustrato di seguito. Per utilizzare i campi calcolati per le trasformazioni di dati, imposta una connessione di destinazione con l’interruttore disattivato.

![Controllo campi calcolati disabilitato.](/help/destinations/assets/ui/export-arrays-calculated-fields/calculated-fields-disabled.png)

## Esporta array, mappe, oggetti *disattiva* {#export-arrays-maps-objects-toggle-off}

Con questa opzione impostata su *off*, puoi utilizzare l&#39;opzione dei campi calcolati e applicare varie funzioni di trasformazione dei dati durante l&#39;attivazione dei tipi di pubblico. Tuttavia, non è possibile esportare array, mappe e oggetti in file JSON o Parquet e a tale scopo è necessario configurare una destinazione separata.

È *possibile* esportare matrici, mappe e oggetti in file CSV utilizzando la funzionalità dei campi calcolati e concatenarli in una stringa utilizzando la funzione `array_to_string`. [Ulteriori informazioni](#array-to-string-function-export-arrays) sull&#39;utilizzo di tale funzione.

Ulteriori informazioni sull&#39;utilizzo dei campi calcolati per [eseguire trasformazioni sui dati esportati nelle destinazioni dell&#39;archiviazione cloud](/help/destinations/ui/data-transformations-calculated-fields.md).

## File esportati di esempio {#sample-exported-files}

Utilizzando questa funzionalità, puoi esportare i file Parquet e JSON in cui i dati mantengono la struttura da Experience Platform. Visualizza di seguito un esempio di file JSON esportato.

+++ Seleziona per visualizzare il file JSON esportato.

```json
{
  "person_name_firstName": "John",
  "person_name_lastName": "Smith",
  "_acmeinc_customer_hs_main_address_scalar": "Oak Avenue No 12",
  "_acmeinc_customer_hs_locations_array": [
    "home address 12",
    "office address 12"
  ],
  "_acmeinc_customer_hs_date_array": [
    "2024-11-14",
    "2024-11-15"
  ],
  "_acmeinc_customer_hs_customer_obj_emails_array0": "john.smith@example.com",
  "_acmeinc_customer_hs_customer_obj": {
    "emails_array": [
      "john.smith@example.com",
      "j.smith@example.com"
    ],
    "name_scalar": "John Smith"
  },
  "_acmeinc_customer_hs_addresses_array_obj": [
    {
      "is_primary": true,
      "streetName_scalar": "Maple Street",
      "streetNo_int": 12
    },
    {
      "is_primary": false,
      "streetName_scalar": "Pine Road",
      "streetNo_int": 45
    }
  ],
  "_acmeinc_customer_hs_addresses_array_obj0": {
    "is_primary": true,
    "streetName_scalar": "Maple Street",
    "streetNo_int": 12
  }
}
```

+++