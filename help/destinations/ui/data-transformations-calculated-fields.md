---
title: Eseguire trasformazioni sui dati esportati nelle destinazioni di archiviazione cloud utilizzando campi calcolati
type: Tutorial
description: Scopri come utilizzare la funzionalità dei campi calcolati per eseguire trasformazioni sui dati esportati nelle destinazioni dell’archiviazione cloud
source-git-commit: 6122ddc078101c26061e8662de3fcdcb1cb65992
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 3%

---

# Eseguire trasformazioni sui dati esportati nelle destinazioni di archiviazione cloud utilizzando campi calcolati {#data-transformation-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Aggiungere campi calcolati"
>abstract="<p>Utilizza il controllo **Aggiungi campo calcolato** per eseguire varie trasformazioni di dati sui dati esportati nelle destinazioni dell&#39;archiviazione cloud. Ad esempio, puoi applicare l’hashing ai dati, concatenare gli array in stringhe e altro ancora."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=it#examples" text="Esempi"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=it#known-limitations" text="Limitazioni note"

>[!AVAILABILITY]
>
>La funzionalità per eseguire trasformazioni sui dati esportati nelle destinazioni di archiviazione cloud è generalmente disponibile per le seguenti destinazioni: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md), nonché per tutte le destinazioni di archiviazione cloud personalizzate create tramite [Destination SDK](/help/destinations/destination-sdk/overview.md) e create dai partner.

Per eseguire varie trasformazioni sui dati esportati nelle destinazioni di archiviazione cloud, devi utilizzare la funzionalità dei campi calcolati nel passaggio di mappatura del flusso di lavoro di esportazione. Per informazioni dettagliate sui campi calcolati, visita le pagine collegate di seguito. Queste pagine includono un’introduzione ai campi calcolati nella preparazione dati e ulteriori informazioni su tutte le funzioni disponibili:

* [Guida e panoramica dell’interfaccia utente](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funzioni di preparazione dati](/help/data-prep/functions.md)

## Prerequisiti {#prerequisites}

Per utilizzare i campi calcolati per le trasformazioni dei dati:

