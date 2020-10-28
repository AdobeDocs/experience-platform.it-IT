---
keywords: launch extensions;launch extension;launch destinations; platform launch extensions;platform launch extension;platform launch destinations
title: Estensioni di Experience Platform Launch
seo-title: Estensioni di Experience Platform Launch
description: Launch è la soluzione Adobe di nuova generazione per la gestione dei tag. Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate.
seo-description: Launch è la soluzione Adobe di nuova generazione per la gestione dei tag. Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate.
translation-type: tm+mt
source-git-commit: 6bb7bbeaceac8a69641138248a1c41cf9fb3dc63
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 21%

---


# Estensioni di Adobe Experience Platform Launch {#experience-platform-launch-extensions}

 Adobe Experience Platform Launch è la nuova generazione di funzionalità di gestione dei tag  Adobe. Platform Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate. Launch piattaforma è disponibile per i clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto.

Per un&#39;introduzione alle funzionalità di Experience Platform Launch, consulta le risorse seguenti:
* Adobe Experience Platform Launch [documentation](https://docs.adobe.com/content/help/it-IT/launch/using/overview.html)
* Adobe Experience Platform Launch [quick start videos](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html). Inizia con [Introduzione a  panoramica](https://www.youtube.com/embed/rwqqkG1SERU) del processo di Adobe Experience Platform Launch [e](https://helpx.adobe.com/it/analytics/how-to/adobe-launch-publishing-process.html)pubblicazione, quindi passa ai concetti successivi.

## Come trovare le estensioni Platform Launch nell&#39;interfaccia CDP  Adobe in tempo reale {#how-to-find-extensions-in-interface}

Per trovare le estensioni Platform Launch nell&#39;interfaccia CDP  Adobe in tempo reale, accedere a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** e selezionare **[!UICONTROL Extensions]** il **[!UICONTROL Types]** filtro.

![Filtro delle estensioni nell&#39;interfaccia](/help/rtcdp/destinations/assets/extensions-filter.png)

## Funzionamento delle estensioni Launch piattaforma {#how-extensions-work}

Le estensioni Launch piattaforma inoltrano i dati evento non elaborati a diversi tipi di destinazioni. Considerate le estensioni come un tipo di destinazione di inoltro **** degli eventi. Si tratta di un tipo di integrazione più semplice con le piattaforme di destinazione, che inoltra solo dati di evento non elaborati. Esempi di questi sono l&#39;estensione [di personalizzazione](/help/rtcdp/destinations/gainsight-extension.md) Gainsight o la [voce Conferma dell&#39;estensione](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)del cliente.

**Destinazioni di esportazione** profilo/segmento nel  Adobe Acquisizione dati evento in tempo reale dalla piattaforma dati cliente, combinate con altre origini dati, applicate segmentazione ed esportate segmenti e profili qualificati per destinazioni. Esempi di questi sono la destinazione [di archiviazione cloud](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 o la destinazione [pubblicitaria](/help/rtcdp/destinations/google-dv360-destination.md)Google Display &amp; Video 360.

![Estensioni Experience Platform Launch confrontate con altre destinazioni](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Vantaggi dell&#39;utilizzo delle estensioni Platform Launch {#extensions-benefits}

 Adobe Experience Platform Launch è gratuito per i clienti  Experienci Cloud esistenti. Platform Launch semplifica la distribuzione dei tag nel sito Web tramite le estensioni di facile utilizzo che puoi installare, configurare, aggiornare ed eliminare. Platform Launch ha un piccolo impatto sul sito Web e consente di mantenere il caricamento delle pagine rapidamente.

>[!IMPORTANT]
>
>Sebbene non sia possibile attivare i segmenti nelle estensioni di Launch piattaforma, è possibile impostare regole per inoltrare solo i dati dell&#39;evento in determinate situazioni. Ulteriori informazioni sono disponibili di seguito.

È possibile creare *regole* che determinano quando inoltrare i dati dell&#39;evento alle estensioni. Questa potente funzionalità consente di inoltrare i dati dell&#39;evento solo in determinate situazioni, anziché inviare i dati dell&#39;evento su ogni interazione. Per ulteriori informazioni, consulta le regole contenute nella documentazione [](https://docs.adobe.com/help/it-IT/launch/using/reference/manage-resources/rules.html)Adobe Experience Platform Launch.

## Esempi di utilizzo per le estensioni Platform Launch {#extensions-use-cases}

Le estensioni Platform Launch consentono di soddisfare diversi casi di utilizzo da parte dei clienti. Alcuni esempi di utilizzo delle estensioni Launch della piattaforma sono:

* Potete inviare dati di siti Web o app native a Facebook tramite l’estensione pixel di Facebook. Pixel di Facebook indica a quali parti del sito o dell’app ha navigato un visitatore, inoltra tali informazioni a Facebook e puoi nuovamente richiamare il visitatore tramite Facebook.
* Potete inoltrare i dati evento dai siti Web e dalle app alle Google Analytics per analizzare e prendere decisioni in base a tali dati.
* Potete attivare un&#39;app chatbox lato client al momento giusto in base a come gli utenti interagiscono con le pagine, in base alle regole configurate in Lancio piattaforma.


## Categorie di estensioni {#extension-categories}

Le estensioni di Launch piattaforma possono rientrare nelle seguenti categorie  CDP in tempo reale del Adobe:

* [Pubblicità](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Piattaforma di gestione dati](/help/rtcdp/destinations/dmp-destinations.md)
* [Destinazioni di marketing e-mail](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personalizzazione](/help/rtcdp/destinations/personalization-destinations.md)
* [Sondaggi](/help/rtcdp/destinations/survey-destinations.md)
* [Voce del cliente](/help/rtcdp/destinations/voice-of-customer-destinations.md)
