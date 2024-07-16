---
keywords: destinazioni;destinazione;tipi di destinazione;destinations;destination types
title: Tipi e categorie di destinazione
description: Scopri i diversi tipi e categorie di destinazioni in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: c6019737e93756f3f524d5a85ea57383baa1a31d
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 1%

---

# Tipi e categorie di destinazione

Leggi questa pagina per comprendere i diversi tipi e categorie di destinazioni Adobe Experience Platform.

## Tipi di destinazione {#destination-types}

In Adobe Experience Platform, distinguiamo tra diversi tipi di destinazione: connessioni, esportazioni di set di dati ed estensioni. Esistono diversi tipi di destinazioni di connessione che ti consentono di esportare dati in destinazioni basate su API, destinazioni social, piattaforme di gestione delle relazioni con i clienti e molto altro.

Infine, è possibile distinguere le connessioni tra le destinazioni pubbliche disponibili in tutte le organizzazioni nel catalogo delle destinazioni e le destinazioni private che i clienti di Real-Time CDP Ultimate possono creare per soddisfare i propri casi di utilizzo specifici per l&#39;esportazione.

![Diagramma dei tipi di destinazioni.](./assets/destination-types/types-of-destinations-no-highlight.png)

## Connessioni {#connections}

**[!UICONTROL Esportazione profilo]**, **[!UICONTROL Esportazione pubblico in streaming]** e **[!DNL Edge Personalization]** destinazioni in Adobe Experience Platform acquisiscono i dati dell&#39;evento, li combinano con altre origini dati per formare il [Profilo cliente in tempo reale](../profile/home.md), applicano la segmentazione ed esportano tipi di pubblico e profili qualificati nelle destinazioni.

## Destinazioni di esportazione profilo {#profile-export}

Le destinazioni di esportazione dei profili ricevono dati non elaborati, spesso con l’indirizzo e-mail come chiave primaria. Experience Platform supporta attualmente due tipi di destinazioni di esportazione del profilo:

