---
title: (Beta) Utilizzare i campi calcolati per esportare array in file di schema piatto
type: Tutorial
description: Scopri come utilizzare i campi calcolati per esportare array in file di schema flat da Real-Time CDP a destinazioni di archiviazione cloud.
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 787aaef26fab5ca3acff8303f928efa299cafa93
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 5%

---

# (Beta) Utilizzare i campi calcolati per esportare array in file di schema piatto {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Supporto per gli array di esportazione (Beta)"
>abstract="Utilizza il controllo **Aggiungi campo calcolato** per esportare semplici array di int, stringa o booleani da Experience Platform alla destinazione di archiviazione cloud desiderata. Si applicano alcune limitazioni. Consulta la documentazione per esempi esaurienti e funzioni supportate."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=it#examples" text="Esempi"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=it#known-limitations" text="Limitazioni note"

>[!AVAILABILITY]
>
>* La funzionalità per esportare array tramite campi calcolati è attualmente disponibile in Beta. La documentazione e le funzionalità sono soggette a modifiche.

Scopri come esportare array tramite campi calcolati da Real-Time CDP in file di schema flat in [destinazioni di archiviazione cloud](/help/destinations/catalog/cloud-storage/overview.md). Leggi questo documento per comprendere i casi d’uso abilitati da questa funzionalità.

Ottieni informazioni complete sui campi calcolati: cosa sono e perché sono importanti. Leggi le pagine collegate di seguito per un’introduzione ai campi calcolati in Preparazione dati e ulteriori informazioni su tutte le funzioni disponibili:

