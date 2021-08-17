---
keywords: estensioni tag;estensione tag;destinazioni launch; estensioni tag piattaforma;estensione tag piattaforma;destinazioni platform launch
title: Assegnare tag alle estensioni in Adobe Experience Platform
description: Adobe Experience Platform fornisce la nuova generazione di funzionalità di gestione dei tag di Adobe. Platform ti offre un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 272cf2906b44ccfeca041d9620ac0780e24ad1ae
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Assegnare tag alle estensioni in Adobe Experience Platform

Adobe Experience Platform fornisce la nuova generazione di funzionalità di gestione dei tag di Adobe. Platform ti offre un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate. I tag sono offerti ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto.

Per un’introduzione ai tag, consulta le risorse seguenti:

- [Panoramica sui tag](../../../tags/home.md)
- [Guida rapida](../../../tags/quick-start/quick-start.md)

## Come trovare le estensioni di tag nell’interfaccia di Platform {#how-to-find-extensions-in-interface}

Per trovare le estensioni nell’interfaccia di Platform, passa a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** e seleziona **[!UICONTROL Estensioni]** nel filtro **[!UICONTROL Tipi]** .

![Filtro delle estensioni nell’interfaccia](../../assets/catalog/launch-extensions/filter.png)

## Funzionamento delle estensioni tag {#how-extensions-work}

Le estensioni inoltrano dati evento non elaborati a diversi tipi di destinazioni. Considera le estensioni come un tipo di destinazione **Inoltro eventi**. Si tratta di un tipo di integrazione più semplice con le piattaforme di destinazione, che inoltra solo dati di evento non elaborati. Alcuni esempi sono l&#39; [Estensione di personalizzazione Gainsight](../personalization/gainsight.md) o la [Voce di conferma dell&#39;estensione del cliente](../voice/confirmit-digital-feedback.md).

**Le destinazioni** esportazione profilo/segmento in Adobe Experience Platform acquisiscono i dati dell’evento, li combinano con altre origini dati, applicano la segmentazione, esportano segmenti e profili qualificati nelle destinazioni. Esempi di questi sono la [destinazione di archiviazione cloud Amazon S3](../cloud-storage/amazon-s3.md) o la [destinazione pubblicitaria Google Display &amp; Video 360](../advertising/google-dv360.md).

![Assegnare tag alle estensioni rispetto ad altre destinazioni](../../assets/common/launch-and-other-destinations.png)

## Vantaggi dell&#39;utilizzo delle estensioni tag {#extensions-benefits}

Le funzionalità tag di Platform sono gratuite per i clienti Experience Cloud esistenti. Il sistema semplifica la distribuzione dei tag sul sito web tramite estensioni facili da usare che puoi installare, configurare, aggiornare ed eliminare. I tag lasciano un piccolo ingombro sul sito web e ti consentono di mantenere le pagine caricate rapidamente.

Sebbene non sia possibile attivare i segmenti per assegnare tag alle estensioni, è possibile impostare regole per inoltrare solo i dati evento in determinate situazioni. Questa potente funzionalità ti consente di inoltrare i dati evento solo in determinate situazioni, anziché inviare i dati evento su ogni interazione. Per ulteriori informazioni, consulta le regole nella [documentazione sui tag](../../../tags/ui/managing-resources/rules.md).

## Esempi di casi d’uso per le estensioni {#extensions-use-cases}

Le estensioni ti consentono di soddisfare vari casi d’uso dei clienti. Alcuni casi d’uso per l’utilizzo delle estensioni sono:

- Puoi inviare dati di siti web o app nativi a Facebook tramite l’estensione Facebook pixel. Facebook Pixel indica in quali parti del sito o dell’app un visitatore ha navigato, inoltra tali informazioni a Facebook e puoi effettuare il retargeting del visitatore tramite Facebook.
- Puoi inoltrare i dati evento dai tuoi siti web e dalle tue app in Google Analytics per analizzarli e prendere decisioni basate su tali dati.
- Puoi attivare un’app chatbox lato client al momento giusto in base alle modalità di interazione degli utenti con le tue pagine, in base alle regole configurate.

## Categorie di estensioni {#extension-categories}

Le estensioni possono rientrare nelle seguenti categorie in Platform:

- [Pubblicità](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Piattaforma di gestione dati](../data-management/overview.md)
- [Destinazioni di marketing e-mail](../email-marketing/overview.md)
- [Personalizzazione](../personalization/overview.md)
- [Indagini](../survey/overview.md)
- [Voce del cliente](../voice/overview.md)
