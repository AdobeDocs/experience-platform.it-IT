---
title: Documentare la destinazione in Adobe Experience Platform
description: Istruzioni dettagliate per creare una pagina di documentazione per la destinazione in Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: dd4a150351b5e0c41586cf663324aeb345a896e4
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# Documentare la destinazione in Adobe Experience Platform

>[!IMPORTANT]
>
>Il processo qui documentato è necessario solo per i partner che inviano destinazioni prodotte (pubbliche). Se crei una destinazione privata per tuo uso, non devi creare e pubblicare la documentazione per la tua destinazione.

## Panoramica {#overview}

Benvenuto in Adobe Experience Platform, grande per averti qui!
Documentare la destinazione è l&#39;ultimo passaggio prima che possa essere impostata in tempo reale in Adobe Experience Platform.

Questa sezione della documentazione include:

* Istruzioni dettagliate per creare una pagina di documentazione per la nuova destinazione;
* Un modello da compilare per la destinazione;
* [Istruzioni generali sull’utilizzo di Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Istruzioni specifiche per l’Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions) (il sapore Adobe Markdown è molto simile al normale Markdown).
* A [pagina delle best practice](./authoring-best-practices.md) per facilitare la creazione di una pagina di documentazione per la pagina di destinazione, che soddisfi gli standard Experienci Platform di qualità della documentazione.

## Prerequisiti {#prerequisites}

Per creare la documentazione per la destinazione in base alle istruzioni contenute in questo articolo, sono necessari i seguenti elementi:

* **Un account GitHub**. Iscriviti a [GitHub](https://github.com/) se non avete ancora un account.
* **Desktop GitHub**. Se selezioni [creare la documentazione nell’ambiente locale](./work-in-local-environment.md), è necessario utilizzare [Desktop GitHub](https://desktop.github.com/).
* L&#39;integrazione con Adobe deve trovarsi in una fase di test con la destinazione distribuita in un ambiente di staging in Adobe Experience Platform.

## Istruzioni di alto livello per creare la documentazione per la destinazione in Adobe Experience Platform {#high-level-instructions}

Ad un livello elevato, per creare la documentazione per la tua destinazione, devi [creare un fork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) dell’archivio della documentazione di Adobe Experience Platform e modifica il [modello di documentazione fornito](./self-service-template.md) in un nuovo ramo. Utilizza il modello fornito dall’Adobe per creare una nuova pagina di destinazione. Apri una richiesta di pull (PR) quando sei pronto. Le istruzioni per eseguire questa operazione sono più avanti, in [Passaggi per creare la nuova pagina di destinazione](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Modello di documentazione {#documentation-template}

Per aiutarti a creare la pagina della documentazione, Adobe ha precompilato un [modello di documentazione](./self-service-template.md) per te. Di seguito, trovi istruzioni su come modificare il modello e aprire una richiesta di pull. Il team di documentazione di Adobe esaminerà e pubblicherà la documentazione per la nuova destinazione.

[Scarica il modello qui](assets/yourdestination-template.zip) e decomprimi il file per estrarre il `yourdestination.md` file.

Di seguito sono riportate ulteriori istruzioni sull’utilizzo del modello per creare la pagina della documentazione.

## Passaggi per creare la nuova pagina di destinazione {#steps-to-create-docs-page}

Puoi utilizzare l’interfaccia web GitHub o l’ambiente locale per creare la documentazione per la nuova destinazione in Adobe Experience Platform. Trova le istruzioni per entrambe le opzioni nei collegamenti seguenti:

* [Utilizza l’interfaccia web GitHub per creare una pagina di documentazione di destinazione](./use-github-interface-to-create-documentation.md)
* [Utilizza un editor di testo nel tuo ambiente locale per creare una pagina di documentazione di destinazione](./work-in-local-environment.md)

## Best practice {#best-practices}

Consulta la sezione [best practice di authoring](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) prima e durante la creazione della pagina della documentazione di destinazione. Assicurati anche di leggere il [guida alla scrittura per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) per ulteriori suggerimenti per la scrittura utilizzati dal team di documentazione di Adobe durante l’authoring della documentazione.