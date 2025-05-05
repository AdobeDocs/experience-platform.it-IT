---
title: Eseguire trasformazioni sui dati esportati nelle destinazioni di archiviazione cloud utilizzando campi calcolati
type: Tutorial
description: Come utilizzare la funzionalità dei campi calcolati per eseguire trasformazioni sui dati esportati verso destinazioni di archiviazione cloud
exl-id: 1e14f964-4c03-4d0c-be8d-c3dcb48a335a
source-git-commit: 14c672ef57e0b0247020075552c782ed18db8484
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 8%

---

# Eseguire trasformazioni sui dati esportati nelle destinazioni di archiviazione cloud utilizzando campi calcolati {#data-transformation-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Aggiungere campi calcolati"
>abstract="<p>Utilizza il controllo **Aggiungi campo calcolato** per eseguire varie trasformazioni sui dati esportati verso destinazioni di archiviazione cloud. Ad esempio, puoi applicare l’hashing ai dati, concatenare gli array in stringhe e altro ancora."

<!--

disable additional URLs for a while

>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-maps-objects.html?lang=it#examples" text="Examples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-maps-objects.html?lang=it#known-limitations" text="Known limitations"

-->

>[!AVAILABILITY]
>
>La funzionalità per eseguire trasformazioni sui dati esportati in cloud destinazioni di archiviazione è disponibile a livello generale per le seguenti destinazioni: , , , , [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md) [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md) [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md), , nonché per qualsiasi destinazione di archiviazione cloud creata da partner personalizzate create tramite [Destination SDK.](/help/destinations/destination-sdk/overview.md) [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)

Per eseguire varie trasformazioni sui dati esportati verso destinazioni di archiviazione cloud, è necessario utilizzare la funzionalità campi calcolati nella fase di mappatura del workflow di esportazione. Per informazioni dettagliate sui campi calcolati, visita le pagine collegate di seguito. Queste pagine includono un&#39;introduzione ai campi calcolati in Preparazione dati e ulteriori informazioni su tutte le funzioni disponibili:

* [interfaccia guida e panoramica](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funzioni di preparazione dati](/help/data-prep/functions.md)

## Prerequisiti {#prerequisites}

Per utilizzare i campi calcolati per le trasformazioni dei dati:

1. [Connettiti](/help/destinations/ui/connect-destination.md) a una destinazione di archiviazione cloud desiderata. Quando ci si connette alla destinazione cloud desiderata, disattivare l&#39;opzione **(/help/destinations/ui/export-arrays-maps-objects.md##export-arrays-maps-objects-toggle)Esporta array, mappe, oggetti&rbrack;**&lbrack;.
2. Segui i [passaggi di attivazione per cloud le destinazioni](/help/destinations/ui/activate-batch-profile-destinations.md) di archiviazione e vai al passaggio di [mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) .

## Utilizzare i campi calcolati {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Abilitare lo schema di output gerarchico"
>abstract="Attiva questa impostazione per abilitare l’esportazione di array, mappe e oggetti verso file JSON o Parquet."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="Aggiungere campi calcolati disabilitati"
>abstract="Questo controllo è disabilitato, perché durante la configurazione della connessione di destinazione hai selezionato **Esporta array, mappe, oggetti** su *Attivato*. Per utilizzare i campi calcolati e le funzioni disponibili all’interno, imposta una nuova connessione di destinazione con l’opzione **Esporta array, mappe, oggetti** su *Disattivato*."

Nel passaggio di mappatura del workflow di attivazione per le destinazioni di archiviazione cloud, selezionare **[!UICONTROL Aggiungi campo]** calcolato.

