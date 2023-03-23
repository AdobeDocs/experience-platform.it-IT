---
description: Scopri come configurare le opzioni di formattazione dei file quando si attivano i dati nelle destinazioni basate su file
title: (Beta) Configurare le opzioni di formattazione per le destinazioni basate su file
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 379a3769965bb425ca2c8df195b99a98f0b5398d
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

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

## Configurazione della formattazione dei file {#file-configuration}

Per visualizzare le opzioni di formattazione del file, avvia la [connessione a destinazione](/help/destinations/ui/connect-destination.md) workflow. Seleziona **Tipo di dati: Segmenti** e **Tipo di file: CSV** per visualizzare le impostazioni di formattazione disponibili per l&#39;esportazione `CSV` file.

>[!IMPORTANT]
>
>La destinazione a cui ci si connette potrebbe non disporre di tutte queste opzioni. Spetta allo sviluppatore di destinazione determinare le opzioni di formattazione dei file che desiderano supportare nella destinazione. Lo sviluppatore di destinazione può determinare quali opzioni sono disponibili quando si effettua la connessione alla destinazione. Le opzioni richieste sono contrassegnate da un asterisco nell’interfaccia utente di Experience Platform.
> 
>Le nuove destinazioni di archiviazione cloud: [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [BLOB di Azure (Beta)](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - al momento supporta solo le sei opzioni CSV evidenziate di seguito.

![Immagine che mostra alcune delle opzioni di formattazione disponibili.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitatore {#delimiter}

Imposta un separatore per ciascun campo e valore. Le opzioni disponibili sono:

* Due punti `(:)`
* Virgola `(,)`
* Barra verticale `(|)`
* Punto e virgola `(;)`
* Tab `(\t)`

### Carattere di citazione

Imposta un singolo carattere utilizzato per l&#39;escape dei valori tra virgolette in cui il separatore può far parte del valore.

### Carattere di escape

Imposta un singolo carattere utilizzato per l&#39;escape delle virgolette all&#39;interno di un valore già citato.

### Output valore vuoto

Imposta la rappresentazione stringa di un valore vuoto.

### Output valore Null

Imposta la rappresentazione stringa di un valore nullo all’interno dei file esportati.

Esempio di output con **[!UICONTROL null]** selezionato: `male,NULL,TestLastName`
Esempio di output con **&quot;&quot;** selezionato: `male,"",TestLastName`
Esempio di output con **[!UICONTROL Stringa vuota]** selezionato: `male,,TestLastName`

### Formato di compressione

Imposta il codec di compressione da utilizzare per il salvataggio dei dati su file. Le opzioni supportate sono GZIP e NONE.

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
