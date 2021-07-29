---
keywords: destinazioni;destinazione;tipi di destinazione
title: Tipi di destinazione e categorie
seo-title: Tipi di destinazione e categorie
description: Scopri i diversi tipi e categorie di destinazioni in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# Tipi di destinazione e categorie

Leggi questa pagina per comprendere i diversi tipi e categorie di destinazioni Adobe Experience Platform.

## Tipi di destinazione

In Adobe Experience Platform, distinguiamo tra due tipi di destinazione: connessioni ed estensioni. Esistono due tipi di destinazioni di connessione, le destinazioni di esportazione del profilo e le destinazioni di esportazione del segmento.

![Tipi di destinazioni](./assets/destination-types/types-of-destinations.png)

## Connessioni {#connections}

**[!UICONTROL Le destinazioni di]** esportazione di profili e  **[!UICONTROL segmenti]** esportati in Adobe Experience Platform acquisiscono dati evento, li combinano con altre sorgenti di dati per formare il profilo cliente in tempo  [reale](../profile/home.md), applicano la segmentazione ed esportano segmenti e profili qualificati nelle destinazioni.

## Destinazioni di esportazione del profilo

Le destinazioni di esportazione del profilo generano un file contenente profili e/o attributi. Queste destinazioni utilizzano dati non elaborati, spesso con l’indirizzo e-mail come chiave primaria. La [destinazione di archiviazione cloud Amazon S3](./catalog/cloud-storage/amazon-s3.md) è un esempio di destinazione in cui puoi depositare i file contenenti esportazioni di profili.

## Destinazioni di esportazione del segmento

Le destinazioni di esportazione dei segmenti inviano i profili e i segmenti per i quali si sono qualificati alle piattaforme di destinazione. Queste destinazioni utilizzano ID segmento o ID utente. Le destinazioni pubblicitarie come [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) o [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md) sono esempi di questo tipo di destinazioni.

## Esportazione del profilo e destinazioni di esportazione del segmento - panoramica video

Il video seguente illustra le particolarità dei due tipi di destinazioni:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Estensioni {#extensions}

Platform sfrutta la potenza e la flessibilità della gestione dei tag, consentendoti di configurare le estensioni dei tag nell’interfaccia utente di raccolta dati.

>[!TIP]
>
>Per informazioni dettagliate sulle estensioni dei tag, compresi i casi d&#39;uso e su come trovarli nell&#39;interfaccia, consulta la [panoramica delle estensioni dei tag](./catalog/launch-extensions/overview.md) .

I tag delle estensioni inoltrano i dati evento non elaborati a diversi tipi di destinazioni. Considera le estensioni come un tipo di destinazione **Inoltro eventi**. Si tratta di un tipo di integrazione più semplice con le piattaforme di destinazione, che inoltra solo dati di evento non elaborati. Alcuni esempi sono l&#39; [Estensione di personalizzazione Gainsight](./catalog/personalization/gainsight.md) o la [Voce di conferma dell&#39;estensione del cliente](./catalog/voice/confirmit-digital-feedback.md).

![Assegnare tag alle estensioni rispetto ad altre destinazioni](./assets/common/launch-and-other-destinations.png)

## Quando utilizzare connessioni ed estensioni

In qualità di addetto al marketing, puoi utilizzare una combinazione di connessioni ed estensioni per risolvere i tuoi casi d’uso.

Le connessioni sono utili quando è necessario sfruttare un profilo cliente centralizzato completo o un segmento cliente per l’attivazione. Ad esempio, utilizza le connessioni se unisci dati comportamentali da un sistema di analisi con dati CRM caricati per qualificare un utente per un dato segmento prima di inviare un messaggio personalizzato a tale utente.

Le estensioni sono utili quando i dati evento vengono utilizzati per attivare un’azione o per eseguire la segmentazione in un ambiente esterno. Ad esempio, se i dati comportamentali devono essere inoltrati a un sistema esterno senza essere collegati ad altre origini dati nel file per un determinato utente.

## Categorie di destinazione

Le connessioni e le estensioni nel catalogo [destinazioni](https://platform.adobe.com/destination/catalog) sono raggruppate per categoria di destinazione (**Pubblicità**, **Archiviazione cloud**, **Piattaforme di sondaggio**, **Marketing e-mail**, ecc.), a seconda dell&#39;azione di marketing che consentono di raggiungere. Per ulteriori informazioni su ciascuna categoria, nonché sulle destinazioni incluse in ciascuna categoria, consulta la [Documentazione del catalogo delle destinazioni](./catalog/overview.md).

![Categorie di destinazione](./assets/destination-types/destination-categories-menu.png)
