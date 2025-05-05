---
description: Scopri come configurare le opzioni di formattazione dei file quando si attivano i dati verso destinazioni basate su file
title: Configurare le opzioni di formattazione dei file per le destinazioni basate su file
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 4dd6e8685ff5cc61342b20e971216416918b95da
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 17%

---

# Configurare le opzioni di formattazione dei file per le destinazioni basate su file

>[!IMPORTANT]
> 
>Le opzioni di formattazione dei file descritte in questo documento sono attualmente disponibili solo per i file CSV.

L&#39;opzione per configurare varie opzioni di formattazione dei file per i file esportati è disponibile quando ci [si connette](/help/destinations/ui/connect-destination.md) a una destinazione basata su file, ad esempio [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [BLOB](/help/destinations/catalog/cloud-storage/azure-blob.md#connect) di Azure o [SFTP.](/help/destinations/catalog/cloud-storage/sftp.md#connect)

È possibile configurare diverse opzioni di formattazione dei file esportati utilizzando la interfaccia Experience Platform. È possibile modificare diverse proprietà dei file esportati per soddisfare i requisiti del sistema di ricezione file dalla propria parte, al fine di leggere e interpretare in modo ottimale i file ricevuti da Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## File configurazione di formattazione per i file CSV {#file-configuration}

Per visualizzare le opzioni di formattazione dei file, avviare l&#39;workflow [di connessione alla destinazione](/help/destinations/ui/connect-destination.md) . Selezionare **Tipo di** dati: Segmenti e **File tipo: CSV** per visualizzare le impostazioni di formattazione dei file disponibili per i file esportati `CSV` .