* [Destinazioni di esportazione dei profili di streaming (destinazioni aziendali)](#streaming-profile-export)
* [Destinazioni batch (basate su file)](#file-based)

### Destinazioni di esportazione dei profili di streaming (destinazioni aziendali) {#streaming-profile-export}

>[!IMPORTANT]
>
>Le destinazioni Enterprise o le destinazioni di esportazione dei profili di streaming sono disponibili solo per [clienti Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html).

Utilizza i connettori dati di destinazione Enterprise per fornire profili Adobe Real-time Customer Data Platform in tempo reale a sistemi interni o ad altri sistemi di terze parti per casi di utilizzo di sincronizzazione, analisi e ulteriore arricchimento dei profili.

Queste destinazioni ricevono i dati di pubblico e profilo come flussi di dati di Experience Platform.

Le destinazioni Enterprise includono:

* [Destinazione API HTTP](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Hub eventi Azure](catalog/cloud-storage/azure-event-hubs.md)

### Destinazioni batch (basate su file) {#file-based}

Le destinazioni basate su file ricevono `.csv` file contenenti profili e/o attributi. [Amazon S3](catalog/cloud-storage/amazon-s3.md) è un esempio di destinazione in cui è possibile esportare file contenenti esportazioni di profili.

## Destinazioni di esportazione del pubblico in streaming {#streaming-destinations}

Le destinazioni di esportazione del pubblico ricevono i dati sul pubblico di Experienci Platform. Queste destinazioni utilizzano ID pubblico o ID utente. Advertising e destinazioni social come [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md) o [Facebook](catalog/social/facebook.md) sono esempi di tali destinazioni.

## Destinazioni di personalizzazione Edge {#edge-personalization-destinations}

Le destinazioni di personalizzazione di Edge in Experience Platform includono [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) e [Personalization destination](/help/destinations/catalog/personalization/custom-personalization.md). Utilizzando queste destinazioni, puoi abilitare per i clienti i casi di utilizzo della personalizzazione della stessa pagina e della pagina successiva.

Ulteriori informazioni su come [configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva](/help/destinations/ui/activate-edge-personalization-destinations.md).

## Destinazioni di esportazione profilo e pubblico - Panoramica video {#video}

Il video seguente illustra le particolarità dei due tipi di destinazioni:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Tipi di pubblico esportati {#exported-audiences-types}

Puoi esportare tre tipi di pubblico da Experience Platform in varie destinazioni:

* Pubblico persone
* Pubblico dell’account
* Pubblico potenziale

Ulteriori informazioni sui [vari tipi di pubblico](/help/segmentation/ui/account-audiences.md#terminology).

Un simbolo sulla scheda di destinazione mostra quali tipi di pubblico puoi esportare in ogni destinazione.

![Esempio di scheda di destinazione con simboli che indicano quali tipi di pubblico possono essere esportati.](/help/destinations/assets/destination-types/types-of-audiences.png)


## Destinazioni di esportazione del set di dati {#dataset-export-destinations}

Alcune destinazioni di archiviazione cloud nel catalogo delle destinazioni supportano le esportazioni dei set di dati. Utilizza queste destinazioni per esportare i set di dati non elaborati nelle posizioni di archiviazione cloud.

Ulteriori informazioni su come [esportare i set di dati](/help/destinations/ui/export-datasets.md).

## Estensioni {#extensions}

Platform sfrutta la potenza e la flessibilità della gestione dei tag, consentendoti di configurare le estensioni tag nell’interfaccia utente.

>[!TIP]
>
>Per informazioni dettagliate sulle estensioni tag, inclusi i casi d&#39;uso e le modalità per trovarle nell&#39;interfaccia, consulta la [panoramica sulle estensioni tag](./catalog/launch-extensions/overview.md).

Le estensioni di tag inoltrano i dati di eventi non elaborati a diversi tipi di destinazioni. Considera le estensioni come un tipo di destinazione **Inoltro eventi**. Si tratta di un tipo più semplice di integrazione con le piattaforme di destinazione, che inoltra solo i dati dell’evento non elaborati. Esempi di queste sono l&#39;[estensione Gainsight personalization](./catalog/personalization/gainsight.md) o la [conferma voce dell&#39;estensione del cliente](./catalog/voice/confirmit-digital-feedback.md).

![Estensioni tag rispetto ad altre destinazioni](./assets/common/launch-and-other-destinations.png)

## Quando utilizzare connessioni ed estensioni {#when-to-use}

In qualità di addetto al marketing, puoi utilizzare una combinazione di connessioni ed estensioni per gestire i tuoi casi d’uso.

Le connessioni sono utili quando è necessario sfruttare un profilo cliente centralizzato completo o un pubblico cliente per l’attivazione. Ad esempio, utilizza le connessioni se unisci dati comportamentali da un sistema di analisi con dati CRM caricati per qualificare un utente per un determinato pubblico prima di inviare un messaggio personalizzato a tale utente.

Le estensioni sono utili quando i dati evento vengono utilizzati per attivare un’azione o per eseguire la segmentazione in un ambiente esterno. Ad esempio, se i dati comportamentali devono essere inoltrati a un sistema esterno senza essere uniti ad altre origini dati nel file per un determinato utente.

## Categorie di destinazione {#categories}

Le connessioni e le estensioni nel [catalogo delle destinazioni](https://platform.adobe.com/destination/catalog) sono raggruppate per categoria di destinazione (**Advertising**, **Archiviazione cloud**, **Piattaforme sondaggio**, **E-mail marketing**, ecc.), a seconda dell&#39;azione di marketing che ti aiutano a ottenere. Per ulteriori informazioni su ciascuna categoria e sulle destinazioni incluse in ciascuna categoria, consulta la [documentazione del catalogo delle destinazioni](./catalog/overview.md).

![Categorie di destinazione evidenziate nella pagina del catalogo.](./assets/destination-types/destination-categories-menu.png)
