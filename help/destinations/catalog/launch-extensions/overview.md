---
keywords: estensioni launch;estensione launch;destinazioni launch; Estensioni platform launch;estensione platform launch;destinazioni platform launch
title: Estensione Adobe Experience Platform Launch
description: Adobe Experience Platform Launch è la soluzione Adobe di nuova generazione per la gestione dei tag. Platform Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 14%

---

# Estensioni di Adobe Experience Platform Launch

Adobe Experience Platform Launch è la soluzione Adobe di nuova generazione per la gestione dei tag. Platform Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate. Il platform launch è offerto ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto.

Per un&#39;introduzione alle funzionalità di Experience Platform Launch, consulta le risorse seguenti:

- Documentazione di Adobe Experience Platform Launch [](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=it)
- Adobe Experience Platform Launch [video di avvio rapido](../../../tags/quick-start/videos.md). Inizia con [Introduzione ad Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) e [Panoramica del processo di pubblicazione](https://helpx.adobe.com/it/analytics/how-to/adobe-launch-publishing-process.html), quindi passa ai concetti successivi.

## Come trovare le estensioni di Platform launch nell’interfaccia di Platform {#how-to-find-extensions-in-interface}

Per trovare le estensioni del Platform launch nell’interfaccia di Platform, passa a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** e seleziona **[!UICONTROL Estensioni]** nel filtro **[!UICONTROL Tipi]** .

![Filtro delle estensioni nell’interfaccia](../../assets/catalog/launch-extensions/filter.png)

## Funzionamento delle estensioni di Platform launch {#how-extensions-work}

Le estensioni di platform launch inoltrano i dati evento non elaborati a diversi tipi di destinazioni. Considera le estensioni come un tipo di destinazione **Inoltro eventi**. Si tratta di un tipo di integrazione più semplice con le piattaforme di destinazione, che inoltra solo dati di evento non elaborati. Alcuni esempi sono l&#39; [Estensione di personalizzazione Gainsight](../personalization/gainsight.md) o la [Voce di conferma dell&#39;estensione del cliente](../voice/confirmit-digital-feedback.md).

**Le destinazioni** esportazione profilo/segmento in Adobe Experience Platform acquisiscono i dati dell’evento, li combinano con altre origini dati, applicano la segmentazione, esportano segmenti e profili qualificati nelle destinazioni. Esempi di questi sono la [destinazione di archiviazione cloud Amazon S3](../cloud-storage/amazon-s3.md) o la [destinazione pubblicitaria Google Display &amp; Video 360](../advertising/google-dv360.md).

![Experience Platform Launch di estensioni rispetto ad altre destinazioni](../../assets/common/launch-and-other-destinations.png)

## Vantaggi dell&#39;utilizzo delle estensioni dei Platform launch {#extensions-benefits}

Adobe Experience Platform Launch è gratuito per i clienti esistenti di Experience Cloud. Il platform launch semplifica la distribuzione dei tag sul sito web tramite estensioni facili da usare che puoi installare, configurare, aggiornare ed eliminare. Il platform launch ha un piccolo ingombro sul tuo sito web e ti consente di mantenere le tue pagine caricate rapidamente.

>[!IMPORTANT]
>
>Sebbene non sia possibile attivare segmenti nelle estensioni di Platform launch, è possibile impostare regole per inoltrare solo i dati evento in determinate situazioni. Ulteriori informazioni qui sotto.

Puoi creare *regole* che determinano quando inoltrare i dati dell&#39;evento alle estensioni. Questa potente funzionalità ti consente di inoltrare i dati evento solo in determinate situazioni, anziché inviare i dati evento su ogni interazione. Per ulteriori informazioni, consulta le regole nella [documentazione di Adobe Experience Platform Launch](../../../tags/ui/managing-resources/rules.md).

## Esempi di casi d’uso per le estensioni di Platform launch {#extensions-use-cases}

Le estensioni di platform launch consentono di soddisfare vari casi d’uso dei clienti. Alcuni esempi di casi d&#39;uso per l&#39;utilizzo di estensioni di Platform launch sono:

- Puoi inviare dati di siti web o app nativi a Facebook tramite l’estensione Facebook pixel. Facebook Pixel indica in quali parti del sito o dell’app un visitatore ha navigato, inoltra tali informazioni a Facebook e puoi effettuare il retargeting del visitatore tramite Facebook.
- Puoi inoltrare i dati evento dai tuoi siti web e dalle tue app in Google Analytics per analizzarli e prendere decisioni basate su tali dati.
- Puoi attivare un’app chatbox lato client al momento giusto in base alle modalità di interazione degli utenti con le tue pagine, in base alle regole impostate in Platform launch.

## Categorie di estensioni {#extension-categories}

Le estensioni di platform launch possono rientrare nelle seguenti categorie in Platform:

- [Pubblicità](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Piattaforma di gestione dati](../data-management/overview.md)
- [Destinazioni di marketing e-mail](../email-marketing/overview.md)
- [Personalizzazione](../personalization/overview.md)
- [Indagini](../survey/overview.md)
- [Voce del cliente](../voice/overview.md)
