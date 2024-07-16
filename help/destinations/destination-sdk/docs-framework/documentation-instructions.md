---
title: Documentare la destinazione in Adobe Experience Platform
description: Istruzioni dettagliate per la creazione di una pagina di documentazione per la destinazione in Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Documentare la destinazione in Adobe Experience Platform

>[!IMPORTANT]
>
>Il processo qui documentato è necessario solo per i partner che inviano destinazioni (pubbliche) prodotte. Se crei una destinazione privata per il tuo utilizzo, non è necessario creare e pubblicare la documentazione per la destinazione.

## Panoramica {#overview}

Benvenuto in Adobe Experience Platform, grande per averti qui!
La documentazione della destinazione è il passaggio finale prima di poterla impostare live in Adobe Experience Platform.

Questa sezione della documentazione include:

* Istruzioni dettagliate per creare una pagina di documentazione per la nuova destinazione;
* Un modello da compilare per la destinazione;
* [Istruzioni generali sull&#39;utilizzo di Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Istruzioni specifiche per il gusto Markdown Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions) (il gusto Markdown Adobe è molto simile al normale Markdown).
* Una [pagina delle best practice](./authoring-best-practices.md) per aiutarti a creare una pagina di documentazione per la pagina di destinazione che soddisfi gli standard di qualità della documentazione di Experience Platform.

## Prerequisiti {#prerequisites}

Per creare la documentazione per la destinazione in base alle istruzioni riportate in questo articolo, sono necessari i seguenti elementi:

* **Un account GitHub**. Registrati a [GitHub](https://github.com/) se non hai ancora un account.
* **Desktop GitHub**. Se si sceglie di [creare la documentazione nell&#39;ambiente locale](./work-in-local-environment.md), è necessario utilizzare [GitHub Desktop](https://desktop.github.com/).
* L’integrazione con Adobe deve essere in una fase di test con la destinazione implementata in un ambiente di staging in Adobe Experience Platform.

## Istruzioni di alto livello per creare la documentazione per la destinazione in Adobe Experience Platform {#high-level-instructions}

Ad alto livello, per creare la documentazione per la destinazione, devi [creare un fork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) dell&#39;archivio della documentazione di Adobe Experience Platform e modificare il [modello di documentazione fornito](./self-service-template.md) in un nuovo ramo. Utilizza il modello fornito dall’Adobe per creare una nuova pagina di destinazione. Apri una richiesta di pull (PR) quando sei pronto. Le istruzioni per eseguire questa operazione sono riportate di seguito, in [Passaggi per creare la nuova pagina di destinazione](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Modello di documentazione {#documentation-template}

Per facilitare la creazione della pagina della documentazione, Adobe ha precompilato un [modello di documentazione](./self-service-template.md) per te. Più avanti, puoi trovare le istruzioni per modificare il modello e aprire una richiesta di pull. Il team della documentazione di Adobe esaminerà e pubblicherà la documentazione per la nuova destinazione.

[Scarica il modello qui](../assets/docs-framework/yourdestination-template.zip) e decomprimi il file per estrarre il file `yourdestination.md`.

Le istruzioni sull’utilizzo del modello per creare la pagina della documentazione sono riportate di seguito.

## Passaggi per creare la nuova pagina di destinazione {#steps-to-create-docs-page}

Puoi utilizzare l’interfaccia web GitHub o l’ambiente locale per creare la documentazione per la nuova destinazione in Adobe Experience Platform. Per istruzioni su entrambe le opzioni, consulta i collegamenti seguenti:

* [Utilizza l’interfaccia web GitHub per creare una pagina della documentazione di destinazione](./use-github-interface-to-create-documentation.md)
* [Utilizza un editor di testo nell’ambiente locale per creare una pagina della documentazione di destinazione](./work-in-local-environment.md)

## Best practice {#best-practices}

Rivedi le [best practice per l&#39;authoring](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) prima e durante la creazione della pagina della documentazione di destinazione. Assicurati anche di leggere le [istruzioni per la scrittura per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) per altri suggerimenti per la scrittura utilizzati dal team della documentazione di Adobe durante l&#39;authoring della documentazione.