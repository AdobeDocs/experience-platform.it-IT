---
keywords: estensioni tag;estensione tag;destinazioni lancio;estensioni tag piattaforma;estensione tag piattaforma;destinazioni platform launch
title: Estensioni tag in Adobe Experience Platform
description: Adobe Experience Platform fornisce la nuova generazione di funzionalità di gestione tag di Adobe. Platform offre un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 2%

---

# Estensioni tag in Adobe Experience Platform

Adobe Experience Platform fornisce la nuova generazione di funzionalità di gestione tag di Adobe. Platform offre un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate. I tag sono offerti ai clienti di Adobe Experience Cloud come funzionalità inclusa a valore aggiunto.

Per un’introduzione ai tag, consulta le risorse seguenti:

- [Panoramica sui tag](../../../tags/home.md)
- [Guida introduttiva](../../../tags/quick-start/quick-start.md)

## Come trovare le estensioni tag nell’interfaccia di Platform {#how-to-find-extensions-in-interface}

Per trovare le estensioni nell&#39;interfaccia di Platform, passa a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** e seleziona **[!UICONTROL Estensioni]** nel filtro **[!UICONTROL Tipi]**.

![Filtro estensioni nell&#39;interfaccia](../../assets/catalog/launch-extensions/filter.png)

## Funzionamento delle estensioni tag {#how-extensions-work}

Un&#39;estensione tag [](../../../tags/home.md#extensions) è un pacchetto di codice che migliora le funzionalità di un sito Web o di un&#39;app mobile. Ciò può includere l&#39;invio di dati evento non elaborati a una destinazione come [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md), ma possono anche servire altre funzioni.

È importante distinguere tra estensioni di tag ed estensioni di inoltro eventi. Le estensioni visualizzate nell&#39;interfaccia utente delle destinazioni di Platform sono *estensioni tag*. Per ulteriori informazioni sulle [differenze tra i tag e l&#39;inoltro degli eventi](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags), consulta la panoramica sull&#39;inoltro degli eventi.



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export audiences and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## Vantaggi dell’utilizzo delle estensioni tag {#extensions-benefits}

Le funzionalità tag di Platform sono gratuite per i clienti Experience Cloud esistenti. Il sistema semplifica la distribuzione dei tag sul sito web tramite estensioni facili da usare che è possibile installare, configurare, aggiornare ed eliminare. I tag lasciano un piccolo spazio sul sito web e consentono di mantenere le pagine in caricamento rapido.

Anche se non è possibile attivare i tipi di pubblico per le estensioni di tag, è possibile impostare regole per inoltrare solo i dati evento in determinate situazioni. Questa potente funzionalità consente di inoltrare i dati dell’evento solo in determinate situazioni, anziché inviare i dati dell’evento su ogni interazione. Per ulteriori informazioni, consulta le regole nella [documentazione sui tag](../../../tags/ui/managing-resources/rules.md).

## Casi di utilizzo di esempio per le estensioni {#extensions-use-cases}

Le estensioni consentono di soddisfare vari casi d’uso per i clienti. Alcuni casi di utilizzo per l’utilizzo delle estensioni sono:

- Puoi inviare dati da siti web o app native a Facebook tramite l’estensione pixel di Facebook. Facebook Pixel indica a quali parti del sito o dell’app un visitatore è passato, inoltra tali informazioni a Facebook e puoi effettuare il retargeting del visitatore tramite Facebook.
- Puoi inoltrare i dati di un evento dai tuoi siti web e dalle tue app a Google Analytics per analizzarli e prendere decisioni basate su di essi.
- Puoi attivare un’app chatbox lato client al momento giusto in base al modo in cui gli utenti interagiscono con le pagine, in base alle regole impostate.

## Categorie di estensioni {#extension-categories}

In Platform, le estensioni possono rientrare nelle seguenti categorie:

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Piattaforma di gestione dati](../data-management/overview.md)
- [Destinazioni di e-mail marketing](../email-marketing/overview.md)
- [Personalizzazione](../personalization/overview.md)
- [Indagini](../survey/overview.md)
- [Voce del cliente](../voice/overview.md)
