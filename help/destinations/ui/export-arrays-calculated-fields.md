---
title: (Beta) Utilizzare i campi calcolati per esportare matrici in file sequenziali
type: Tutorial
description: Scopri come esportare array e campi calcolati da Real-Time CDP a destinazioni basate su profili batch.
badge: "Beta"
source-git-commit: 79924b9a7d5114c94a004f99fb194102845b2127
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 2%

---


# (Beta) Utilizzare i campi calcolati per esportare le matrici in file di schema flat {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Supporto per gli array di esportazione (Beta)"
>abstract="Esporta semplici array di valori int, stringa o booleani da Experienci Platform alla destinazione di archiviazione cloud desiderata. Si applicano alcune limitazioni. Consulta la documentazione per esempi esaurienti e funzioni supportate."

<!--

additional links for contextualhelp:

>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Examples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Known limitations"

-->

>[!AVAILABILITY]
>
>* La funzionalità per esportare array tramite campi calcolati è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Scopri come esportare array tramite campi calcolati da Real-Time CDP in file di schema flat nelle destinazioni di archiviazione cloud. Leggi questo documento per comprendere i casi d’uso abilitati da questa funzionalità.

Ottieni informazioni complete sui campi calcolati: cosa sono e perché sono importanti. Leggi le pagine collegate di seguito per un’introduzione ai campi calcolati in Preparazione dati e ulteriori informazioni su tutte le funzioni disponibili:

* [Guida e panoramica dell’interfaccia utente](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funzioni di preparazione dei dati](/help/data-prep/functions.md)