>[!IMPORTANT]
>
>La destinazione a cui ci si connette potrebbe non avere tutte queste opzioni disponibili. Spetta allo sviluppatore di destinazione determinare quali opzioni di formattazione dei file desidera supportare nella propria destinazione. Lo sviluppatore di destinazione può determinare quali opzioni sono disponibili per la connessione alla destinazione. Le opzioni obbligatorie sono contrassegnate da un asterisco nella Experience Platform interfaccia.
> 
>Le destinazioni di archiviazione cloud create da Adobe Systems - [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - supportano attualmente solo le sei opzioni CSV evidenziate di seguito.

![Immagine vengono visualizzate alcune delle opzioni di formattazione dei file disponibili.](../assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitatore {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="Delimitatore"
>abstract="Utilizza questo controllo per impostare un separatore per ciascun campo e valore. Consulta la documentazione per vedere degli esempi di ogni selezione."

Utilizza questo controllo per impostare un separatore per ogni campo e valore nei file CSV esportati. Le opzioni disponibili sono:

* Colon `(:)`
* Virgola `(,)`
* Pipa `(|)`
* Punto e virgola `(;)`
* Scheda `(\t)`

#### Esempi

Visualizza gli esempi seguenti delle contenuto nei file CSV esportati, con ciascuna delle selezioni nella interfaccia.

* Esempio di output con **[!UICONTROL due`(:)`]** punti selezionati: `male:John:Doe`
* Esempio di output con **[!UICONTROL la virgola`(,)`]** selezionata: `male,John,Doe`
* Esempio di uscita con **[!UICONTROL barra verticale`(|)`]** selezionata: `male|John|Doe`
* Esempio di output con **[!UICONTROL punto e virgola`(;)`]** selezionato: `male;John;Doe`
* Esempio di output con **[!UICONTROL la scheda`(\t)`]** selezionata: `male \t John \t Doe`

### Carattere virgolette {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="Carattere virgolette"
>abstract="Utilizza questa opzione se desideri rimuovere le virgolette doppie dalle stringhe esportate. Consulta la documentazione per vedere degli esempi di ogni selezione."

Utilizzare questa opzione per controllare se le virgolette doppie devono essere rimosse o mantenute all&#39;interno delle stringhe esportate.

Le opzioni disponibili sono le seguenti:

* **[!UICONTROL Null Carattere (\0000).]** Utilizza questa opzione per rimuovere le virgolette doppie dai file CSV esportati.
* **[!UICONTROL Virgolette doppie (&quot;)]**. Utilizzare questa opzione quando i valori stringa contengono un delimitatore o virgolette doppie. Questa opzione consente di mantenere i delimitatori o le virgolette doppie nei file CSV esportati, in modo da poter identificare correttamente quale valore corrisponde a quale campo.

#### Esempi

Considera il valore `Anna,"Doe,John"`di input .

Visualizza gli esempi seguenti dei contenuto dai file CSV esportati con ciascuna delle selezioni nella interfaccia.

* Esempio di output con **[!UICONTROL Carattere null (\0000)]** selezionato: `Anna,Doe,John`
* Esempio di output con **[!UICONTROL virgolette doppie (&quot;)]** selezionate: `Anna,"Doe,John"`

### Carattere di escape {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="Carattere di escape"
>abstract="Imposta un singolo carattere utilizzato per eseguire l’escape delle virgolette all’interno di un valore già tra virgolette. Consulta la documentazione per vedere degli esempi di ogni selezione."

Utilizzare questa opzione per impostare un singolo carattere per le virgolette di escape all&#39;interno di un valore già citato. Ad esempio, questa opzione è utile quando si dispone di una stringa racchiusa tra virgolette doppie in cui parte della stringa è già racchiusa tra virgolette doppie. Questa opzione determina con quale carattere sostituire le virgolette doppie interne. Le opzioni disponibili sono:

* Indietro barra `(\)`
* Citazione singola `(')`

#### Esempi

Visualizza gli esempi seguenti dei contenuto dai file CSV esportati con ciascuna delle selezioni nella interfaccia.

* Esempio di output con **[!UICONTROL Indietro barra`(\)`]** selezionata: `"Test,\"John\",LastName"`
* Esempio di output con **[!UICONTROL virgolette`(')`]** singole selezionate: `"Test,'"John'",LastName"`

### Output valore vuoto {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="Output valore vuoto"
>abstract="Utilizza questa opzione per impostare come devono essere rappresentati i valori vuoti nei file CSV esportati. Consulta la documentazione per vedere degli esempi di ogni selezione."

Utilizzare questo controllo per impostare la rappresentazione in forma di stringa di un valore vuoto. Questa opzione determina il modo in cui i valori vuoti vengono rappresentati nei file CSV esportati. Le opzioni disponibili sono:

* **[!UICONTROL Null (null)]**
* **stringa vuota tra virgolette doppie (&quot;&quot;)**
* **[!UICONTROL Stringa vuota]**

#### Esempi

Visualizza gli esempi seguenti dei contenuto dai file CSV esportati con ciascuna delle selezioni nella interfaccia.

* Esempio di output con **[!UICONTROL null]** selezionato: `male,NULL,TestLastName`. In questo caso, Experience Platform trasforma il valore vuoto in valore null.
* Esempio di output con **&quot;&quot;** selezionato: `male,"",TestLastName`. In questo caso, Experience Platform trasforma il valore vuoto in una coppia di virgolette doppie.
* Esempio di output con **[!UICONTROL stringa vuota]** selezionata: `male,,TestLastName`. In questo caso, il Experience Platform mantiene il valore vuoto e lo esporta così com&#39;è (senza virgolette).

>[!TIP]
>
>La differenza tra l&#39;output del valore vuoto e l&#39;output del valore nullo nella sezione seguente è che un valore vuoto ha un valore effettivo vuoto. Il valore NULL non ha alcun valore. Pensa al valore vuoto come a un bicchiere vuoto sul tavolo e al valore nullo come a non avere affatto il bicchiere sul tavolo.

### Output valore nullo {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Output valore nullo"
>abstract="Utilizza questo controllo per impostare la rappresentazione stringa di un valore nullo all’interno dei file esportati. Consulta la documentazione per vedere degli esempi di ogni selezione."

Utilizza questo controllo per impostare la rappresentazione stringa di un valore nullo all’interno dei file esportati. Questa opzione determina in che modo i valori nulli sono rappresentati nei file CSV esportati. Le opzioni disponibili sono:

* **[!UICONTROL Null (null)]**
* **stringa vuota tra virgolette doppie (&quot;&quot;)**
* **[!UICONTROL Stringa vuota]**

#### Esempi

Visualizza gli esempi seguenti dei contenuto dai file CSV esportati con ciascuna delle selezioni nella interfaccia.

* Esempio di output con **[!UICONTROL null]** selezionato: `male,NULL,TestLastName`. In questo caso, non si verifica alcuna trasformazione e il file CSV contiene il valore null.
* Esempio di output con **&quot;&quot;** selezionato: `male,"",TestLastName`. In questo caso, Experience Platform sostituisce il valore null con virgolette doppie intorno a una stringa vuota.
* Esempio di output con **[!UICONTROL stringa vuota]** selezionata: `male,,TestLastName`. In questo caso, Experience Platform sostituisce il valore null con una stringa vuota (senza virgolette doppie).

### Formato di compressione {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="Formato di compressione"
>abstract="Imposta il tipo di compressione da utilizzare per il salvataggio dei dati nel file. Le opzioni supportate sono GZIP e NONE. Consulta la documentazione per vedere degli esempi di ogni selezione."

Imposta il tipo di compressione da utilizzare per il salvataggio dei dati nel file. Le opzioni supportate sono GZIP e NONE. Questa opzione determina se esportare o meno i file compressi.

### Codifica

*Non visualizzata nella schermata interfaccia*. Specifica la codifica (set di caratteri) dei file CSV salvati. Opzioni sono UTF-8 o UTF-16.

### Char per evitare citazione

*Non visualizzata nella schermata interfaccia*. Un contrassegno che indica se i valori contenenti virgolette devono sempre essere racchiusi tra virgolette.

Per impostazione predefinita viene escape tutti i valori contenenti virgolette.

### Separatore di linea

*Non visualizzata nella schermata interfaccia*. Definisce il separatore di riga da utilizzare per scrivere. La lunghezza massima è di 1 carattere.

### Ignora spazi vuoti iniziali

*Non visualizzata nella schermata interfaccia*. Una contrassegno che indica se ignorare o meno gli spazi vuoti iniziali dei valori esportati.

Esempio di output con **[!UICONTROL True]** selezionato: `"male","John","TestLastName"`
Esempio di output con **[!UICONTROL false]** selezionata: `" male","John","TestLastName"`

### Ignora spazi vuoti finali

Non visualizzata nella schermata interfaccia. Una contrassegno che indica se ignorare o meno gli spazi vuoti finali dei valori esportati.

Esempio di output con **[!UICONTROL True]** selezionato: `"male","John","TestLastName"`
Esempio di output con **[!UICONTROL false]** selezionata: `"male ","John","TestLastName"`

### Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come configurare le opzioni di esportazione dei file per i tuoi file di dati CSV per adattare il contenuto del file ai requisiti del tuo sistema di ricezione dei file a valle. Successivo, è possibile leggere il esercitazione[&#128279;](/help/destinations/ui/activate-batch-profile-destinations.md) di attivazione delle destinazioni basate su file per avviare l&#39;esportazione dei file nella posizione di archiviazione cloud preferita.
