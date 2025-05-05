---
title: Documentare il Source (Streaming SDK)
description: L’ultimo passaggio prima che la nuova origine possa essere pubblicata in Adobe Experience Platform è documentarne la nuova.
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Documenta la sorgente (Streaming SDK)

>[!NOTE]
>
>Origini self-service Streaming SDK è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

L’ultimo passaggio prima che la nuova origine possa essere impostata live in Adobe Experience Platform è documentare la nuova origine.

Questa guida alla documentazione include:

* Un tutorial che puoi seguire per creare una pagina di documentazione per la nuova sorgente;
* Un modello di documentazione da compilare per la nuova sorgente;
* [Istruzioni sull&#39;utilizzo di Markdown per la scrittura della documentazione tecnica](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=it);
* [Istruzioni su come comprendere Adobe Markdown flavor](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=it#custom-markdown-extensions).

## Prerequisiti

Prima di iniziare a documentare la nuova origine, sono necessari i seguenti elementi:

* **Un account utente GitHub valido**: se non disponi di un account GitHub esistente, devi crearne uno tramite la [pagina di iscrizione a GitHub](https://github.com/);
* **Accesso a GitHub Desktop**: è necessario utilizzare l&#39;app desktop [GitHub](https://desktop.github.com/) per creare la documentazione di origine nell&#39;ambiente locale;
* L’integrazione con Adobe deve essere in una fase di test con l’origine implementata in un ambiente di staging in Experience Platform.

## Istruzioni di alto livello per la creazione di documentazione per la sorgente in Experience Platform

Ad alto livello, per creare la documentazione per la tua origine, devi creare un fork dell’archivio della documentazione di Experience Platform e modificare il modello di documentazione fornito in un nuovo ramo. Utilizza il modello fornito da Adobe per creare una nuova pagina sorgente e aprire una richiesta di pull (PR) quando è il momento. Le istruzioni per eseguire questa operazione sono riportate di seguito, nei passaggi per creare la nuova pagina sorgente.

## Modello di documentazione

Puoi utilizzare un [modello di documentazione API](streaming-template-api.md) precompilato o il [modello di documentazione dell&#39;interfaccia utente](streaming-template-ui.md) per facilitare la creazione della documentazione per la tua origine. Più avanti, puoi trovare istruzioni su come modificare il modello e aprire una richiesta di pull. La documentazione inviata per la nuova origine verrà rivista e pubblicata dal team di documentazione di Adobe.

Puoi scaricare i modelli di documentazione riportati di seguito:

* [Modello di documentazione API](../assets/streaming/streaming-template-api.zip)
* [Modello di documentazione per l’interfaccia utente](../assets/streaming/streaming-template-ui.zip)

## Crea la nuova pagina sorgente

Puoi utilizzare l’interfaccia web GitHub o l’ambiente locale per creare la documentazione per la nuova origine in Experience Platform. Per istruzioni su entrambe le opzioni, consulta i collegamenti seguenti:

* [Utilizza l’interfaccia web GitHub per creare una pagina della documentazione di origine](../documentation/github.md)
* [Utilizza un editor di testo nell’ambiente locale per creare una pagina della documentazione di origine](../documentation/text-editor.md)
