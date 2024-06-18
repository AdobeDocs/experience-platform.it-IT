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
>* La funzionalità per esportare array tramite campi calcolati è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Scopri come esportare array tramite campi calcolati da Real-Time CDP in file di schema flat in [destinazioni archiviazione cloud](/help/destinations/catalog/cloud-storage/overview.md). Leggi questo documento per comprendere i casi d’uso abilitati da questa funzionalità.

Ottieni informazioni complete sui campi calcolati: cosa sono e perché sono importanti. Leggi le pagine collegate di seguito per un’introduzione ai campi calcolati in Preparazione dati e ulteriori informazioni su tutte le funzioni disponibili:

* [Guida e panoramica dell’interfaccia utente](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funzioni di preparazione dati](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Array e altri tipi di oggetti in Platform {#arrays-strings-other-objects}

Ad Experience Platform, puoi utilizzare [Schemi XDM](/help/xdm/home.md) per gestire diversi tipi di campi. In precedenza, era possibile esportare nelle destinazioni desiderate campi di tipo coppia chiave-valore semplici, come stringhe di Experience Platform. Un esempio di questo campo precedentemente supportato per l’esportazione è `personalEmail.address`:`johndoe@acme.org`.

Altri tipi di campo in Experienci Platform includono i campi array. Ulteriori informazioni su [gestione dei campi array nell’interfaccia utente di Experienci Platform](/help/xdm/ui/fields/array.md). Oltre ai tipi di campo supportati in precedenza, ora è possibile esportare oggetti array come: `organizations:[marketing, sales, engineering]`. Vedi più avanti [esempi dettagliati](#examples) informazioni su come utilizzare varie funzioni per accedere a elementi di array, unire elementi di array in una stringa e altro ancora.

## Limitazioni note {#known-limitations}

Tieni presente le seguenti limitazioni note per la versione beta di questa funzionalità:

* Al momento, l’esportazione in file JSON o Parquet con schemi gerarchici non è supportata. Puoi esportare gli array solo in file flat schema CSV, JSON e Parquet.
* In questo momento, *è possibile esportare solo array semplici (o array di valori primitivi) nelle destinazioni di archiviazione cloud*. Ciò significa che è possibile esportare oggetti array che includono valori stringa, int o booleani. Non è possibile esportare mappe o array di mappe o oggetti. Nella finestra modale dei campi calcolati vengono visualizzate solo le matrici che è possibile esportare.

## Prerequisiti {#prerequisites}

[Connetti](/help/destinations/ui/connect-destination.md) nella destinazione di archiviazione cloud desiderata, procedere attraverso [passaggi di attivazione per le destinazioni di archiviazione cloud](/help/destinations/ui/activate-batch-profile-destinations.md) e accedi al [mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) passaggio.

## Come esportare i campi calcolati {#how-to-export-calculated-fields}

Nel passaggio di mappatura del flusso di lavoro di attivazione per le destinazioni di archiviazione cloud, seleziona **[!UICONTROL (Beta) Aggiungi campo calcolato]**.

![Aggiungi campo calcolato evidenziato nella fase di mappatura del flusso di lavoro di attivazione batch.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Viene visualizzata una finestra modale in cui è possibile selezionare gli attributi che è possibile utilizzare per esportare gli attributi da Experienci Platform.

>[!IMPORTANT]
>
>Solo alcuni dei campi dello schema XDM sono disponibili nel **[!UICONTROL Campo]** visualizzazione. Puoi visualizzare valori stringa e matrici di valori stringa, int e booleani. Ad esempio, il `segmentMembership` non viene visualizzato, in quanto include altri valori di array.

![Finestra modale della funzionalità del campo calcolato senza che sia stata ancora selezionata alcuna funzione.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Ad esempio, utilizza `join` funzione su `loyaltyID` come mostrato di seguito per esportare un array di ID fedeltà come stringa concatenata con un trattino basso in un file CSV. Visualizza [ulteriori informazioni su questo e altri esempi riportati di seguito](#join-function-export-arrays).

![Finestra modale della funzionalità del campo calcolato con la funzione di join selezionata.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Seleziona **[!UICONTROL Salva]** per mantenere il campo calcolato e tornare al passaggio di mappatura.

![Finestra modale della funzionalità del campo calcolato con la funzione di unione selezionata ed il controllo Salva evidenziato.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Torna al passaggio di mappatura del flusso di lavoro, compila il **[!UICONTROL Campo di destinazione]** con un valore dell’intestazione di colonna desiderata per questo campo nei file esportati.

![Mappatura del passaggio con il campo di destinazione evidenziato.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Seleziona campo di destinazione 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Quando è pronto, seleziona **[!UICONTROL Successivo]** per procedere al passaggio successivo del flusso di lavoro di attivazione.

![Fase di mappatura con il campo di destinazione evidenziato e un valore di destinazione compilato.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Funzioni supportate {#supported-functions}

Tutti i documenti [Funzioni di preparazione dati](/help/data-prep/functions.md) sono supportate quando si attivano i dati in destinazioni basate su file.

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

Consulta gli esempi e ulteriori informazioni nelle sezioni seguenti per alcune delle funzioni elencate in precedenza. Per le altre funzioni elencate, fare riferimento a [documentazione sulle funzioni generali nella sezione Preparazione dati](/help/data-prep/functions.md).

### `join` funzione per esportare array {#join-function-export-arrays}

Utilizza il `join` funzione per concatenare gli elementi di un array in una stringa, utilizzando un separatore desiderato, ad esempio `_` o `|`.

Ad esempio, puoi combinare i seguenti campi XDM come mostrato nella schermata di mappatura utilizzando un `join('_',loyalty.loyaltyID)` sintassi:

* `"organizations": ["Marketing","Sales,"Finance"]` array
* `person.name.firstName` stringa
* `person.name.lastName` stringa
* `personalEmail.address` stringa

![Esempio di mappatura che include la funzione di join.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

In questo caso, il file di output si presenta come di seguito. I tre elementi dell’array vengono concatenati in una singola stringa utilizzando `_` carattere.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
```

### `iif` funzione per esportare array {#iif-function-export-arrays}

Utilizza il `iif` funzione per esportare elementi di un array in determinate condizioni. Ad esempio, continuando con `organizations` oggetto array dall’alto, puoi scrivere una semplice funzione condizionale come `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Esempio di mappatura che include la funzione iif.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

In questo caso, il file di output si presenta come di seguito. In questo caso, il primo elemento dell’array è Marketing, quindi la persona è membro del reparto marketing.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` funzione per esportare array {#add-to-array-function-export-arrays}

Utilizza il `add_to_array` per aggiungere elementi a un array esportato. È possibile combinare questa funzione con `join` funzione descritta in precedenza.

Continuando con `organizations` oggetto array dall&#39;alto, puoi scrivere una funzione come `source: join('_', add_to_array(organizations,"2023"))`, restituendo le organizzazioni di cui una persona è membro nel 2023.

![Esempio di mappatura che include la funzione add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

In questo caso, il file di output si presenta come di seguito. I tre elementi dell’array vengono concatenati in una singola stringa utilizzando `_` e 2023 viene inoltre aggiunto alla fine della stringa.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce` funzione per esportare array {#coalesce-function-export-arrays}

Utilizza il `coalesce` funzione per accedere ed esportare il primo elemento non nullo di un array in una stringa.

Ad esempio, puoi combinare i seguenti campi XDM come mostrato nella schermata di mappatura utilizzando un `coalesce(subscriptions.hasPromotion)` sintassi per restituire il primo `true` di `false` valore nell’array:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` array
* `person.name.firstName` stringa
* `person.name.lastName` stringa
* `personalEmail.address` stringa

![Esempio di mappatura che include la funzione coalesce.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

In questo caso, il file di output si presenta come di seguito. Notare come il primo non-null `true` valore nell’array viene esportato nel file.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` funzione per esportare array {#sizeof-function-export-arrays}

Utilizza il `size_of` per indicare quanti elementi esistono in un array. Ad esempio, se hai un `purchaseTime` oggetto array con più marche temporali, è possibile utilizzare `size_of` funzione che indica quanti acquisti separati sono stati effettuati da una persona.

Ad esempio, puoi combinare i seguenti campi XDM come mostrato nella schermata di mappatura.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` array che indica cinque diversi tempi di acquisto da parte del cliente
* `personalEmail.address` stringa

![Esempio di mappatura che include la funzione size_of.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In questo caso, il file di output si presenta come di seguito. Osserva come la seconda colonna indica il numero di elementi nell’array, corrispondente al numero di acquisti separati effettuati dal cliente.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Accesso all&#39;array basato su indice {#index-based-array-access}

È possibile accedere a un indice di un array per esportare un singolo elemento dall’array. Ad esempio, simile all’esempio precedente per il `size_of` , se desideri accedere ed esportare solo la prima volta che un cliente ha acquistato un determinato prodotto, puoi utilizzare `purchaseTime[0]` per esportare il primo elemento della marca temporale, `purchaseTime[1]` per esportare il secondo elemento della marca temporale, `purchaseTime[2]` per esportare il terzo elemento della marca temporale e così via.

![Esempio di mappatura che mostra come accedere a un elemento di un array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In questo caso, il file di output si presenta come di seguito, esportando la prima volta che il cliente ha effettuato un acquisto:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` e `last` funzioni per esportare array {#first-and-last-functions-export-arrays}

Utilizza il `first` e `last` funzioni per esportare il primo o l&#39;ultimo elemento di un array. Ad esempio, continuando con `purchaseTime` oggetto array con più marche temporali dagli esempi precedenti, è possibile utilizzarle per esportare la prima o l’ultima ora di acquisto effettuata da una persona.

![Esempio di mappatura che include la prima e l’ultima funzione.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In questo caso, il file di output si presenta come di seguito, esportando la prima e l’ultima volta che il cliente ha effettuato un acquisto:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### Funzioni di hashing {#hashing-functions}

Oltre alle funzioni specifiche per l&#39;esportazione di array o elementi da un array, è possibile utilizzare funzioni di hashing per eseguire l&#39;hashing degli attributi nei file esportati. Ad esempio, se negli attributi sono presenti informazioni di identificazione personale, puoi eseguire l’hashing di tali campi durante l’esportazione.

Puoi eseguire l’hashing diretto dei valori stringa, ad esempio `md5(personalEmail.address)`. Se lo desideri, puoi anche eseguire l’hash di singoli elementi di campi array, supponendo che gli elementi nell’array siano stringhe, come segue: `md5(purchaseTime[0])`

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