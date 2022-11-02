---
keywords: destinazioni;destinazione;tipi di destinazione
title: Tipi di destinazione e categorie
description: Scopri i diversi tipi e categorie di destinazioni in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: c140e68467065d17f143850bfb8eefb3ac46443a
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Tipi di destinazione e categorie

Leggi questa pagina per comprendere i diversi tipi e categorie di destinazioni Adobe Experience Platform.

## Tipi di destinazione {#destination-types}

In Adobe Experience Platform, distinguiamo tra due tipi di destinazione: connessioni ed estensioni. Esistono due tipi di destinazioni di connessione, le destinazioni di esportazione del profilo e le destinazioni di esportazione del segmento.

![Tipi di destinazioni](./assets/destination-types/types-of-destinations.png)

## Connessioni {#connections}

**[!UICONTROL Esportazione profilo]**, **[!UICONTROL Esportazione segmento streaming]** e **[!DNL Edge Personalization]** le destinazioni in Adobe Experience Platform acquisiscono i dati dell’evento, combinandoli con altre origini dati per formare [Profilo cliente in tempo reale](../profile/home.md), applica la segmentazione ed esporta segmenti e profili qualificati nelle destinazioni.

## Destinazioni di esportazione del profilo {#profile-export}

Le destinazioni di esportazione del profilo ricevono dati non elaborati, spesso con l’indirizzo e-mail come chiave primaria. Experience Platform supporta attualmente due tipi di destinazioni di esportazione del profilo:

* [Destinazioni di esportazione del profilo in streaming (destinazioni aziendali)](#streaming-profile-export)
* [Destinazioni batch (basate su file)](#file-based)

### Destinazioni di esportazione del profilo in streaming (destinazioni aziendali) {#streaming-profile-export}

>[!IMPORTANT]
>
>Le destinazioni Enterprise o le destinazioni di esportazione del profilo in streaming sono disponibili per [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) Solo clienti.

Utilizza i connettori dati di destinazione Enterprise per fornire profili Adobe Real-time Customer Data Platform in tempo quasi reale a sistemi interni o ad altri sistemi di terze parti per la sincronizzazione dei dati, l’analisi e ulteriori casi d’uso di arricchimento dei profili.

Queste destinazioni ricevono dati di segmenti e profili come flussi di dati di Experience Platform.

Le destinazioni aziendali includono:

* [Destinazione API HTTP](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Hub eventi di Azure](catalog/cloud-storage/azure-event-hubs.md)

### Destinazioni batch (basate su file) {#file-based}

Le destinazioni basate su file ricevono `.csv` file contenenti profili e/o attributi. [Amazon S3](catalog/cloud-storage/amazon-s3.md) è un esempio di destinazione in cui è possibile esportare file contenenti esportazioni di profili.

## Destinazioni di esportazione dei segmenti in streaming {#streaming-destinations}

Le destinazioni di esportazione dei segmenti ricevono dati Experienci Platform sui segmenti. Queste destinazioni utilizzano ID segmento o ID utente. Pubblicità e destinazioni social come [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)oppure [Facebook](catalog/social/facebook.md) sono esempi di tali destinazioni.

## Destinazioni di personalizzazione Edge {#edge-personalization-destinations}

Le destinazioni di personalizzazione Edge in Experience Platform includono [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) e [Destinazione di personalizzazione personalizzata](/help/destinations/catalog/personalization/custom-personalization.md). Utilizzando queste destinazioni, puoi abilitare i tuoi clienti per i casi d’uso di personalizzazione della stessa pagina e della pagina successiva.

Ulteriori informazioni su come [configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva](/help/destinations/ui/configure-personalization-destinations.md).

## Esportazione di profili e destinazioni di esportazione di segmenti - panoramica video {#video}

Il video seguente illustra le particolarità dei due tipi di destinazioni:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Destinazioni di esportazione del set di dati (Beta) {#dataset-export-destinations}

Alcune destinazioni di archiviazione cloud nel catalogo delle destinazioni supportano le esportazioni di set di dati. Utilizza queste destinazioni per esportare i set di dati non elaborati nelle posizioni di archiviazione cloud.

Ulteriori informazioni su come [esportare i set di dati](/help/destinations/ui/export-datasets.md).

## Estensioni {#extensions}

Platform sfrutta la potenza e la flessibilità della gestione dei tag, consentendoti di configurare le estensioni dei tag nell’interfaccia utente di .

>[!TIP]
>
>Per informazioni dettagliate sulle estensioni dei tag, compresi i casi d’uso e su come trovarli nell’interfaccia, consulta la sezione [panoramica delle estensioni di tag](./catalog/launch-extensions/overview.md).

I tag delle estensioni inoltrano i dati evento non elaborati a diversi tipi di destinazioni. Considera le estensioni come un **Inoltro eventi** tipo di destinazione. Si tratta di un tipo di integrazione più semplice con le piattaforme di destinazione, che inoltra solo dati di evento non elaborati. Alcuni esempi sono [Estensione Gainsight Personalization](./catalog/personalization/gainsight.md) o [Conferma la voce dell&#39;estensione del cliente](./catalog/voice/confirmit-digital-feedback.md).

![Assegnare tag alle estensioni rispetto ad altre destinazioni](./assets/common/launch-and-other-destinations.png)

## Quando utilizzare connessioni ed estensioni {#when-to-use}

In qualità di addetto al marketing, puoi utilizzare una combinazione di connessioni ed estensioni per risolvere i tuoi casi d’uso.

Le connessioni sono utili quando è necessario sfruttare un profilo cliente centralizzato completo o un segmento cliente per l’attivazione. Ad esempio, utilizza le connessioni se unisci dati comportamentali da un sistema di analisi con dati CRM caricati per qualificare un utente per un dato segmento prima di inviare un messaggio personalizzato a tale utente.

Le estensioni sono utili quando i dati evento vengono utilizzati per attivare un’azione o per eseguire la segmentazione in un ambiente esterno. Ad esempio, se i dati comportamentali devono essere inoltrati a un sistema esterno senza essere collegati ad altre origini dati nel file per un determinato utente.

## Categorie di destinazione {#categories}

Le connessioni e le estensioni nel [catalogo delle destinazioni](https://platform.adobe.com/destination/catalog) sono raggruppati per categoria di destinazione (**Pubblicità**, **archiviazione cloud**, **Piattaforme di sondaggio**, **E-mail marketing**, ecc.), a seconda dell’azione di marketing che ti consente di ottenere. Per ulteriori informazioni su ciascuna categoria e sulle destinazioni incluse in ciascuna categoria, consulta la sezione [Documentazione del catalogo delle destinazioni](./catalog/overview.md).

![Categorie di destinazione](./assets/destination-types/destination-categories-menu.png)
