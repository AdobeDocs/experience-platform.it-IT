---
title: Tipi e categorie di destinazioni
seo-title: Tipi e categorie di destinazioni
description: 'In Adobe Real-time Customer Data Platform, le destinazioni di esportazione dei profili/segmenti acquisiscono i dati degli eventi, li combinano con altre origini dati, applicano la segmentazione ed esportano segmenti e profili qualificati per destinazioni. Avviate le estensioni per inoltrare i dati degli eventi non elaborati a diversi tipi di destinazioni. '
seo-description: In Adobe Real-time Customer Data Platform, le destinazioni di esportazione dei profili/segmenti acquisiscono i dati degli eventi, li combinano con altre origini dati, applicano la segmentazione ed esportano segmenti e profili qualificati per destinazioni. Avviate le estensioni per inoltrare i dati degli eventi non elaborati a diversi tipi di destinazioni.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Tipi di destinazione e categorie

Leggi questa pagina per comprendere i diversi tipi e categorie di destinazioni Adobe Real-time Customer Data Platform.

## Tipi di destinazione

In Adobe Real-time Customer Data Platform, distinguiamo tra due tipi di destinazione: connessioni ed estensioni. Esistono due tipi di destinazioni di connessione, le destinazioni di esportazione dei profili e le destinazioni di esportazione dei segmenti.

![Tipi di destinazioni](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### Connessioni

**[!UICONTROL Profile Export]** e **[!UICONTROL Segment Export]** le destinazioni in Adobe Real-time Customer Data Platform acquisiscono i dati dell&#39;evento, li combinano con altre origini dati per formare il profilo [cliente in tempo](/help/profile/home.md)reale, applicare segmentazione ed esportare segmenti e profili qualificati per destinazioni.

<br> 

#### Destinazioni di esportazione profilo

Le destinazioni di esportazione dei profili generano un file contenente profili e/o attributi. Queste destinazioni utilizzano dati non elaborati, spesso con l&#39;indirizzo e-mail come chiave primaria. La destinazione [di archiviazione cloud](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 è un esempio di destinazione in cui è possibile depositare i file contenenti esportazioni di profilo.

#### Destinazioni di esportazione dei segmenti

Le destinazioni di esportazione dei segmenti inviano i profili e i segmenti per i quali si sono qualificati alle piattaforme di destinazione. Queste destinazioni utilizzano ID segmento o ID utente. Destinazioni pubblicitarie come [!DNL Google Display & Video 360](/help/rtcdp/destinations/google-dv360-destination.md) o [!DNL Google Ads](/help/rtcdp/destinations/google-ads-destination.md) sono esempi di questi tipi di destinazioni.

#### Destinazioni di esportazione dei profili e dei segmenti - Panoramica video

Il video seguente illustra le particolarità dei due tipi di destinazioni:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### Estensioni

Adobe Real-time CDP sfrutta la potenza e la flessibilità del Experience Platform Launch per includere le estensioni Launch nell&#39;interfaccia Adobe Real-time CDP.

>[!TIP]
>
>Per informazioni dettagliate sulle estensioni di Experience Platform Launch, compresi i casi di utilizzo e come trovarle nell&#39;interfaccia, consultate la panoramica [sulle estensioni di](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Launch.

Avviate le estensioni per inoltrare i dati degli eventi non elaborati a diversi tipi di destinazioni. Considerate le estensioni come un tipo di destinazione di inoltro **** degli eventi. Si tratta di un tipo di integrazione più semplice con le piattaforme di destinazione, che inoltra solo dati di evento non elaborati. Esempi di questi sono l&#39;estensione [di personalizzazione](/help/rtcdp/destinations/gainsight-extension.md) Gainsight o la [voce Conferma dell&#39;estensione](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)del cliente.

![Estensioni Experience Platform Launch confrontate con altre destinazioni](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### Quando utilizzare connessioni ed estensioni

Come esperto di marketing, puoi usare una combinazione di connessioni ed estensioni per risolvere i tuoi casi d&#39;uso.

Le connessioni sono utili quando è necessario sfruttare un profilo cliente centralizzato completo o un segmento cliente per l&#39;attivazione. Ad esempio, utilizza le connessioni se unisci dati comportamentali da un sistema di analisi con dati CRM caricati per qualificare un utente per un determinato segmento prima di inviare un messaggio personalizzato a tale utente.

Le estensioni sono utili quando i dati dell&#39;evento vengono utilizzati per attivare un&#39;azione o per eseguire la segmentazione in un ambiente esterno. Ad esempio, se i dati comportamentali devono essere inoltrati a un sistema esterno senza essere uniti ad altre origini dati sul file per un determinato utente.

<br> 

## Categorie di destinazione

Le connessioni e le estensioni nel catalogo [delle](https://platform.adobe.com/destination/catalog) destinazioni sono raggruppate per categoria di destinazione (**Annuncio**, Archivio **** Cloud, Piattaforme **** per sondaggi, Marketing **tramite** e-mail, ecc.), a seconda del caso di utilizzo del marketing che aiutano a ottenere. Per ulteriori informazioni su ciascuna categoria, nonché sulle destinazioni incluse in ciascuna categoria, consulta la documentazione [del catalogo](/help/rtcdp/destinations/destinations-catalog.md)Destinazioni.

![Categorie di destinazione](/help/rtcdp/destinations/assets/destination-categories-menu.png)