1. [Connetti](/help/destinations/ui/connect-destination.md) a una destinazione di archiviazione cloud desiderata. Quando ci si connette alla destinazione cloud desiderata, disattivare **[!UICONTROL Esporta array, mappe, oggetti]** [opzione](/help/destinations/ui/export-arrays-calculated-fields.md##export-arrays-maps-objects-toggle).
2. Segui i [passaggi di attivazione per le destinazioni dell&#39;archiviazione cloud](/help/destinations/ui/activate-batch-profile-destinations.md) e passa al passaggio [mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Utilizzare i campi calcolati {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Abilitare lo schema di output gerarchico"
>abstract="Attiva questa impostazione per abilitare l’esportazione di array, mappe e oggetti in file JSON o Parquet."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="Aggiungere campi calcolati disabilitati"
>abstract="Questo controllo è disabilitato, perché durante la configurazione della connessione di destinazione hai selezionato **Esporta array, mappe, oggetti** su *Attivato*. Per utilizzare i campi calcolati e le funzioni disponibili all’interno, imposta una nuova connessione di destinazione con l’opzione **Esporta array, mappe, oggetti** su *Disattivato*."

Nel passaggio di mappatura del flusso di lavoro di attivazione per le destinazioni di archiviazione cloud, seleziona **[!UICONTROL Aggiungi campo calcolato]**.

>[!TIP]
>
>Il controllo **[!UICONTROL Aggiungi campo calcolato]** è disabilitato per le connessioni di destinazione in cui il controllo **[!UICONTROL Esporta matrici, mappe e oggetti]** è stato disattivato. [Ulteriori informazioni](/help/destinations/ui/export-arrays-calculated-fields.md#export-arrays-maps-objects-toggle).

![Aggiungi campo calcolato evidenziato nel passaggio di mappatura del flusso di lavoro di attivazione batch.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Viene visualizzata una finestra modale in cui è possibile selezionare funzioni e campi per esportare gli attributi da Experience Platform.

![Finestra modale della funzionalità del campo calcolato senza alcuna funzione ancora selezionata.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Ad esempio, utilizza la funzione `array_to_string` nel campo `organizations` come mostrato di seguito per esportare l&#39;array organization come stringa in un file CSV. Visualizza [ulteriori informazioni su questo e altri esempi più avanti](#array-to-string-function-export-arrays).

![Finestra modale della funzionalità del campo calcolato con la funzione array-to-string selezionata.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Seleziona **[!UICONTROL Salva]** per mantenere il campo calcolato e tornare al passaggio di mappatura.

![Finestra modale della funzionalità del campo calcolato con la funzione matrice-stringa selezionata ed il controllo Salva evidenziato.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Tornando al passaggio di mappatura del flusso di lavoro, compila il **[!UICONTROL campo di destinazione]** con il valore dell&#39;intestazione di colonna desiderata per questo campo nei file esportati.

![Passaggio di mapping con il campo di destinazione evidenziato.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Seleziona campo di destinazione 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Al termine, seleziona **[!UICONTROL Avanti]** per procedere al passaggio successivo del flusso di lavoro di attivazione.

![Passaggio di mappatura con il campo di destinazione evidenziato e un valore di destinazione compilato.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Esempi di funzioni supportate per eseguire le trasformazioni dei dati {#supported-functions}

Tutte le [funzioni di preparazione dati](/help/data-prep/functions.md) documentate sono supportate quando si attivano i dati in destinazioni basate su file.

Le funzioni seguenti, specifiche per la gestione delle esportazioni di array o l’applicazione di hashing ai campi, sono documentate insieme ad esempi.

* `array_to_string`
* `flattenArray`
* `filterArray`
* `transformArray`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`

## Esempi di funzioni utilizzate per eseguire le trasformazioni dei dati {#examples}

Consulta gli esempi e ulteriori informazioni nelle sezioni seguenti per alcune delle funzioni elencate in precedenza. Per le altre funzioni elencate, consulta la [documentazione sulle funzioni generali nella sezione Preparazione dati](/help/data-prep/functions.md).

### Funzione `array_to_string` per esportare array {#array-to-string-function-export-arrays}

Utilizzare la funzione `array_to_string` per concatenare gli elementi di un array in una stringa utilizzando un separatore desiderato, ad esempio `_` o `|`. Questa funzione è utile quando si desidera esportare gli elementi di un array da Experience Platform in un file CSV.

Ad esempio, puoi combinare i seguenti campi XDM come mostrato nella schermata di mappatura utilizzando una sintassi `array_to_string('_',organizations)`:

* Array `organizations`
* `person.name.firstName` stringa
* `person.name.lastName` stringa
* `personalEmail.address` stringa

![Esempio di mapping che include la funzione array_to_string.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

In questo caso, il file di output si presenta come di seguito. Gli elementi dell&#39;array vengono concatenati in una singola stringa utilizzando il carattere `_`.

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### Funzione `filterArray` per esportare array filtrati {#filter-array}

Utilizzare la funzione `filterArray` per filtrare gli elementi di un array esportato. È possibile combinare questa funzione con la funzione `array_to_string` descritta in precedenza.

Continuando con l&#39;oggetto array `organizations` dall&#39;alto, è possibile scrivere una funzione come `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`, che restituisce le organizzazioni con un valore per `founded` nell&#39;anno 2021 o più recente.

![Esempio della funzione filterArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

In questo caso, il file di output si presenta come di seguito. I due elementi dell&#39;array che soddisfano il criterio vengono concatenati in una singola stringa utilizzando il carattere `_`.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### Funzione `transformArray` per esportare array trasformati {#transform-array}

Utilizzare la funzione `transformArray` per trasformare gli elementi di un array esportato. È possibile combinare questa funzione con la funzione `array_to_string` descritta in precedenza.

Continuando con l&#39;oggetto array `organizations` dall&#39;alto, è possibile scrivere una funzione come `array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))`, restituendo i nomi delle organizzazioni convertite in lettere maiuscole.

![Esempio della funzione transformArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

In questo caso, il file di output si presenta come di seguito. I tre elementi dell&#39;array vengono trasformati e concatenati in una singola stringa utilizzando il carattere `_`.

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### Funzione `iif` per esportare array {#iif-function-export-arrays}

Utilizzare la funzione `iif` per esportare gli elementi di un array in determinate condizioni. Ad esempio, continuando con l&#39;oggetto array `organizations` dall&#39;alto, è possibile scrivere una funzione condizionale semplice come `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Esempio di mapping che include la funzione iif.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

In questo caso, il file di output si presenta come di seguito. In questo caso, il primo elemento dell’array è Marketing, quindi la persona è membro del reparto marketing.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### Funzione `add_to_array` per esportare array {#add-to-array-function-export-arrays}

Utilizzare la funzione `add_to_array` per aggiungere elementi a un array esportato. È possibile combinare questa funzione con la funzione `array_to_string` descritta in precedenza.

Continuando con l&#39;oggetto array `organizations` dall&#39;alto, è possibile scrivere una funzione come `source: array_to_string('_', add_to_array(organizations,"2023"))`, restituendo le organizzazioni di cui una persona è membro nel 2023.

![Esempio di mapping che include la funzione add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

In questo caso, il file di output si presenta come di seguito. Nota come i tre elementi dell’array sono concatenati in una singola stringa utilizzando il carattere `_` e 2023 viene aggiunto alla fine della stringa.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### Funzione `flattenArray` per esportare array appiattiti {#flatten-array}

Utilizzare la funzione `flattenArray` per appiattire una matrice multidimensionale esportata. È possibile combinare questa funzione con la funzione `array_to_string` descritta in precedenza.

Continuando con l&#39;oggetto array `organizations` dall&#39;alto, è possibile scrivere una funzione come `array_to_string('_', flattenArray(organizations))`. La funzione `array_to_string` appiattisce l&#39;array di input per impostazione predefinita in una stringa.

L&#39;output risultante è lo stesso della funzione `array_to_string` descritta più sopra.

### Funzione `coalesce` per esportare array {#coalesce-function-export-arrays}

Utilizzare la funzione `coalesce` per accedere ed esportare il primo elemento non Null di un array in una stringa.

Ad esempio, puoi combinare i seguenti campi XDM come mostrato nella schermata di mappatura utilizzando una sintassi `coalesce(subscriptions.hasPromotion)` per restituire il primo `true` del valore `false` nell&#39;array:

* Array `"subscriptions.hasPromotion": [null, true, null, false, true]`
* `person.name.firstName` stringa
* `person.name.lastName` stringa
* `personalEmail.address` stringa

![Esempio di mapping che include la funzione coalesce.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

In questo caso, il file di output si presenta come di seguito. Il primo valore `true` non nullo nell&#39;array viene esportato nel file.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### Funzione `size_of` per esportare array {#sizeof-function-export-arrays}

Utilizzare la funzione `size_of` per indicare quanti elementi esistono in un array. Ad esempio, se si dispone di un oggetto array `purchaseTime` con più marche temporali, è possibile utilizzare la funzione `size_of` per indicare quanti acquisti separati sono stati effettuati da una persona.

Ad esempio, puoi combinare i seguenti campi XDM come mostrato nella schermata di mappatura.

* Array `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` che indica cinque tempi di acquisto separati per il cliente
* `personalEmail.address` stringa

![Esempio di mapping che include la funzione size_of.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In questo caso, il file di output si presenta come di seguito. Osserva come la seconda colonna indica il numero di elementi nell’array, corrispondente al numero di acquisti separati effettuati dal cliente.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Accesso all&#39;array basato su indice {#index-based-array-access}

>[!IMPORTANT]
>
>A differenza delle altre funzioni descritte in questa pagina, per esportare singoli elementi di un array non è necessario ** per utilizzare il controllo **[!UICONTROL Campi calcolati]** nell&#39;interfaccia utente.

È possibile accedere a un indice di un array per esportare un singolo elemento dall’array. Ad esempio, come nell&#39;esempio precedente per la funzione `size_of`, se si desidera accedere ed esportare solo la prima volta che un cliente ha acquistato un determinato prodotto, è possibile utilizzare `purchaseTime[0]` per esportare il primo elemento del timestamp, `purchaseTime[1]` per esportare il secondo elemento del timestamp, `purchaseTime[2]` per esportare il terzo elemento del timestamp e così via.

![Esempio di mapping che mostra come è possibile accedere a un elemento di un array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In questo caso, il file di output si presenta come di seguito, esportando la prima volta che il cliente ha effettuato un acquisto:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` e `last` funzioni per esportare array {#first-and-last-functions-export-arrays}

Utilizzare le funzioni `first` e `last` per esportare il primo o l&#39;ultimo elemento di un array. Ad esempio, continuando con l&#39;oggetto array `purchaseTime` con più marche temporali degli esempi precedenti, è possibile utilizzarle per le funzioni per esportare il primo o l&#39;ultimo acquisto effettuato da una persona.

![Esempio di mapping che include la prima e l&#39;ultima funzione.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In questo caso, il file di output si presenta come di seguito, esportando la prima e l’ultima volta che il cliente ha effettuato un acquisto:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### Funzioni di hashing {#hashing-functions}

Altre funzioni disponibili sono specifiche per l&#39;esportazione di array o elementi da un array. È possibile utilizzare le funzioni di hashing per eseguire l&#39;hashing degli attributi nei file esportati. Ad esempio, se negli attributi sono presenti informazioni di identificazione personale, puoi eseguire l’hashing di tali campi durante l’esportazione.

È possibile eseguire l&#39;hashing diretto dei valori stringa, ad esempio `md5(personalEmail.address)`. Se lo desideri, puoi anche eseguire l&#39;hashing di singoli elementi di campi array, supponendo che gli elementi nell&#39;array siano stringhe, come segue: `md5(purchaseTime[0])`

Le funzioni di hashing supportate sono:

| Funzione | Espressione di esempio |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` | `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}
