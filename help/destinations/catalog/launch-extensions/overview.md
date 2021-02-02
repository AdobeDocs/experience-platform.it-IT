---
keywords: estensioni lancio;estensione lancio;destinazioni lancio; estensioni lancio piattaforma;estensione lancio piattaforma;destinazioni lancio piattaforma
title: Estensioni di Experience Platform Launch
seo-title: Estensioni di Experience Platform Launch
description: Launch è la soluzione Adobe di nuova generazione per la gestione dei tag. Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate.
seo-description: Launch è la soluzione Adobe di nuova generazione per la gestione dei tag. Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 19%

---


# Estensioni di Adobe Experience Platform Launch {#overview.md}

 Adobe Experience Platform Launch è la nuova generazione di funzionalità di gestione dei tag  Adobe. Platform Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate. Launch piattaforma è disponibile per i clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto.

Per un&#39;introduzione alle funzionalità di Experience Platform Launch, consulta le risorse seguenti:
-  documentazione Adobe Experience Platform Launch [](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html)
-  Adobe Experience Platform Launch [video di avvio rapido](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?). Inizia con [Introduzione a  Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) e [Panoramica del processo di pubblicazione](https://helpx.adobe.com/it/analytics/how-to/adobe-launch-publishing-process.html), quindi passa ai concetti successivi.

## Come trovare le estensioni Platform Launch nell&#39;interfaccia della piattaforma {#how-to-find-extensions-in-interface}

Per trovare le estensioni Platform Launch nell&#39;interfaccia della piattaforma, individuare **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** e selezionare **[!UICONTROL Extensions]** nel filtro **[!UICONTROL Types]**.

![Filtro delle estensioni nell&#39;interfaccia](../../assets/catalog/launch-extensions/filter.png)

## Funzionamento delle estensioni del lancio della piattaforma {#how-extensions-work}

Le estensioni Launch piattaforma inoltrano i dati evento non elaborati a diversi tipi di destinazioni. Considerate le estensioni come un tipo di destinazione **Inoltro eventi**. Si tratta di un tipo di integrazione più semplice con le piattaforme di destinazione, che inoltra solo dati di evento non elaborati. Alcuni esempi sono l&#39; [Estensione di personalizzazione del guadagno](../personalization/gainsight.md) o la [Conferma voce dell&#39;estensione del cliente](../voice/confirmit-digital-feedback.md).

**Le destinazioni di** esportazione profilo/segmento nei dati dell&#39;evento Adobe Experience Platform acquisiscono i dati, li combinano con altre origini dati, applicano la segmentazione ed esportano segmenti e profili qualificati per destinazioni. Alcuni esempi sono la [ destinazione di archiviazione cloud Amazon S3](../cloud-storage/amazon-s3.md) o la [destinazione pubblicitaria Google Display &amp; Video 360](../advertising/google-dv360.md).

![Estensioni Experience Platform Launch confrontate con altre destinazioni](../../assets/common/launch-and-other-destinations.png)

## Vantaggi dell&#39;utilizzo delle estensioni del lancio della piattaforma {#extensions-benefits}

 Adobe Experience Platform Launch è gratuito per i clienti  Experienci Cloud esistenti. Platform Launch semplifica la distribuzione dei tag nel sito Web tramite le estensioni di facile utilizzo che puoi installare, configurare, aggiornare ed eliminare. Platform Launch ha un piccolo impatto sul sito Web e consente di mantenere il caricamento delle pagine rapidamente.

>[!IMPORTANT]
>
>Sebbene non sia possibile attivare i segmenti nelle estensioni di Launch piattaforma, è possibile impostare regole per inoltrare solo i dati dell&#39;evento in determinate situazioni. Ulteriori informazioni sono disponibili di seguito.

È possibile creare *regole* che determinano quando inoltrare i dati dell&#39;evento alle estensioni. Questa potente funzionalità consente di inoltrare i dati dell&#39;evento solo in determinate situazioni, anziché inviare i dati dell&#39;evento su ogni interazione. Per ulteriori informazioni, leggi le regole nella [ documentazione Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Esempi di utilizzo per le estensioni del lancio della piattaforma {#extensions-use-cases}

Le estensioni Platform Launch consentono di soddisfare diversi casi di utilizzo da parte dei clienti. Alcuni esempi di utilizzo delle estensioni Launch della piattaforma sono:

- Potete inviare dati di siti Web o app native a Facebook tramite l’estensione pixel di Facebook. Pixel di Facebook indica a quali parti del sito o dell’app ha navigato un visitatore, inoltra tali informazioni a Facebook e puoi nuovamente richiamare il visitatore tramite Facebook.
- Potete inoltrare i dati evento dai siti Web e dalle app alle Google Analytics per analizzare e prendere decisioni in base a tali dati.
- Potete attivare un&#39;app chatbox lato client al momento giusto in base a come gli utenti interagiscono con le pagine, in base alle regole configurate in Lancio piattaforma.

## Categorie di estensione {#extension-categories}

Le estensioni Launch piattaforma possono essere classificate nelle seguenti categorie in Piattaforma:

- [Pubblicità](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Piattaforma di gestione dati](../data-management/overview.md)
- [Destinazioni di marketing e-mail](../email-marketing/overview.md)
- [Personalizzazione](../personalization/overview.md)
- [Sondaggi](../survey/overview.md)
- [Voce del cliente](../voice/overview.md)
