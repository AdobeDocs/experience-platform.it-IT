---
description: Scopri come configurare le opzioni di formattazione dei file quando si attivano i dati in destinazioni basate su file
title: (Beta) Configurare le opzioni di formattazione dei file per le destinazioni basate su file
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 14ce4a11f53ef24b3008b3f775cc926d05ea8f8e
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

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

## Configurazione formattazione file {#file-configuration}

Per visualizzare le opzioni di formattazione del file, avviare [connetti alla destinazione](/help/destinations/ui/connect-destination.md) flusso di lavoro. Seleziona **Tipo di dati: Segmenti** e **Tipo di file: CSV** per visualizzare le impostazioni di formattazione del file disponibili per il file esportato `CSV` file.

>[!IMPORTANT]
>
>È possibile che nella destinazione a cui ci si connette non siano disponibili tutte queste opzioni. Spetta allo sviluppatore di destinazione determinare le opzioni di formattazione dei file da supportare nella destinazione. Lo sviluppatore di destinazione può determinare quali opzioni sono disponibili quando si connette alla destinazione. Le opzioni obbligatorie sono contrassegnate da un asterisco nell’interfaccia utente di Experience Platform.
> 
>Le nuove destinazioni dell&#39;archiviazione cloud - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) BLOB di Azure](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Archiviazione Azure Data Lake Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Data Landing Zone (Beta)](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP (beta)](/help/destinations/catalog/cloud-storage/sftp.md) : attualmente supporta solo le sei opzioni CSV evidenziate di seguito.

![Immagine che mostra alcune delle opzioni di formattazione disponibili per il file.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitatore {#delimiter}

Imposta un separatore per ogni campo e valore. Le opzioni disponibili sono:

* Due punti `(:)`
* Virgola `(,)`
* Barra verticale `(|)`
* Punto e virgola `(;)`
* Tab `(\\t)`

### Virgoletta

Imposta un singolo carattere utilizzato per l&#39;escape dei valori tra virgolette, in cui il separatore può far parte del valore.

### Carattere di escape

Imposta un singolo carattere utilizzato per l&#39;escape delle virgolette all&#39;interno di un valore già citato.

### Output valore vuoto

Imposta la rappresentazione di stringa di un valore vuoto.

### Output valore nullo

Imposta la rappresentazione di stringa di un valore null all&#39;interno dei file esportati.

Output di esempio con **[!UICONTROL nulle]** selezionato: `male,NULL,TestLastName`
Output di esempio con **&quot;&quot;** selezionato: `male,"",TestLastName`
Output di esempio con **[!UICONTROL Stringa vuota]** selezionato: `male,,TestLastName`

### Formato di compressione

Imposta il codec di compressione da utilizzare per il salvataggio dei dati in un file. Le opzioni supportate sono GZIP e NONE.

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
