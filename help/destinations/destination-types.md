---
keywords: destinazioni;destinazione;tipi di destinazione;destinations;destination types
title: Tipi e categorie di destinazione
description: Scopri i diversi tipi e categorie di destinazioni in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 25f1b2197e5b10b04668d16bff3a6ce48cfad5fc
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# Tipi e categorie di destinazione

Leggi questa pagina per comprendere i diversi tipi e categorie di destinazioni Adobe Experience Platform.

## Tipi di destinazione {#destination-types}

In Adobe Experience Platform, distinguiamo tra diversi tipi di destinazione: connessioni, esportazioni di set di dati ed estensioni. Esistono diversi tipi di destinazioni di connessione che consentono di esportare dati in destinazioni basate su API:

Infine, è possibile distinguere le connessioni tra le destinazioni pubbliche disponibili in tutte le organizzazioni nel catalogo delle destinazioni e le destinazioni private che i clienti di Real-time CDP Ultimate possono creare per soddisfare i propri casi di utilizzo specifici per l’esportazione.

![Diagramma dei tipi di destinazioni.](./assets/destination-types/types-of-destinations-no-highlight.png)

## Connessioni {#connections}

**[!UICONTROL Esportazione profilo]**, **[!UICONTROL Esportazione di segmenti in streaming]**, e **[!DNL Edge Personalization]** le destinazioni in Adobe Experience Platform acquisiscono i dati dell’evento, combinandoli con altre origini dati per formare la [Profilo cliente in tempo reale](../profile/home.md), applica la segmentazione ed esporta segmenti e profili qualificati nelle destinazioni.

## Destinazioni di esportazione profilo {#profile-export}

Le destinazioni di esportazione dei profili ricevono dati non elaborati, spesso con l’indirizzo e-mail come chiave primaria. Experience Platform supporta attualmente due tipi di destinazioni di esportazione del profilo:

* [Destinazioni di esportazione dei profili di streaming (destinazioni aziendali)](#streaming-profile-export)
* [Destinazioni batch (basate su file)](#file-based)

### Destinazioni di esportazione dei profili di streaming (destinazioni aziendali) {#streaming-profile-export}

>[!IMPORTANT]
>
>Le destinazioni Enterprise, o destinazioni di esportazione di profili di streaming, sono disponibili per [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) solo clienti.

Utilizza i connettori dati di destinazione Enterprise per fornire profili Adobe Real-time Customer Data Platform in tempo reale a sistemi interni o ad altri sistemi di terze parti per casi di utilizzo di sincronizzazione, analisi e ulteriore arricchimento dei profili.

Queste destinazioni ricevono i dati di segmenti e profili come flussi di dati di Experience Platform.

Le destinazioni Enterprise includono:

* [Destinazione API HTTP](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Hub eventi di Azure](catalog/cloud-storage/azure-event-hubs.md)

### Destinazioni batch (basate su file) {#file-based}

Ricezione di destinazioni basate su file `.csv` file contenenti profili e/o attributi. [Amazon S3](catalog/cloud-storage/amazon-s3.md) è un esempio di destinazione in cui è possibile esportare file contenenti esportazioni di profili.

## Destinazioni di esportazione di segmenti in streaming {#streaming-destinations}

Le destinazioni di esportazione dei segmenti ricevono i dati dei segmenti di Experience Platform. Queste destinazioni utilizzano ID segmento o ID utente. Destinazioni pubblicitarie e social come [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md), o [Facebook](catalog/social/facebook.md) sono esempi di tali destinazioni.

## Destinazioni di personalizzazione Edge {#edge-personalization-destinations}

Le destinazioni di personalizzazione Edge in Experience Platform includono [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) e [Destinazione di personalizzazione personalizzata](/help/destinations/catalog/personalization/custom-personalization.md). Utilizzando queste destinazioni, puoi abilitare per i clienti i casi di utilizzo della personalizzazione della stessa pagina e della pagina successiva.

Ulteriori informazioni su come [configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva](/help/destinations/ui/configure-personalization-destinations.md).

## Destinazioni di esportazione di profili e segmenti: panoramica video {#video}

Il video seguente illustra le particolarità dei due tipi di destinazioni:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Destinazioni di esportazione del set di dati (Beta) {#dataset-export-destinations}

Alcune destinazioni di archiviazione cloud nel catalogo delle destinazioni supportano le esportazioni dei set di dati. Utilizza queste destinazioni per esportare i set di dati non elaborati nelle posizioni di archiviazione cloud.

Ulteriori informazioni su come [esportare i set di dati](/help/destinations/ui/export-datasets.md).

## Estensioni {#extensions}

Platform sfrutta la potenza e la flessibilità della gestione dei tag, consentendoti di configurare le estensioni tag nell’interfaccia utente.

>[!TIP]
>
>Per informazioni dettagliate sulle estensioni tag, inclusi i casi di utilizzo e come trovarle nell’interfaccia, vedi [panoramica delle estensioni tag](./catalog/launch-extensions/overview.md).

Le estensioni di tag inoltrano i dati di eventi non elaborati a diversi tipi di destinazioni. Considera le estensioni come un **Inoltro eventi** tipo di destinazione. Si tratta di un tipo più semplice di integrazione con le piattaforme di destinazione, che inoltra solo i dati dell’evento non elaborati. Esempi di questi sono [Estensione di personalizzazione Gainsight](./catalog/personalization/gainsight.md) o [Conferma voce dell’estensione del cliente](./catalog/voice/confirmit-digital-feedback.md).

![Estensioni di tag rispetto ad altre destinazioni](./assets/common/launch-and-other-destinations.png)

## Quando utilizzare connessioni ed estensioni {#when-to-use}

In qualità di addetto al marketing, puoi utilizzare una combinazione di connessioni ed estensioni per gestire i tuoi casi d’uso.

Le connessioni sono utili quando è necessario sfruttare un profilo cliente centralizzato completo o un segmento di cliente per l’attivazione. Ad esempio, utilizza le connessioni se stai unendo dati comportamentali da un sistema di analisi con dati CRM caricati per qualificare un utente per un dato segmento prima di inviare un messaggio personalizzato a tale utente.

Le estensioni sono utili quando i dati evento vengono utilizzati per attivare un’azione o per eseguire la segmentazione in un ambiente esterno. Ad esempio, se i dati comportamentali devono essere inoltrati a un sistema esterno senza essere uniti ad altre origini dati nel file per un determinato utente.

## Categorie di destinazione {#categories}

Le connessioni e le estensioni in [catalogo delle destinazioni](https://platform.adobe.com/destination/catalog) sono raggruppati per categoria di destinazione (**Pubblicità**, **Archiviazione cloud**, **Piattaforme di sondaggio**, **E-mail marketing**, ecc.), a seconda dell’azione di marketing che ti aiutano a raggiungere. Per ulteriori informazioni su ciascuna categoria, nonché sulle destinazioni incluse in ciascuna categoria, consulta la [Documentazione del catalogo delle destinazioni](./catalog/overview.md).

![Le categorie di destinazione sono evidenziate nella pagina del catalogo.](./assets/destination-types/destination-categories-menu.png)
