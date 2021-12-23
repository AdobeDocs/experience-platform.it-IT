---
keywords: estensioni tag;estensione tag;destinazioni launch; estensioni tag piattaforma;estensione tag piattaforma;destinazioni platform launch
title: Assegnare tag alle estensioni in Adobe Experience Platform
description: Adobe Experience Platform fornisce la nuova generazione di funzionalità di gestione dei tag di Adobe. Platform ti offre un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: fe71294cb73a25c2c4708b0a6ebe04fc2b97afdf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Assegnare tag alle estensioni in Adobe Experience Platform

Adobe Experience Platform fornisce la nuova generazione di funzionalità di gestione tag di Adobe. Platform ti offre un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate. I tag sono offerti ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto.

Per un’introduzione ai tag, consulta le risorse seguenti:

- [Panoramica sui tag](../../../tags/home.md)
- [Guida rapida](../../../tags/quick-start/quick-start.md)

## Come trovare le estensioni di tag nell’interfaccia di Platform {#how-to-find-extensions-in-interface}

Per trovare le estensioni nell’interfaccia di Platform, sfoglia fino a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** e seleziona **[!UICONTROL Estensioni]** in **[!UICONTROL Tipi]** filtro.

![Filtro delle estensioni nell’interfaccia](../../assets/catalog/launch-extensions/filter.png)

## Funzionamento delle estensioni tag {#how-extensions-work}

A [estensione tag](../../../tags/home.md#extensions) è un pacchetto di codice che migliora la funzionalità di un sito web o di un’app mobile. Ciò potrebbe includere l&#39;invio di dati di evento non elaborati a una destinazione come [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) ma possono anche servire altre funzioni.

È importante distinguere tra estensioni di tag ed eventi di inoltro. Le estensioni visualizzate nell’interfaccia utente delle destinazioni Platform sono *estensioni tag*. Per ulteriori informazioni sull’ [differenze tra tag e inoltro eventi](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export segments and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## Vantaggi dell&#39;utilizzo delle estensioni tag {#extensions-benefits}

Le funzionalità tag di Platform sono gratuite per i clienti Experience Cloud esistenti. Il sistema semplifica la distribuzione dei tag sul sito web tramite estensioni facili da usare che puoi installare, configurare, aggiornare ed eliminare. I tag lasciano un piccolo ingombro sul sito web e ti consentono di mantenere le pagine caricate rapidamente.

Sebbene non sia possibile attivare i segmenti per assegnare tag alle estensioni, è possibile impostare regole per inoltrare solo i dati evento in determinate situazioni. Questa potente funzionalità ti consente di inoltrare i dati evento solo in determinate situazioni, anziché inviare i dati evento su ogni interazione. Per ulteriori informazioni, consulta le regole nella sezione [documentazione sui tag](../../../tags/ui/managing-resources/rules.md).

## Esempi di casi d’uso per le estensioni {#extensions-use-cases}

Le estensioni ti consentono di soddisfare vari casi d’uso dei clienti. Alcuni casi d’uso per l’utilizzo delle estensioni sono:

- Puoi inviare dati di siti web o app nativi a Facebook tramite l’estensione Facebook pixel. Facebook Pixel indica in quali parti del sito o dell’app un visitatore ha navigato, inoltra tali informazioni a Facebook e puoi effettuare il retargeting del visitatore tramite Facebook.
- Puoi inoltrare i dati evento dai tuoi siti web e dalle tue app in Google Analytics per analizzarli e prendere decisioni basate su tali dati.
- Puoi attivare un’app chatbox lato client al momento giusto in base alle modalità di interazione degli utenti con le tue pagine, in base alle regole configurate.

## Categorie di estensioni {#extension-categories}

Le estensioni possono rientrare nelle seguenti categorie in Platform:

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Piattaforma di gestione dati](../data-management/overview.md)
- [Destinazioni di marketing e-mail](../email-marketing/overview.md)
- [Personalizzazione](../personalization/overview.md)
- [Indagini](../survey/overview.md)
- [Voce del cliente](../voice/overview.md)