>[!TIP]
>
>Il **[!UICONTROL controllo Aggiungi campo calcolato]** è disabilitato per le connessioni di destinazione in cui è stato disattivato il **[!UICONTROL controllo Esporta matrici, mappe e oggetti]** . [Ulteriori informazioni](/help/destinations/ui/export-arrays-maps-objects.md#export-arrays-maps-objects-toggle).

![Aggiungi il campo calcolato evidenziato nella fase di mappatura del workflow di attivazione batch.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Si apre una finestra modale in cui è possibile selezionare le funzioni e i campi per esportare gli attributi dal Experience Platform.

![Finestra modale della funzionalità del campo calcolato senza alcuna funzione selezionata ancora.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Ad esempio, utilizza la `array_to_string` `organizations` funzione sul campo come mostrato di seguito per esportare l&#39;array organizations come stringa in un file CSV. [Visualizza ulteriori informazioni su questo e altri esempi più avanti](#array-to-string-function-export-arrays).

![Finestra modale della funzionalità del campo calcolato con la funzione array-to-string selezionata.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Selezionare **[!UICONTROL Salva]** per mantenere il campo calcolato e tornare al passaggio di mappatura.

![Finestra modale della funzionalità del campo calcolato con la funzione array-to-string selezionata e il controllo Salva evidenziato.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Indietro nella fase di mappatura del workflow, compilare il **[!UICONTROL campo]** Target con un valore dell&#39;intestazione di colonna desiderato per questo campo nei file esportati.

![Passaggio di mappatura con il campo destinazione evidenziato.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Seleziona destinazione campo 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Quando è pronto, selezionare **[!UICONTROL Successivo]** per procedere al passaggio successivo del workflow di attivazione.

![Passaggio di mappatura con il campo destinazione evidenziato e un valore destinazione compilato.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Funzioni supportate di esempio per eseguire trasformazioni di dati {#supported-functions}

Tutte le funzioni[&#128279;](/help/data-prep/functions.md) documentate di Data Prep sono supportate quando si attivano i dati verso destinazioni basate su file.

Le funzioni riportate di seguito, specifiche per la gestione delle esportazioni di array o l&#39;applicazione dell&#39;hashing ai campi, sono documentate insieme agli esempi.

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

## Esempi di funzioni utilizzate per eseguire trasformazioni di dati {#examples}

Consulta esempi e ulteriori informazioni nelle sezioni seguenti per alcune delle funzioni sopra elencate. Per le altre funzioni elencate, fare riferimento alla documentazione relativa [alle funzioni generali nella sezione](/help/data-prep/functions.md) Preparazione dati.

### `array_to_string` Funzione per esportare gli array {#array-to-string-function-export-arrays}

Utilizzare la `array_to_string` funzione per concatenare gli elementi di una matrice in una stringa, utilizzando un separatore desiderato, ad esempio `_` o `|`. Questa funzione è utile quando si desidera esportare gli elementi di un array da Experience Platform in un file CSV.

Ad esempio, è possibile combinare i seguenti campi XDM come mostrato nel schermata di mappatura utilizzando una `array_to_string('_',organizations)` sintassi:

* `organizations` array
* `person.name.firstName` corda
* `person.name.lastName` corda
* `personalEmail.address` corda

![Esempio di mappatura con funzione array_to_string.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

In questo caso, il tuo file di output guarda like sotto. Si noti come gli elementi della matrice sono concatenati in una singola stringa utilizzando il `_` carattere.

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `filterArray`Funzione per esportare array filtrati {#filter-array}

Utilizzare questa `filterArray` funzione per filtrare gli elementi di un array esportato. È possibile combinare questa funzione con la `array_to_string` funzione descritta più avanti.

Continuando con l&#39;oggetto array dall&#39;alto`organizations`, è possibile scrivere una funzione like `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`, che restituisce alle organizzazioni un valore per `founded` nell&#39;anno 2021 o più recente.

![Esempio della funzione filterArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

In questo caso, il tuo file di output guarda like sotto. Si noti come i due elementi della matrice che soddisfano il criterio vengono concatenati in un&#39;unica stringa utilizzando il `_` carattere.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray`Funzione per esportare gli array trasformati {#transform-array}

Utilizzare la `transformArray` funzione per trasformare gli elementi di un array esportato. È possibile combinare questa funzione con la `array_to_string` funzione descritta più avanti.

Continuando con l&#39;oggetto array dall&#39;alto`organizations`, è possibile scrivere una funzione like `array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))`, restituendo i nomi delle organizzazioni convertiti tutti in maiuscolo.

![Esempio della funzione transformArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

In questo caso, il tuo file di output guarda like sotto. Si noti come i tre elementi della matrice vengono trasformati e concatenati in una singola stringa utilizzando il `_` carattere.

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### `iif` Funzione per esportare gli array {#iif-function-export-arrays}

Utilizzare la `iif` funzione per esportare elementi di un array in determinate condizioni. Ad esempio, continuando con l&#39;oggetto array dall&#39;alto `organizations` , è possibile scrivere una semplice funzione condizionale like `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Esempio di mappatura con funzione if.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

In questo caso, il tuo file di output guarda like sotto. In questo caso, il primo elemento della matrice è Marketing, quindi la persona è un membro del reparto marketing.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` Funzione per esportare gli array {#add-to-array-function-export-arrays}

Utilizzare la `add_to_array` funzione per aggiungere elementi a un array esportato. È possibile combinare questa funzione con la `array_to_string` funzione descritta più avanti.

Continuando con l&#39;oggetto array dall&#39;alto `organizations` , è possibile scrivere una funzione like `source: array_to_string('_', add_to_array(organizations,"2023"))`, restituendo le organizzazioni di cui una persona è membro nell&#39;anno 2023.

![Esempio di mappatura con funzione add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

In questo caso, il tuo file di output guarda like sotto. Si noti come i tre elementi della matrice sono concatenati in una singola stringa usando il `_` carattere e 2023 viene anche aggiunto alla fine della stringa.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `flattenArray`Funzione per esportare array appiattiti {#flatten-array}

Utilizzare la `flattenArray` funzione per appiattire un array multidimensionale esportato. È possibile combinare questa funzione con la `array_to_string` funzione descritta più avanti.

Continuando con l&#39;oggetto array dall&#39;alto`organizations`, è possibile scrivere una funzione like `array_to_string('_', flattenArray(organizations))`. Si noti che la `array_to_string` funzione appiattisce l&#39;array di input per impostazione predefinita in una stringa.

L&#39;output `array_to_string` risultante è lo stesso della funzione descritta più avanti.

### `coalesce` Funzione per esportare gli array {#coalesce-function-export-arrays}

Utilizzare questa `coalesce` funzione per accesso ed esportare il primo elemento non nullo di una matrice in una stringa.

Ad esempio, è possibile combinare i seguenti campi XDM come mostrato nel schermata di mappatura utilizzando una `coalesce(subscriptions.hasPromotion)` sintassi per restituire il primo `true` valore della `false` matrice:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` array
* `person.name.firstName` corda
* `person.name.lastName` corda
* `personalEmail.address` corda

![Esempio di mappatura con funzione coalesce.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

In questo caso, il tuo file di output guarda like sotto. Si noti come il primo valore non nullo `true` della matrice viene esportato nel file.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` Funzione per esportare gli array {#sizeof-function-export-arrays}

Utilizzare la `size_of` funzione per indicare quanti elementi esistono in un array. Ad esempio, se si dispone di un `purchaseTime` oggetto matrice con più timestamp, è possibile utilizzare la `size_of` funzione per indicare quanti acquisti separati sono stati effettuati da una persona.

Ad esempio, puoi combinare i seguenti campi XDM, come mostrato nel schermata di mappatura.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` array che indica cinque tempi di acquisto separati da parte del cliente
* `personalEmail.address` corda

![Esempio di mappatura con funzione size_of.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In questo caso, il tuo file di output guarda like sotto. Si noti come la seconda colonna indichi il numero di elementi nell&#39;array, corrispondente al numero di acquisti separati effettuati dal cliente.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### accesso di array basati su Index {#index-based-array-access}

>[!IMPORTANT]
>
>A differenza delle altre funzioni descritte in questa pagina, per esportare singoli elementi di una matrice non è *necessario* utilizzare il **[!UICONTROL controllo Campi]** calcolati nella interfaccia.

È possibile accesso un indice di una matrice per esportare un singolo elemento dalla matrice. Ad esempio, simile all&#39;esempio precedente per la `size_of` funzione, se stai cercando di accesso ed esportare solo la prima volta che un cliente ha acquistato un determinato prodotto, puoi utilizzare `purchaseTime[0]` per esportare il primo elemento del timestamp, `purchaseTime[1]` per esportare il secondo elemento del timestamp, `purchaseTime[2]` per esportare il terzo elemento del timestamp,  E così via.

![Esempio di mappatura che mostra come è possibile accedere a un elemento di un array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In questo caso, il file di output ha like di seguito, esportando la prima volta che il cliente ha effettuato un acquisto:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` e `last` funzioni per esportare gli array {#first-and-last-functions-export-arrays}

Utilizzare le `first` funzioni and `last` per esportare il primo o l&#39;ultimo elemento di una matrice. Ad esempio, continuando con l&#39;oggetto `purchaseTime` matrice con più timestamp degli esempi precedenti, è possibile utilizzarli per esportare la prima o l&#39;ultima ora di acquisto effettuata da una persona.

![Esempio di mappatura con la prima e l&#39;ultima funzione.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In questo caso, il file di output ha la like di seguito, esportando la prima e l&#39;ultima volta che il cliente ha effettuato un acquisto:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### Funzioni di hashing {#hashing-functions}

Altre funzioni disponibili sono specifiche per l&#39;esportazione di array o elementi da un array. Potete utilizzare le funzioni di hashing per eseguire l&#39;hashing degli attributi nei file esportati. Ad esempio, se gli attributi contengono informazioni personali identificabili, è possibile eseguire l&#39;hashing di tali campi durante l&#39;esportazione.

È possibile eseguire direttamente l&#39;hashing dei valori stringa, ad esempio `md5(personalEmail.address)`. Se lo si desidera, è anche possibile eseguire l&#39;hashing di singoli elementi dei campi della matrice, supponendo che gli elementi nella matrice siano stringhe, like seguente: `md5(purchaseTime[0])`

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