* [Guida e panoramica dell’interfaccia utente](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funzioni di preparazione dati](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Array e altri tipi di oggetti in Platform {#arrays-strings-other-objects}

Ad Experience Platform, puoi utilizzare [schemi XDM](/help/xdm/home.md) per gestire diversi tipi di campo. In precedenza, era possibile esportare nelle destinazioni desiderate campi di tipo coppia chiave-valore semplici, come stringhe di Experience Platform. Un esempio di questo campo precedentemente supportato per l&#39;esportazione è `personalEmail.address`:`johndoe@acme.org`.

Altri tipi di campo in Experience Platform includono i campi array. Ulteriori informazioni sulla [gestione dei campi array nell&#39;interfaccia utente Experience Platform](/help/xdm/ui/fields/array.md). Oltre ai tipi di campo supportati in precedenza, è ora possibile esportare oggetti array come: `organizations:[marketing, sales, engineering]`. Di seguito sono riportati [estesi esempi](#examples) su come utilizzare varie funzioni per accedere a elementi di array, unire elementi di array in una stringa e altro ancora.

## Limitazioni note {#known-limitations}

Tieni presente le seguenti limitazioni note per la versione beta di questa funzionalità:

* Al momento, l’esportazione in file JSON o Parquet con schemi gerarchici non è supportata. Puoi esportare gli array solo in file flat schema CSV, JSON e Parquet.
* Al momento, *è possibile esportare solo array semplici (o array di valori primitivi) nelle destinazioni dell&#39;archiviazione cloud*. Ciò significa che è possibile esportare oggetti array che includono valori stringa, int o booleani. Non è possibile esportare mappe o array di mappe o oggetti. Nella finestra modale dei campi calcolati vengono visualizzate solo le matrici che è possibile esportare.

## Prerequisiti {#prerequisites}

[Connetti](/help/destinations/ui/connect-destination.md) a una destinazione di archiviazione cloud desiderata, segui i [passaggi di attivazione per le destinazioni di archiviazione cloud](/help/destinations/ui/activate-batch-profile-destinations.md) e procedi al passaggio [mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Come esportare i campi calcolati {#how-to-export-calculated-fields}

Nel passaggio di mappatura del flusso di lavoro di attivazione per le destinazioni di archiviazione cloud, seleziona **[!UICONTROL (Beta) Aggiungi campo calcolato]**.

![Aggiungi campo calcolato evidenziato nel passaggio di mappatura del flusso di lavoro di attivazione batch.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Viene visualizzata una finestra modale in cui è possibile selezionare gli attributi che è possibile utilizzare per esportare gli attributi da Experience Platform.

>[!IMPORTANT]
>
>Nella visualizzazione **[!UICONTROL Campo]** sono disponibili solo alcuni campi dello schema XDM. Puoi visualizzare valori stringa e matrici di valori stringa, int e booleani. Ad esempio, l&#39;array `segmentMembership` non viene visualizzato, in quanto include altri valori dell&#39;array.

![Finestra modale della funzionalità del campo calcolato senza alcuna funzione ancora selezionata.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Ad esempio, utilizza la funzione `join` nel campo `loyaltyID` come mostrato di seguito per esportare un array di ID fedeltà come stringa concatenata con un trattino basso in un file CSV. Visualizza [ulteriori informazioni su questo e altri esempi più avanti](#join-function-export-arrays).

![Finestra modale della funzionalità del campo calcolato con la funzione di unione selezionata.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Seleziona **[!UICONTROL Salva]** per mantenere il campo calcolato e tornare al passaggio di mappatura.

![Finestra modale della funzionalità del campo calcolato con la funzione di unione selezionata ed il controllo Salva evidenziato.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Tornando al passaggio di mappatura del flusso di lavoro, compila il **[!UICONTROL campo di destinazione]** con il valore dell&#39;intestazione di colonna desiderata per questo campo nei file esportati.

![Passaggio di mapping con il campo di destinazione evidenziato.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Seleziona campo di destinazione 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Al termine, seleziona **[!UICONTROL Avanti]** per procedere al passaggio successivo del flusso di lavoro di attivazione.

![Passaggio di mappatura con il campo di destinazione evidenziato e un valore di destinazione compilato.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Funzioni supportate {#supported-functions}

Tutte le [funzioni di preparazione dati](/help/data-prep/functions.md) documentate sono supportate quando si attivano i dati in destinazioni basate su file.

Tuttavia, attualmente vengono fornite descrizioni estese dei casi d’uso e informazioni sull’output di esempio solo per le seguenti funzioni nella versione beta dei campi calcolati e per il supporto degli array per le destinazioni:

* `join`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`
* `sha256`
* `md5`

## Esempi di funzioni utilizzate per esportare array {#examples}

Consulta gli esempi e ulteriori informazioni nelle sezioni seguenti per alcune delle funzioni elencate in precedenza. Per le altre funzioni elencate, consulta la [documentazione sulle funzioni generali nella sezione Preparazione dati](/help/data-prep/functions.md).

### Funzione `join` per esportare array {#join-function-export-arrays}

Utilizzare la funzione `join` per concatenare gli elementi di un array in una stringa utilizzando un separatore desiderato, ad esempio `_` o `|`.

Ad esempio, puoi combinare i seguenti campi XDM come mostrato nella schermata di mappatura utilizzando una sintassi `join('_',loyalty.loyaltyID)`:

* Array `"organizations": ["Marketing","Sales,"Finance"]`
* `person.name.firstName` stringa
* `person.name.lastName` stringa
* `personalEmail.address` stringa

![Esempio di mapping che include la funzione di join.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

In questo caso, il file di output si presenta come di seguito. I tre elementi dell&#39;array vengono concatenati in una singola stringa utilizzando il carattere `_`.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
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

Utilizzare la funzione `add_to_array` per aggiungere elementi a un array esportato. È possibile combinare questa funzione con la funzione `join` descritta in precedenza.

Continuando con l&#39;oggetto array `organizations` dall&#39;alto, è possibile scrivere una funzione come `source: join('_', add_to_array(organizations,"2023"))`, restituendo le organizzazioni di cui una persona è membro nel 2023.

![Esempio di mapping che include la funzione add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

In questo caso, il file di output si presenta come di seguito. Nota come i tre elementi dell’array sono concatenati in una singola stringa utilizzando il carattere `_` e 2023 viene aggiunto alla fine della stringa.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

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

### Funzioni di hashing {#hashing-functions}

Oltre alle funzioni specifiche per l&#39;esportazione di array o elementi da un array, è possibile utilizzare funzioni di hashing per eseguire l&#39;hashing degli attributi nei file esportati. Ad esempio, se negli attributi sono presenti informazioni di identificazione personale, puoi eseguire l’hashing di tali campi durante l’esportazione.

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