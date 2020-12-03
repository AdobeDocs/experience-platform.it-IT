---
keywords: destinations;destination;destination types
title: Tipi e categorie di destinazioni
seo-title: Tipi e categorie di destinazioni
description: 'In Real-time Customer Data Platform (Piattaforma dati cliente in tempo reale), le destinazioni di esportazione profilo/segmento acquisiscono i dati dell''evento, li combinano con altre origini dati, applicano la segmentazione ed esportano segmenti e profili qualificati per destinazioni. Le estensioni di Experience Platform Launch inoltrano i dati dell''evento non elaborati a diversi tipi di destinazioni. '
seo-description: In Real-time Customer Data Platform (Piattaforma dati cliente in tempo reale), le destinazioni di esportazione profilo/segmento acquisiscono i dati dell'evento, li combinano con altre origini dati, applicano la segmentazione ed esportano segmenti e profili qualificati per destinazioni. Le estensioni di Experience Platform Launch inoltrano i dati dell'evento non elaborati a diversi tipi di destinazioni.
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Tipi di destinazione e categorie

Leggi questa pagina per comprendere i diversi tipi e categorie di destinazioni della piattaforma dati cliente in tempo reale.

## Tipi di destinazione

In Real-time Customer Data Platform, distinguiamo tra due tipi di destinazione: connessioni ed estensioni. Esistono due tipi di destinazioni di connessione, le destinazioni di esportazione dei profili e le destinazioni di esportazione dei segmenti.

![Tipi di destinazioni](./assets/destination-types/types-of-destinations.png)

### Connessioni {#connections}

**[!UICONTROL Profile Export]** e **[!UICONTROL Segment Export]** le destinazioni in Real-time Customer Data Platform acquisiscono i dati dell&#39;evento, li combinano con altre origini dati per formare il profilo [cliente in tempo](../profile/home.md)reale, applicare segmentazione ed esportare segmenti e profili qualificati per destinazioni.

#### Destinazioni di esportazione profilo

Le destinazioni di esportazione dei profili generano un file contenente profili e/o attributi. Queste destinazioni utilizzano dati non elaborati, spesso con l&#39;indirizzo e-mail come chiave primaria. La [destinazione](./catalog/cloud-storage/amazon-s3.md) di archiviazione cloud Amazon S3 è un esempio di destinazione in cui è possibile depositare i file contenenti esportazioni di profilo.

#### Destinazioni di esportazione dei segmenti

Le destinazioni di esportazione dei segmenti inviano i profili e i segmenti per i quali si sono qualificati alle piattaforme di destinazione. Queste destinazioni utilizzano ID segmento o ID utente. Destinazioni pubblicitarie come [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) o [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md) sono esempi di questi tipi di destinazioni.

#### Destinazioni di esportazione dei profili e dei segmenti - Panoramica video

Il video seguente illustra le particolarità dei due tipi di destinazioni:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### Estensioni {#extensions}

CDP in tempo reale sfrutta la potenza e la flessibilità di  Adobe Experience Platform Launch per includere estensioni Platform Launch nell&#39;interfaccia CDP in tempo reale.

>[!TIP]
>
>Per informazioni dettagliate su  estensioni Adobe Experience Platform Launch, compresi i casi di utilizzo e come trovarle nell&#39;interfaccia, consultate la panoramica [delle estensioni Adobe Experience Platform Launch](./catalog/launch-extensions/overview.md).

Le estensioni Launch piattaforma inoltrano i dati evento non elaborati a diversi tipi di destinazioni. Considerate le estensioni come un tipo di destinazione di inoltro **** degli eventi. Si tratta di un tipo di integrazione più semplice con le piattaforme di destinazione, che inoltra solo dati di evento non elaborati. Esempi di questi sono l&#39;estensione [di personalizzazione](./catalog/personalization/gainsight.md) Gainsight o la [voce Conferma dell&#39;estensione](./catalog/voice/confirmit-digital-feedback.md)del cliente.

![Estensioni Experience Platform Launch confrontate con altre destinazioni](./assets/common/launch-and-other-destinations.png)

### Quando utilizzare connessioni ed estensioni

Come esperto di marketing, puoi usare una combinazione di connessioni ed estensioni per risolvere i tuoi casi d&#39;uso.

Le connessioni sono utili quando è necessario sfruttare un profilo cliente centralizzato completo o un segmento cliente per l&#39;attivazione. Ad esempio, utilizza le connessioni se unisci dati comportamentali da un sistema di analisi con dati CRM caricati per qualificare un utente per un determinato segmento prima di inviare un messaggio personalizzato a tale utente.

Le estensioni sono utili quando i dati dell&#39;evento vengono utilizzati per attivare un&#39;azione o per eseguire la segmentazione in un ambiente esterno. Ad esempio, se i dati comportamentali devono essere inoltrati a un sistema esterno senza essere uniti ad altre origini dati sul file per un determinato utente.

## Categorie di destinazione

Le connessioni e le estensioni nel catalogo [delle](https://platform.adobe.com/destination/catalog) destinazioni sono raggruppate per categoria di destinazione (**Annuncio**, Archivio **** Cloud, Piattaforme **** per sondaggi, Marketing **tramite** e-mail, ecc.), a seconda del caso di utilizzo del marketing che aiutano a ottenere. Per ulteriori informazioni su ciascuna categoria, nonché sulle destinazioni incluse in ciascuna categoria, consulta la documentazione [del catalogo](./catalog/overview.md)Destinazioni.

![Categorie di destinazione](./assets/destination-types/destination-categories-menu.png)

