---
title: Utilizzare i campi calcolati per esportare matrici come stringhe
type: Tutorial
description: Scopri come utilizzare i campi calcolati per esportare gli array da Real-Time CDP a destinazioni di archiviazione cloud come stringhe.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 849d42e36921e60b6ac3a5e89336b954e64a35d7
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# Utilizzare i campi calcolati per esportare matrici come stringhe{#use-calculated-fields-to-export-arrays-as-strings}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Supporto per l&#39;esportazione di array"
>abstract="<p>Utilizzare il controllo **Add calculfield** per esportare matrici di valori int, string, boolean e object da Experience Platform alla destinazione di archiviazione cloud desiderata.</p><p> Le matrici devono essere esportate come stringhe utilizzando la funzione `array_to_string`. Consulta la documentazione per esempi esaurienti e altre funzioni supportate.</p>"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=it#examples" text="Esempi"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=it#known-limitations" text="Limitazioni note"

>[!AVAILABILITY]
>
>* La funzionalità di esportazione di array tramite campi calcolati è generalmente disponibile.

Scopri come esportare array tramite campi calcolati da Real-Time CDP a [destinazioni di archiviazione cloud](/help/destinations/catalog/cloud-storage/overview.md) come stringhe. Leggi questo documento per comprendere i casi d’uso abilitati da questa funzionalità.

Ottieni informazioni complete sui campi calcolati: cosa sono e perché sono importanti. Leggi le pagine collegate di seguito per un’introduzione ai campi calcolati in Preparazione dati e ulteriori informazioni su tutte le funzioni disponibili:

* [Guida e panoramica dell’interfaccia utente](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funzioni di preparazione dati](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Array e altri tipi di oggetti in Platform {#arrays-strings-other-objects}

Ad Experience Platform, puoi utilizzare [schemi XDM](/help/xdm/home.md) per gestire diversi tipi di campo. Prima di aggiungere il supporto per le esportazioni di array, era possibile esportare semplici campi di tipo coppia chiave-valore, come stringhe di Experience Platform, nelle destinazioni desiderate. Un esempio di questo campo precedentemente supportato per l&#39;esportazione è `personalEmail.address`:`johndoe@acme.org`.

Altri tipi di campo in Experience Platform includono i campi array. Ulteriori informazioni sulla [gestione dei campi array nell&#39;interfaccia utente Experience Platform](/help/xdm/ui/fields/array.md). Oltre ai tipi di campo supportati in precedenza, è ora possibile esportare oggetti array come l&#39;esempio seguente, concatenati in una stringa utilizzando la funzione `array_to_string`.

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

Di seguito sono riportati [estesi esempi](#examples) di come utilizzare varie funzioni per accedere a elementi di array, trasformare e filtrare array, unire elementi di array in una stringa e altro ancora.

## Limitazioni note {#known-limitations}

Tieni presente le seguenti limitazioni note attualmente applicabili a questa funzionalità:

* L&#39;esportazione in file JSON o Parquet *con schemi gerarchici* non è al momento supportata. È possibile esportare array nei file CSV, JSON e Parquet *solo come stringhe*, utilizzando la funzione `array_to_string`.

## Prerequisiti {#prerequisites}

[Connetti](/help/destinations/ui/connect-destination.md) a una destinazione di archiviazione cloud desiderata, segui i [passaggi di attivazione per le destinazioni di archiviazione cloud](/help/destinations/ui/activate-batch-profile-destinations.md) e procedi al passaggio [mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Come esportare i campi calcolati {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Abilita schema di output gerarchico"
>abstract="Attiva per esportare strutture gerarchiche come array."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="Aggiungi campi calcolati disabilitati"
>abstract="Questo controllo è disattivato perché è stata selezionata l&#39;esportazione di strutture piatte durante la connessione alla destinazione."

Nel passaggio di mappatura del flusso di lavoro di attivazione per le destinazioni di archiviazione cloud, seleziona **[!UICONTROL Aggiungi campo calcolato]**.

![Aggiungi campo calcolato evidenziato nel passaggio di mappatura del flusso di lavoro di attivazione batch.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Viene visualizzata una finestra modale in cui è possibile selezionare funzioni e campi per esportare attributi da Experience Platform.

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

## Funzioni supportate di esempio per esportare array {#supported-functions}

Tutte le [funzioni di preparazione dati](/help/data-prep/functions.md) documentate sono supportate quando si attivano i dati in destinazioni basate su file.

Le funzioni seguenti, specifiche per la gestione delle esportazioni di array, sono documentate insieme ad esempi.

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

## Esempi di funzioni utilizzate per esportare array {#examples}

Consulta gli esempi e ulteriori informazioni nelle sezioni seguenti per alcune delle funzioni elencate in precedenza. Per le altre funzioni elencate, consulta la [documentazione sulle funzioni generali nella sezione Preparazione dati](/help/data-prep/functions.md).

### Funzione `array_to_string` per esportare array {#array-to-string-function-export-arrays}

Utilizzare la funzione `array_to_string` per concatenare gli elementi di un array in una stringa utilizzando un separatore desiderato, ad esempio `_` o `|`.

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

### Funzione `filterArray` per esportare array filtrati

Utilizzare la funzione `filterArray` per filtrare gli elementi di un array esportato. È possibile combinare questa funzione con la funzione `array_to_string` descritta in precedenza.

Continuando con l&#39;oggetto array `organizations` dall&#39;alto, è possibile scrivere una funzione come `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`, restituendo alle organizzazioni un valore per `founded` nell&#39;anno 2021 o più recente.

![Esempio della funzione filterArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

In questo caso, il file di output si presenta come di seguito. I due elementi dell&#39;array che soddisfano il criterio vengono concatenati in una singola stringa utilizzando il carattere `_`.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### Funzione `transformArray` per esportare array trasformati

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

### Funzione `flattenArray` per esportare array appiattiti

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

<!--

### Hashing functions {#hashing-functions}

In addition to the functions specific for exporting arrays or elements from an array, you can use hashing functions to hash attributes in the exported files. For example, if you have any personally identifiable information in attributes, you can hash those fields when exporting them. 

You can hash string values directly, for example `md5(personalEmail.address)`. If desired, you can also hash individual elements of array fields, assuming elements in the array are strings, like this: `md5(purchaseTime[0])`

The supported hashing functions are:

|Function | Sample expression |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` |  `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}

-->