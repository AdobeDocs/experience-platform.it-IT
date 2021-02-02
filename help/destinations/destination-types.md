---
keywords: destinazioni;destinazione;tipi di destinazione
title: Tipi e categorie di destinazioni
seo-title: Tipi e categorie di destinazioni
description: 'In Adobe Experience Platform, le destinazioni di esportazione Profilo/Segmento acquisiscono i dati degli eventi, li combinano con altre origini dati, applicano la segmentazione ed esportano segmenti e profili qualificati per destinazioni. Le estensioni di Experience Platform Launch inoltrano i dati dell''evento non elaborati a diversi tipi di destinazioni. '
seo-description: In Adobe Experience Platform, le destinazioni di esportazione Profilo/Segmento acquisiscono i dati degli eventi, li combinano con altre origini dati, applicano la segmentazione ed esportano segmenti e profili qualificati per destinazioni. Le estensioni di Experience Platform Launch inoltrano i dati dell'evento non elaborati a diversi tipi di destinazioni.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Tipi di destinazione e categorie

Leggi questa pagina per comprendere i diversi tipi e categorie di destinazioni Adobe Experience Platform.

## Tipi di destinazione

In Adobe Experience Platform, distinguiamo tra due tipi di destinazione: connessioni ed estensioni. Esistono due tipi di destinazioni di connessione, le destinazioni di esportazione dei profili e le destinazioni di esportazione dei segmenti.

![Tipi di destinazioni](./assets/destination-types/types-of-destinations.png)

### Connessioni {#connections}

**[!UICONTROL Profile Export]** e  **[!UICONTROL Segment Export]** le destinazioni in Adobe Experience Platform acquisiscono i dati degli eventi, li combinano con altre origini dati per formare il profilo [ cliente in tempo ](../profile/home.md)reale, applicare la segmentazione ed esportare segmenti e profili qualificati per destinazioni.

#### Destinazioni di esportazione profilo

Le destinazioni di esportazione dei profili generano un file contenente profili e/o attributi. Queste destinazioni utilizzano dati non elaborati, spesso con l&#39;indirizzo e-mail come chiave primaria. La [ destinazione di archiviazione cloud Amazon S3](./catalog/cloud-storage/amazon-s3.md) è un esempio di destinazione in cui è possibile depositare i file contenenti esportazioni di profilo.

#### Destinazioni di esportazione dei segmenti

Le destinazioni di esportazione dei segmenti inviano i profili e i segmenti per i quali si sono qualificati alle piattaforme di destinazione. Queste destinazioni utilizzano ID segmento o ID utente. Le destinazioni pubblicitarie come [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) o [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md) sono esempi di questo tipo di destinazioni.

#### Destinazioni di esportazione dei profili e dei segmenti - Panoramica video

Il video seguente illustra le particolarità dei due tipi di destinazioni:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### Estensioni {#extensions}

La piattaforma sfrutta la potenza e la flessibilità di  Adobe Experience Platform Launch per includere estensioni Platform Launch nell&#39;interfaccia della piattaforma.

>[!TIP]
>
>Per informazioni dettagliate su  estensioni Adobe Experience Platform Launch, compresi i casi di utilizzo e come trovarle nell&#39;interfaccia, vedere la [ panoramica delle estensioni Adobe Experience Platform Launch](./catalog/launch-extensions/overview.md).

Le estensioni Launch piattaforma inoltrano i dati evento non elaborati a diversi tipi di destinazioni. Considerate le estensioni come un tipo di destinazione **Inoltro eventi**. Si tratta di un tipo di integrazione più semplice con le piattaforme di destinazione, che inoltra solo dati di evento non elaborati. Alcuni esempi sono l&#39; [Estensione di personalizzazione del guadagno](./catalog/personalization/gainsight.md) o la [Conferma voce dell&#39;estensione del cliente](./catalog/voice/confirmit-digital-feedback.md).

![Estensioni Experience Platform Launch confrontate con altre destinazioni](./assets/common/launch-and-other-destinations.png)

### Quando utilizzare connessioni ed estensioni

Come esperto di marketing, puoi usare una combinazione di connessioni ed estensioni per risolvere i tuoi casi d&#39;uso.

Le connessioni sono utili quando è necessario sfruttare un profilo cliente centralizzato completo o un segmento cliente per l&#39;attivazione. Ad esempio, utilizza le connessioni se unisci dati comportamentali da un sistema di analisi con dati CRM caricati per qualificare un utente per un determinato segmento prima di inviare un messaggio personalizzato a tale utente.

Le estensioni sono utili quando i dati dell&#39;evento vengono utilizzati per attivare un&#39;azione o per eseguire la segmentazione in un ambiente esterno. Ad esempio, se i dati comportamentali devono essere inoltrati a un sistema esterno senza essere uniti ad altre origini dati sul file per un determinato utente.

## Categorie di destinazione

Le connessioni e le estensioni nel catalogo [delle destinazioni](https://platform.adobe.com/destination/catalog) sono raggruppate per categoria di destinazione (**Pubblicità**, **Cloud storage**, **Piattaforme di sondaggio**, **Email marketing** ecc.), a seconda del caso di utilizzo del marketing che consentono di ottenere. Per ulteriori informazioni su ciascuna categoria, nonché sulle destinazioni incluse in ciascuna categoria, consultare la [Documentazione del catalogo delle destinazioni](./catalog/overview.md).

![Categorie di destinazione](./assets/destination-types/destination-categories-menu.png)

