---
description: Scopri come configurare le opzioni di formattazione dei file quando si attivano i dati nelle destinazioni basate su file
title: (Beta) Configurare le opzioni di formattazione per le destinazioni basate su file
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: b1e9b781f3b78a22b8b977fe08712d2926254e8c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# (Beta) Configurare le opzioni di formattazione per le destinazioni basate su file

>[!IMPORTANT]
>
>La **[!UICONTROL Opzioni di formattazione dei file]** funzionalità in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.
>Contatta il tuo rappresentante di Adobe per accedere a questa funzionalità.
> 
>Le opzioni di formattazione descritte in questo documento sono attualmente disponibili solo per i file CSV.

L&#39;opzione per configurare varie opzioni di formattazione per i file esportati è disponibile quando [connect](/help/destinations/ui/connect-destination.md) a una destinazione basata su file, ad esempio [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [BLOB di Azure](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)oppure [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

È possibile configurare varie opzioni di formattazione per i file esportati utilizzando l’interfaccia utente di Experience Platform. È possibile modificare diverse proprietà dei file esportati in modo che corrispondano ai requisiti del sistema di ricezione dei file sul proprio lato, al fine di leggere e interpretare in modo ottimale i file ricevuti da Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configurazione della formattazione dei file per i file CSV {#file-configuration}

Per visualizzare le opzioni di formattazione del file, avvia la [connessione a destinazione](/help/destinations/ui/connect-destination.md) workflow. Seleziona **Tipo di dati: Segmenti** e **Tipo di file: CSV** per visualizzare le impostazioni di formattazione disponibili per l&#39;esportazione `CSV` file.

>[!IMPORTANT]
>
>La destinazione a cui ci si connette potrebbe non disporre di tutte queste opzioni. Spetta allo sviluppatore di destinazione determinare le opzioni di formattazione dei file che desiderano supportare nella destinazione. Lo sviluppatore di destinazione può determinare quali opzioni sono disponibili quando si effettua la connessione alla destinazione. Le opzioni richieste sono contrassegnate da un asterisco nell’interfaccia utente di Experience Platform.
> 
>Le nuove destinazioni di archiviazione cloud: [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [BLOB di Azure (Beta)](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - al momento supporta solo le sei opzioni CSV evidenziate di seguito.

![Immagine che mostra alcune delle opzioni di formattazione disponibili.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitatore {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="Delimitatore"
>abstract="Utilizzare questo controllo per impostare un separatore per ciascun campo e valore. Visualizza la documentazione relativa agli esempi per ogni selezione."

Usa questo controllo per impostare un separatore per ciascun campo e valore nei file CSV esportati. Le opzioni disponibili sono:

* Due punti `(:)`
* Virgola `(,)`
* Barra verticale `(|)`
* Punto e virgola `(;)`
* Tab `(\t)`

#### Esempi

Di seguito sono riportati alcuni esempi del contenuto dei file CSV esportati, con ciascuna selezione nell’interfaccia utente.

* Esempio di output con **[!UICONTROL Due punti`(:)`]** selezionato: `male:John:Doe`
* Esempio di output con **[!UICONTROL Virgola`(,)`]** selezionato: `male,John,Doe`
* Esempio di output con **[!UICONTROL Tubo`(|)`]** selezionato: `male|John|Doe`
* Esempio di output con **[!UICONTROL Punto e virgola`(;)`]** selezionato: `male;John;Doe`
* Esempio di output con **[!UICONTROL Scheda`(\t)`]** selezionato: `male \t John \t Doe`

### Carattere di citazione {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="Carattere di citazione"
>abstract="Utilizzare questa opzione se si desidera rimuovere le virgolette doppie dalle stringhe esportate. Visualizza la documentazione relativa agli esempi per ogni selezione."

Utilizzare questa opzione se si desidera rimuovere le virgolette doppie dalle stringhe esportate. Le opzioni disponibili sono:

* **[!UICONTROL Carattere Null (\0000)]**. Utilizza questa opzione per rimuovere le virgolette doppie dai file CSV esportati.
* **[!UICONTROL Virgolette doppie (&quot;)]**. Utilizza questa opzione per mantenere le virgolette doppie nei file CSV esportati.

#### Esempi

Di seguito sono riportati alcuni esempi del contenuto dei file CSV esportati, con ciascuna selezione nell’interfaccia utente.

* Esempio di output con **[!UICONTROL Carattere Null (\0000)]** selezionato: `Test,John,LastName`
* Esempio di output con **[!UICONTROL Virgolette doppie (&quot;)]** selezionato: `"Test","John","LastName"`

### Carattere di escape {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="Carattere di escape"
>abstract="Imposta un singolo carattere utilizzato per l&#39;escape delle virgolette all&#39;interno di un valore già citato. Visualizza la documentazione relativa agli esempi per ogni selezione."

Utilizzare questa opzione per impostare un singolo carattere per l&#39;escape delle virgolette all&#39;interno di un valore già citato. Ad esempio, questa opzione è utile quando una stringa è racchiusa tra virgolette doppie in cui parte della stringa è già racchiusa tra virgolette doppie. Questa opzione determina con quale carattere sostituire le virgolette doppie interne. Le opzioni disponibili sono:

* Barra rovesciata `(\)`
* Virgoletta singola `(')`

#### Esempi

Di seguito sono riportati alcuni esempi del contenuto dei file CSV esportati, con ciascuna selezione nell’interfaccia utente.

* Esempio di output con **[!UICONTROL Barra rovesciata`(\)`]** selezionato: `"Test,\"John\",LastName"`
* Esempio di output con **[!UICONTROL Virgoletta singola`(')`]** selezionato: `"Test,'"John'",LastName"`

### Output valore vuoto {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="Output valore vuoto"
>abstract="Utilizza questa opzione per impostare come devono essere rappresentati i valori vuoti nei file CSV esportati. Visualizza la documentazione relativa agli esempi per ogni selezione."

Utilizzare questo controllo per impostare la rappresentazione stringa di un valore vuoto. Questa opzione determina il modo in cui i valori vuoti vengono rappresentati nei file CSV esportati. Le opzioni disponibili sono:

* **[!UICONTROL null]**
* **&quot;&quot;**
* **[!UICONTROL Stringa vuota]**

#### Esempi

Di seguito sono riportati alcuni esempi del contenuto dei file CSV esportati, con ciascuna selezione nell’interfaccia utente.

* Esempio di output con **[!UICONTROL null]** selezionato: `male,NULL,TestLastName`. In questo caso, Experience Platform trasforma il valore vuoto in un valore null.
* Esempio di output con **&quot;&quot;** selezionato: `male,"",TestLastName`. In questo caso, Experience Platform trasforma il valore vuoto in una coppia di virgolette doppie.
* Esempio di output con **[!UICONTROL Stringa vuota]** selezionato: `male,,TestLastName`. In questo caso, l’Experience Platform mantiene il valore vuoto ed lo esporta così com’è (senza virgolette doppie).

>[!TIP]
>
>La differenza tra l&#39;output del valore vuoto e l&#39;output del valore nullo nella sezione seguente è che un valore vuoto ha un valore effettivo vuoto. Il valore NULL non ha alcun valore. Considera il valore vuoto come un vetro vuoto sulla tabella e il valore nullo come non avere il vetro affatto sulla tavola.

### Output valore Null {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Output valore Null"
>abstract="Utilizzare questo controllo per impostare la rappresentazione stringa di un valore null all&#39;interno dei file esportati. Visualizza la documentazione relativa agli esempi per ogni selezione."

Utilizzare questo controllo per impostare la rappresentazione stringa di un valore null all&#39;interno dei file esportati. Questa opzione determina il modo in cui i valori nulli vengono rappresentati nei file CSV esportati. Le opzioni disponibili sono:

* **[!UICONTROL null]**
* **&quot;&quot;**
* **[!UICONTROL Stringa vuota]**

#### Esempi

Di seguito sono riportati alcuni esempi del contenuto dei file CSV esportati, con ciascuna selezione nell’interfaccia utente.

* Esempio di output con **[!UICONTROL null]** selezionato: `male,NULL,TestLastName`. In questo caso, non si verifica alcuna trasformazione e il file CSV contiene il valore null.
* Esempio di output con **&quot;&quot;** selezionato: `male,"",TestLastName`. In questo caso, l&#39;Experience Platform sostituisce il valore nullo con virgolette doppie intorno a una stringa vuota.
* Esempio di output con **[!UICONTROL Stringa vuota]** selezionato: `male,,TestLastName`. In questo caso, l&#39;Experience Platform sostituisce il valore null con una stringa vuota (senza virgolette doppie).

### Formato di compressione {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="Formato di compressione"
>abstract="Imposta il tipo di compressione da utilizzare per il salvataggio dei dati nel file. Le opzioni supportate sono GZIP e NONE. Visualizza la documentazione relativa agli esempi per ogni selezione."

Imposta il tipo di compressione da utilizzare per il salvataggio dei dati nel file. Le opzioni supportate sono GZIP e NONE. Questa opzione determina se esportare o meno i file compressi.

### Codifica

*Non mostrato nella schermata dell’interfaccia utente*. Specifica la codifica (charset) dei file CSV salvati. Le opzioni sono UTF-8 o UTF-16.

### Char per evitare il preventivo

*Non mostrato nella schermata dell’interfaccia utente*. Flag che indica se i valori contenenti virgolette devono sempre essere racchiusi tra virgolette.

L&#39;impostazione predefinita prevede l&#39;escape di tutti i valori contenenti un carattere di virgolette.

### Separatore di riga

*Non mostrato nella schermata dell’interfaccia utente*. Definisce il separatore di riga da utilizzare per la scrittura. La lunghezza massima è di 1 carattere.

### Ignora spazi vuoti iniziali

*Non mostrato nella schermata dell’interfaccia utente*. Un flag che indica se gli spazi bianchi iniziali dai valori da esportare devono essere ignorati o meno.

Esempio di output con **[!UICONTROL True]** selezionato: `"male","John","TestLastName"`
Esempio di output con **[!UICONTROL False]** selezionato: `" male","John","TestLastName"`

### Ignora spazi vuoti finali

Non viene visualizzato nella schermata dell’interfaccia utente. Un flag che indica se gli spazi bianchi finali dei valori da esportare devono essere ignorati o meno.

Esempio di output con **[!UICONTROL True]** selezionato: `"male","John","TestLastName"`
Esempio di output con **[!UICONTROL False]** selezionato: `"male ","John","TestLastName"`

### Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come configurare le opzioni di esportazione dei file per i file di dati CSV per adattare il contenuto dei file ai requisiti del sistema di ricezione dei file a valle. Successivamente, puoi leggere il [esercitazione sull&#39;attivazione delle destinazioni basate su file](/help/destinations/ui/activate-batch-profile-destinations.md) per iniziare l&#39;esportazione dei file nel percorso di archiviazione cloud desiderato.
