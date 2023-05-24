---
description: Scopri come configurare le opzioni di formattazione dei file quando si attivano i dati in destinazioni basate su file
title: (Beta) Configurare le opzioni di formattazione dei file per le destinazioni basate su file
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: b1e9b781f3b78a22b8b977fe08712d2926254e8c
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 19%

---

# (Beta) Configurare le opzioni di formattazione dei file per le destinazioni basate su file

>[!IMPORTANT]
>
>Il **[!UICONTROL Opzioni di formattazione del file]** funzionalità in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.
>Contatta il rappresentante del tuo Adobe per accedere a questa funzionalità.
> 
>Le opzioni di formattazione descritte in questo documento sono attualmente disponibili solo per i file CSV.

L&#39;opzione per configurare varie opzioni di formattazione per i file esportati è disponibile quando [connetti](/help/destinations/ui/connect-destination.md) in una destinazione basata su file, ad esempio [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [BLOB di Azure](/help/destinations/catalog/cloud-storage/azure-blob.md#connect), o [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Puoi configurare varie opzioni di formattazione per i file esportati utilizzando l’interfaccia utente di Experience Platform. È possibile modificare diverse proprietà dei file esportati in modo che corrispondano ai requisiti del sistema di ricezione dei file sul proprio lato, al fine di leggere e interpretare in modo ottimale i file ricevuti da Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configurazione della formattazione dei file per i file CSV {#file-configuration}

Per visualizzare le opzioni di formattazione del file, avviare [connetti alla destinazione](/help/destinations/ui/connect-destination.md) flusso di lavoro. Seleziona **Tipo di dati: Segmenti** e **Tipo di file: CSV** per visualizzare le impostazioni di formattazione del file disponibili per il file esportato `CSV` file.

>[!IMPORTANT]
>
>È possibile che nella destinazione a cui ci si connette non siano disponibili tutte queste opzioni. Spetta allo sviluppatore di destinazione determinare le opzioni di formattazione dei file da supportare nella destinazione. Lo sviluppatore di destinazione può determinare quali opzioni sono disponibili quando si connette alla destinazione. Le opzioni obbligatorie sono contrassegnate da un asterisco nell’interfaccia utente di Experience Platform.
> 
>Le nuove destinazioni dell&#39;archiviazione cloud - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) BLOB di Azure](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Archiviazione Azure Data Lake Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Data Landing Zone (Beta)](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP (beta)](/help/destinations/catalog/cloud-storage/sftp.md) : attualmente supporta solo le sei opzioni CSV evidenziate di seguito.

