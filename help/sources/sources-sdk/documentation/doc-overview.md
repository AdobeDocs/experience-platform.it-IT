---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
solution: Experience Platform
title: Documentare il Source
description: L’ultimo passaggio prima che la nuova origine possa essere pubblicata in Adobe Experience Platform è documentarne la nuova.
exl-id: 80daadb1-127f-4f42-8bc9-fb89a7898462
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Documenta la sorgente

L’ultimo passaggio prima che la nuova origine possa essere impostata live in Adobe Experience Platform è documentare la nuova origine.

Questa guida alla documentazione include:

* Un tutorial che puoi seguire per creare una pagina di documentazione per la nuova sorgente;
* Un modello di documentazione da compilare per la nuova sorgente;
* [Istruzioni sull&#39;utilizzo di Markdown per la scrittura della documentazione tecnica](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Istruzioni su come comprendere il sapore Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions).

## Prerequisiti

Prima di iniziare a documentare la nuova origine, sono necessari i seguenti elementi:

* **Un account utente GitHub valido**: se non disponi di un account GitHub esistente, devi crearne uno tramite la [pagina di iscrizione a GitHub](https://github.com/);
* **Accesso a GitHub Desktop**: è necessario utilizzare l&#39;app desktop [GitHub](https://desktop.github.com/) per creare la documentazione di origine nell&#39;ambiente locale;
* L’integrazione con Adobe deve essere in una fase di test con l’origine implementata in un ambiente di staging in Platform.

## Istruzioni di alto livello per creare la documentazione per l’origine in Platform

Ad alto livello, per creare la documentazione per la tua origine, devi creare un fork dell’archivio della documentazione di Platform e modificare il modello di documentazione fornito in un nuovo ramo. Utilizza il modello fornito dall’Adobe per creare una nuova pagina sorgente e aprire una richiesta di pull (PR) quando è il momento. Le istruzioni per eseguire questa operazione sono riportate di seguito, nei passaggi per creare la nuova pagina sorgente.

## Modello di documentazione

Puoi utilizzare un [modello di documentazione](./template.md) precompilato per facilitare la creazione della documentazione per la tua origine. Più avanti, puoi trovare istruzioni su come modificare il modello e aprire una richiesta di pull. La documentazione inviata per la nuova origine verrà rivista e pubblicata dal team di documentazione di Adobe.

Puoi scaricare i modelli di documentazione riportati di seguito:

* [Modello di documentazione API](../assets/api-template.zip)
* [Modello di documentazione per l’interfaccia utente](../assets/ui-template.zip)

## Crea la nuova pagina sorgente

Puoi utilizzare l’interfaccia web GitHub o l’ambiente locale per creare la documentazione per la nuova origine in Platform. Per istruzioni su entrambe le opzioni, consulta i collegamenti seguenti:

* [Utilizza l’interfaccia web GitHub per creare una pagina della documentazione di origine](./github.md)
* [Utilizza un editor di testo nell’ambiente locale per creare una pagina della documentazione di origine](./text-editor.md)