>[!IMPORTANT]
>
>Non tutte le funzioni elencate sopra sono supportate *durante l’esportazione di campi nelle destinazioni di archiviazione cloud* utilizzo della funzionalità campi calcolati. Consulta la [sezione funzioni supportate](#supported-functions) per ulteriori informazioni, consulta.

## Array e altri tipi di oggetti in Platform {#arrays-strings-other-objects}

Ad Experience Platform, puoi utilizzare [Schemi XDM](/help/xdm/home.md) per gestire diversi tipi di campi. In precedenza, era possibile esportare nelle destinazioni desiderate campi di tipo coppia chiave-valore semplici, come stringhe di Experience Platform. Un esempio di questo campo precedentemente supportato per l’esportazione è `personalEmail.address`:`johndoe@acme.org`.

Altri tipi di campo in Experienci Platform includono i campi array. Ulteriori informazioni su [gestione dei campi array nell’interfaccia utente di Experienci Platform](/help/xdm/ui/fields/array.md). Oltre ai tipi di campo supportati in precedenza, ora è possibile esportare oggetti array come: `organizations:[marketing, sales, engineering]`. Vedi più avanti [esempi dettagliati](#examples) informazioni su come utilizzare varie funzioni per accedere a elementi di array, unire elementi di array in una stringa e altro ancora.

## Limitazioni note {#known-limitations}

Tieni presente le seguenti limitazioni note per la versione beta di questa funzionalità:

* Al momento, l’esportazione in file JSON o Parquet con schemi gerarchici non è supportata. Puoi esportare gli array solo in file flat schema CSV, JSON e Parquet.
* In questo momento, *è possibile esportare solo array semplici (o array di valori primitivi) nelle destinazioni di archiviazione cloud*. Ciò significa che è possibile esportare oggetti array che includono valori stringa, int o booleani. Non è possibile esportare mappe o array di mappe o oggetti. Nella finestra modale dei campi calcolati vengono visualizzate solo le matrici che è possibile esportare.

## Prerequisiti {#prerequisites}

Avanzamento attraverso [passaggi di attivazione per le destinazioni di archiviazione cloud](/help/destinations/ui/activate-batch-profile-destinations.md) e accedi al [mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) passaggio.

## Come esportare i campi calcolati {#how-to-export-calculated-fields}

Nel passaggio di mappatura del flusso di lavoro di attivazione per le destinazioni di archiviazione cloud, seleziona **[!UICONTROL (Beta) Aggiungi campo calcolato]**.

![Aggiungi campo calcolato da esportare](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Viene visualizzata una finestra modale in cui è possibile selezionare gli attributi che è possibile utilizzare per esportare gli attributi da Experienci Platform.

>[!IMPORTANT]
>
>Solo alcuni dei campi dello schema XDM sono disponibili nel **[!UICONTROL Campo]** visualizzazione. Puoi visualizzare valori stringa e matrici di valori stringa, int e booleani. Ad esempio, il `segmentMembership` non viene visualizzato, in quanto include altri valori di array.

![Finestra modale 1](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Ad esempio, utilizza `join` funzione su `loyaltyID` come mostrato di seguito per esportare un array di ID fedeltà come stringa concatenata con un trattino basso in un file CSV. Visualizza [ulteriori informazioni su questo e altri esempi riportati di seguito](#join-function-export-arrays).

![Finestra modale 2](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Seleziona **[!UICONTROL Salva]** per mantenere il campo calcolato e tornare al passaggio di mappatura.

![Finestra modale 3](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Torna al passaggio di mappatura del flusso di lavoro, compila il **[!UICONTROL Campo di destinazione]** con un valore dell’intestazione di colonna desiderata per questo campo nei file esportati.

![Seleziona campo di destinazione 1](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Seleziona campo di destinazione 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Quando è pronto, seleziona **[!UICONTROL Successivo]** per procedere al passaggio successivo del flusso di lavoro di attivazione.

![Seleziona avanti per procedere](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Funzioni supportate {#supported-functions}

Nella versione beta dei campi calcolati e nel supporto degli array per le destinazioni sono supportate solo le seguenti funzioni:

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

Consulta gli esempi e ulteriori informazioni nelle sezioni seguenti per alcune delle funzioni elencate in precedenza. Per le altre funzioni elencate, fare riferimento a [documentazione sulle funzioni generali nella sezione Preparazione dati](/help/data-prep/functions.md).

### `join` funzione per esportare array {#join-function-export-arrays}

Utilizza il `join` funzione per concatenare gli elementi di un array in una stringa, utilizzando un separatore desiderato, ad esempio `_` o `|`.

Ad esempio, puoi combinare i seguenti campi XDM come mostrato nella schermata di mappatura utilizzando un `join('_',loyalty.loyaltyID)` sintassi:

* `"organizations": ["Marketing","Sales,"Finance"]` array
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Schermata di mappatura](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

In questo caso, il file di output si presenta come di seguito. I tre elementi dell’array vengono concatenati in una singola stringa utilizzando `_` carattere.

```
`First_Name,Last_Name,Organization
John,Doe,"Marketing_Sales_Finance"
```

### `coalesce` funzione per esportare array {#coalesce-function-export-arrays}

Utilizza il `coalesce` funzione per accedere ed esportare il primo elemento non nullo di un array in una stringa.

Ad esempio, puoi combinare i seguenti campi XDM come mostrato nella schermata di mappatura utilizzando un `coalesce(subscriptions.hasPromotion)` sintassi per restituire il primo vero di falso valore nell’array:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` array
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Schermata di mappatura per la funzione coalesce](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

In questo caso, il file di output si presenta come di seguito. Notare come il primo non-null `true` valore nell’array viene esportato nel file.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```


### `size_of` funzione per esportare array {#sizeof-function-export-arrays}

Utilizza il `size_of` per indicare quanti elementi esistono in un array. Ad esempio, se hai un `purchaseTime` oggetto array con più marche temporali, è possibile utilizzare `size_of` funzione che indica quanti acquisti separati sono stati effettuati da una persona.

Ad esempio, puoi combinare i seguenti campi XDM come mostrato nella schermata di mappatura.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` array che indica cinque diversi tempi di acquisto da parte del cliente
* `personalEmail.address` string

![Schermata di mappatura per la funzione size_of](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In questo caso, il file di output si presenta come di seguito. Osserva come la seconda colonna indica il numero di elementi nell’array, corrispondente al numero di acquisti separati effettuati dal cliente.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Accesso all&#39;array basato su indice {#index-based-array-access}

È possibile accedere a un indice di un array per esportare un singolo elemento dall’array. Ad esempio, simile all’esempio precedente per il `size_of` , se desideri accedere ed esportare solo la prima volta che un cliente ha acquistato un determinato prodotto, puoi utilizzare `purchaseTime[0]` per esportare il primo elemento della marca temporale, `purchaseTime[1]` per esportare il secondo elemento della marca temporale, `purchaseTime[2]` per esportare il terzo elemento della marca temporale e così via.

![Schermata di mappatura per l’accesso all’indice](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In questo caso, il file di output si presenta come:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` e `last` funzioni per esportare array {#first-and-last-functions-export-arrays}

Utilizza il `first` e `last` funzioni per esportare il primo o l&#39;ultimo elemento di un array. Ad esempio, continuando con `purchaseTime` oggetto array con più marche temporali dagli esempi precedenti, è possibile utilizzarle per esportare la prima o l’ultima ora di acquisto effettuata da una persona.

![Schermata di mappatura per la prima e l’ultima funzione](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In questo caso, il file di output si presenta come:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

<!--

### `iif` function to export arrays {#iif-function-export-arrays}

Here are some examples of how you could use the `iif` function to access and export arrays and other fields: (STILL TO DO)

-->

### `md5` e `sha256` funzioni di hashing {#hashing-functions}

Oltre alle funzioni specifiche per l’esportazione di array o elementi da un array, puoi utilizzare funzioni di hashing per eseguire l’hashing degli attributi. Ad esempio, se negli attributi sono presenti informazioni di identificazione personale, puoi eseguire l’hashing di tali campi durante l’esportazione.

Puoi eseguire l’hashing diretto dei valori stringa, ad esempio `md5(personalEmail.address)`. Se lo desideri, puoi anche eseguire l’hashing di singoli elementi di campi array, come segue: `md5(purchaseTime[0])`