![Immagine che mostra alcune delle opzioni di formattazione disponibili per il file.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitatore {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="Delimitatore"
>abstract="Utilizza questo controllo per impostare un separatore per ciascun campo e valore. Consulta la documentazione per vedere degli esempi di ogni selezione."

Utilizzare questo controllo per impostare un separatore per ogni campo e valore nei file CSV esportati. Le opzioni disponibili sono:

* Due punti `(:)`
* Virgola `(,)`
* Barra verticale `(|)`
* Punto e virgola `(;)`
* Tab `(\t)`

#### Esempi

Visualizza gli esempi seguenti dei contenuti dei file CSV esportati con ciascuna selezione nell’interfaccia utente.

* Output di esempio con **[!UICONTROL Due punti`(:)`]** selezionato: `male:John:Doe`
* Output di esempio con **[!UICONTROL Virgola`(,)`]** selezionato: `male,John,Doe`
* Output di esempio con **[!UICONTROL Tubo`(|)`]** selezionato: `male|John|Doe`
* Output di esempio con **[!UICONTROL Punto e virgola`(;)`]** selezionato: `male;John;Doe`
* Output di esempio con **[!UICONTROL Linguetta`(\t)`]** selezionato: `male \t John \t Doe`

### Carattere virgolette {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="Carattere virgolette"
>abstract="Utilizza questa opzione se desideri rimuovere le virgolette doppie dalle stringhe esportate. Consulta la documentazione per vedere degli esempi di ogni selezione."

Utilizza questa opzione se desideri rimuovere le virgolette doppie dalle stringhe esportate. Le opzioni disponibili sono:

* **[!UICONTROL Carattere nullo (\0000)]**. Utilizza questa opzione per rimuovere le virgolette doppie dai file CSV esportati.
* **[!UICONTROL Virgolette doppie (&quot;)]**. Utilizza questa opzione per conservare le virgolette doppie nei file CSV esportati.

#### Esempi

Visualizza gli esempi seguenti del contenuto dei file CSV esportati con ciascuna selezione nell’interfaccia utente.

* Output di esempio con **[!UICONTROL Carattere nullo (\0000)]** selezionato: `Test,John,LastName`
* Output di esempio con **[!UICONTROL Virgolette doppie (&quot;)]** selezionato: `"Test","John","LastName"`

### Carattere di escape {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="Carattere di escape"
>abstract="Imposta un singolo carattere utilizzato per eseguire l’escape delle virgolette all’interno di un valore già tra virgolette. Consulta la documentazione per vedere degli esempi di ogni selezione."

Utilizzare questa opzione per impostare un singolo carattere per l&#39;escape delle virgolette all&#39;interno di un valore già citato. Questa opzione è utile, ad esempio, quando si dispone di una stringa racchiusa tra virgolette doppie in cui parte della stringa è già racchiusa tra virgolette doppie. Questa opzione determina il carattere con cui sostituire le virgolette doppie interne. Le opzioni disponibili sono:

* Barra indietro `(\)`
* Virgoletta singola `(')`

#### Esempi

Visualizza gli esempi seguenti del contenuto dei file CSV esportati con ciascuna selezione nell’interfaccia utente.

* Output di esempio con **[!UICONTROL Barra indietro`(\)`]** selezionato: `"Test,\"John\",LastName"`
* Output di esempio con **[!UICONTROL Virgoletta singola`(')`]** selezionato: `"Test,'"John'",LastName"`

### Output valore vuoto {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="Output valore vuoto"
>abstract="Utilizza questa opzione per impostare come devono essere rappresentati i valori vuoti nei file CSV esportati. Consulta la documentazione per vedere degli esempi di ogni selezione."

Utilizzare questo controllo per impostare la rappresentazione di stringa di un valore vuoto. Questa opzione determina il modo in cui i valori vuoti vengono rappresentati nei file CSV esportati. Le opzioni disponibili sono:

* **[!UICONTROL null]**
* **&quot;&quot;**
* **[!UICONTROL Stringa vuota]**

#### Esempi

Visualizza gli esempi seguenti del contenuto dei file CSV esportati con ciascuna selezione nell’interfaccia utente.

* Output di esempio con **[!UICONTROL nulle]** selezionato: `male,NULL,TestLastName`. In questo caso, Experience Platform trasforma il valore vuoto in un valore nullo.
* Output di esempio con **&quot;&quot;** selezionato: `male,"",TestLastName`. In questo caso, Experience Platform trasforma il valore vuoto in una coppia di virgolette.
* Output di esempio con **[!UICONTROL Stringa vuota]** selezionato: `male,,TestLastName`. In questo caso, l’Experience Platform mantiene il valore vuoto e lo esporta così com’è (senza virgolette doppie).

>[!TIP]
>
>La differenza tra l’output di un valore vuoto e l’output di un valore nullo nella sezione seguente è che un valore vuoto ha un valore effettivo vuoto. Il valore NULL non ha alcun valore. Considera il valore vuoto come un bicchiere vuoto sul tavolo e il valore nullo come se il bicchiere non fosse affatto sul tavolo.

### Output valore nullo {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Output valore nullo"
>abstract="Utilizza questo controllo per impostare la rappresentazione stringa di un valore nullo all’interno dei file esportati. Consulta la documentazione per vedere degli esempi di ogni selezione."

Utilizza questo controllo per impostare la rappresentazione stringa di un valore nullo all’interno dei file esportati. Questa opzione determina il modo in cui i valori Null vengono rappresentati nei file CSV esportati. Le opzioni disponibili sono:

* **[!UICONTROL null]**
* **&quot;&quot;**
* **[!UICONTROL Stringa vuota]**

#### Esempi

Visualizza gli esempi seguenti del contenuto dei file CSV esportati con ciascuna selezione nell’interfaccia utente.

* Output di esempio con **[!UICONTROL nulle]** selezionato: `male,NULL,TestLastName`. In questo caso, non si verifica alcuna trasformazione e il file CSV contiene il valore null.
* Output di esempio con **&quot;&quot;** selezionato: `male,"",TestLastName`. In questo caso, Experience Platform sostituisce il valore null con virgolette doppie intorno a una stringa vuota.
* Output di esempio con **[!UICONTROL Stringa vuota]** selezionato: `male,,TestLastName`. In questo caso, Experience Platform sostituisce il valore null con una stringa vuota (senza virgolette doppie).

### Formato di compressione {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="Formato di compressione"
>abstract="Imposta il tipo di compressione da utilizzare per il salvataggio dei dati nel file. Le opzioni supportate sono GZIP e NONE. Consulta la documentazione per vedere degli esempi di ogni selezione."

Imposta il tipo di compressione da utilizzare per il salvataggio dei dati nel file. Le opzioni supportate sono GZIP e NONE. Questa opzione determina se esportare o meno i file compressi.

### Codifica

*Non visualizzato nella schermata dell’interfaccia utente*. Specifica la codifica (charset) dei file CSV salvati. Le opzioni sono UTF-8 o UTF-16.

### Carattere per virgolette di escape

*Non visualizzato nella schermata dell’interfaccia utente*. Flag che indica se i valori contenenti virgolette devono sempre essere racchiusi tra virgolette.

L&#39;impostazione predefinita prevede l&#39;escape di tutti i valori contenenti una virgoletta.

### Separatore di righe

*Non visualizzato nella schermata dell’interfaccia utente*. Definisce il separatore di riga da utilizzare per la scrittura. La lunghezza massima è di 1 carattere.

### Ignora spazio vuoto iniziale

*Non visualizzato nella schermata dell’interfaccia utente*. Un flag che indica se gli spazi vuoti iniziali dei valori esportati devono essere ignorati o meno.

Output di esempio con **[!UICONTROL Vero]** selezionato: `"male","John","TestLastName"`
Output di esempio con **[!UICONTROL Falso]** selezionato: `" male","John","TestLastName"`

### Ignora spazio vuoto finale

Non visualizzato nella schermata dell’interfaccia utente. Un flag che indica se gli spazi vuoti finali dei valori esportati devono essere ignorati o meno.

Output di esempio con **[!UICONTROL Vero]** selezionato: `"male","John","TestLastName"`
Output di esempio con **[!UICONTROL Falso]** selezionato: `"male ","John","TestLastName"`

### Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come configurare le opzioni di esportazione dei file per i file di dati CSV per adattare il contenuto dei file ai requisiti del sistema di ricezione dei file a valle. Quindi, puoi leggere [tutorial sull’attivazione delle destinazioni basate su file](/help/destinations/ui/activate-batch-profile-destinations.md) per iniziare a esportare i file nel percorso di archiviazione cloud preferito.
