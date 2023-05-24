---
title: Documentare l’origine (Streaming SDK)
description: L’ultimo passaggio prima che la nuova origine possa essere pubblicata in Adobe Experience Platform è documentarne la nuova.
hide: true
hidefromtoc: true
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Documentare l’origine (Streaming SDK)

L’ultimo passaggio prima che la nuova origine possa essere impostata live in Adobe Experience Platform è documentare la nuova origine.

Questa guida alla documentazione include:

* Un tutorial che puoi seguire per creare una pagina di documentazione per la nuova sorgente;
* Un modello di documentazione da compilare per la nuova sorgente;
* [Istruzioni su come utilizzare Markdown per la scrittura della documentazione tecnica](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Istruzioni su come comprendere il sapore Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions).

## Prerequisiti

Prima di iniziare a documentare la nuova origine, sono necessari i seguenti elementi:

* **Un account utente GitHub valido**: se non disponi di un account GitHub esistente, devi crearne uno tramite [Pagina di registrazione a GitHub](https://github.com/);
* **Accesso a GitHub Desktop**: utilizza [App desktop GitHub](https://desktop.github.com/) per creare la documentazione di origine nell’ambiente locale;
* L’integrazione con Adobe deve essere in una fase di test con l’origine implementata in un ambiente di staging in Platform.

## Istruzioni di alto livello per creare la documentazione per l’origine in Platform

Ad alto livello, per creare la documentazione per la tua origine, devi creare un fork dell’archivio della documentazione di Platform e modificare il modello di documentazione fornito in un nuovo ramo. Utilizza il modello fornito dall’Adobe per creare una nuova pagina sorgente e aprire una richiesta di pull (PR) quando è il momento. Le istruzioni per eseguire questa operazione sono riportate di seguito, nei passaggi per creare la nuova pagina sorgente.

## Modello di documentazione

Può usare una penna [Modello di documentazione API](streaming-template-api.md) o [Modello di documentazione per l’interfaccia utente](streaming-template-ui.md) per facilitare la creazione della documentazione per la tua origine. Più avanti, puoi trovare istruzioni su come modificare il modello e aprire una richiesta di pull. La documentazione inviata per la nuova origine verrà rivista e pubblicata dal team di documentazione di Adobe.

Puoi scaricare i modelli di documentazione riportati di seguito:

* [Modello di documentazione API](../assets/streaming/streaming-template-api.zip)
* [Modello di documentazione per l’interfaccia utente](../assets/streaming/streaming-template-ui.zip)

## Crea la nuova pagina sorgente

Puoi utilizzare l’interfaccia web GitHub o l’ambiente locale per creare la documentazione per la nuova origine in Platform. Per istruzioni su entrambe le opzioni, consulta i collegamenti seguenti:

* [Utilizza l’interfaccia web GitHub per creare una pagina della documentazione di origine](../documentation/github.md)
* [Utilizza un editor di testo nell’ambiente locale per creare una pagina della documentazione di origine](../documentation/text-editor.md)
