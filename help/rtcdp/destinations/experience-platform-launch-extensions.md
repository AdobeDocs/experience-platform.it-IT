---
keywords: launch extensions;launch extension;launch destinations
title: Estensioni Experience Platform Launch
seo-title: Estensioni Experience Platform Launch
description: Launch è la soluzione Adobe di nuova generazione per la gestione dei tag. Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate.
seo-description: Launch è la soluzione Adobe di nuova generazione per la gestione dei tag. Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 21%

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

Experience Platform Launch è la soluzione Adobe di nuova generazione per la gestione dei tag. Launch offre ai clienti un modo semplice di implementare e gestire tutti i tag pubblicitari, di analisi e di marketing necessari per fornire ai clienti esperienze personalizzate. Launch viene offerto ai clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto.

Per un&#39;introduzione alle funzionalità di Experience Platform Launch, consulta le risorse seguenti:
* Experience Platform Launch [documentation](https://docs.adobe.com/content/help/it-IT/launch/using/overview.html)
* Experience Platform Launch video [di avvio rapido](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html). Inizia con [Introduzione alla panoramica](https://www.youtube.com/embed/rwqqkG1SERU) del processo di Experience Platform Launch [e](https://helpx.adobe.com/it/analytics/how-to/adobe-launch-publishing-process.html)pubblicazione, quindi passa ai concetti successivi.

## Come trovare le estensioni Launch nel Adobe  Interfaccia CDP in tempo reale {#how-to-find-extensions-in-interface}

Per trovare le estensioni Launch nell&#39;interfaccia CDP in tempo reale del Adobe , accedere a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** e selezionare **[!UICONTROL Extensions]** il **[!UICONTROL Types]** filtro.

![Filtro delle estensioni nell&#39;interfaccia](/help/rtcdp/destinations/assets/extensions-filter.png)

## Funzionamento delle estensioni Launch {#how-extensions-work}

Avviate le estensioni per inoltrare i dati degli eventi non elaborati a diversi tipi di destinazioni. Considerate le estensioni come un tipo di destinazione di inoltro **** degli eventi. Si tratta di un tipo di integrazione più semplice con le piattaforme di destinazione, che inoltra solo dati di evento non elaborati. Esempi di questi sono l&#39;estensione [di personalizzazione](/help/rtcdp/destinations/gainsight-extension.md) Gainsight o la [voce Conferma dell&#39;estensione](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)del cliente.

**Destinazioni di esportazione** profilo/segmento nel  Adobe Acquisizione dati evento in tempo reale dalla piattaforma dati cliente, combinate con altre origini dati, applicate segmentazione ed esportate segmenti e profili qualificati per destinazioni. Esempi di questi sono la destinazione [di archiviazione cloud](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 o la destinazione [pubblicitaria](/help/rtcdp/destinations/google-dv360-destination.md)Google Display &amp; Video 360.

![Estensioni Experience Platform Launch confrontate con altre destinazioni](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Vantaggi dell’utilizzo delle estensioni Launch {#extensions-benefits}

Il Experience Platform Launch è gratuito per i clienti  Experience Cloud esistenti. Launch semplifica la distribuzione dei tag nel sito Web mediante estensioni facili da usare che possono essere installate, configurate, aggiornate ed eliminate. Launch presenta un piccolo ingombro sul sito Web e consente di mantenere il caricamento delle pagine rapidamente.

>[!IMPORTANT]
>
>Anche se non è possibile attivare i segmenti per le estensioni Launch, è possibile impostare regole per inoltrare solo i dati dell&#39;evento in determinate situazioni. Ulteriori informazioni sono disponibili di seguito.

È possibile creare *regole* che determinano quando inoltrare i dati dell&#39;evento alle estensioni. Questa potente funzionalità consente di inoltrare i dati dell&#39;evento solo in determinate situazioni, anziché inviare i dati dell&#39;evento su ogni interazione. Per ulteriori informazioni, consulta le regole nella documentazione [](https://docs.adobe.com/help/it-IT/launch/using/reference/manage-resources/rules.html)Launch.

## Esempi di utilizzo per le estensioni Launch {#extensions-use-cases}

Le estensioni Launch consentono di soddisfare diversi casi di utilizzo da parte del cliente. Alcuni esempi di utilizzo delle estensioni Launch sono:

* Potete inviare dati di siti Web o app native a Facebook tramite l’estensione pixel di Facebook. Pixel di Facebook indica a quali parti del sito o dell’app ha navigato un visitatore, inoltra tali informazioni a Facebook e puoi nuovamente richiamare il visitatore tramite Facebook.
* Potete inoltrare i dati evento dai siti Web e dalle app alle Google Analytics per analizzare e prendere decisioni in base a tali dati.
* Potete attivare un&#39;app chatbox lato client al momento giusto in base a come gli utenti interagiscono con le pagine, in base alle regole impostate in Launch.


## Categorie di estensioni {#extension-categories}

Le estensioni di avvio possono rientrare nelle seguenti categorie  CDP in tempo reale del Adobe:

* [Pubblicità](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Piattaforma di gestione dati](/help/rtcdp/destinations/dmp-destinations.md)
* [Destinazioni di marketing e-mail](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personalizzazione](/help/rtcdp/destinations/personalization-destinations.md)
* [Sondaggi](/help/rtcdp/destinations/survey-destinations.md)
* [Voce del cliente](/help/rtcdp/destinations/voice-of-customer-destinations.md)
