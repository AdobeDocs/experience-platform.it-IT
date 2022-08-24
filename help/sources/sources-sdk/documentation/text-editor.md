---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
solution: Experience Platform
title: Utilizza un editor di testo nel tuo ambiente locale per creare una pagina di documentazione sulle sorgenti
topic-legacy: tutorial
description: Questo documento descrive come utilizzare l’ambiente locale per creare la documentazione relativa all’origine e inviare una richiesta di pull (PR).
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# Utilizza un editor di testo nel tuo ambiente locale per creare una pagina di documentazione di origini

Questo documento descrive come utilizzare l’ambiente locale per creare la documentazione relativa all’origine e inviare una richiesta di pull (PR).

>[!TIP]
>
>Per supportare ulteriormente il processo di documentazione, puoi utilizzare i seguenti documenti della guida al contributo di Adobe: <ul><li>[Installare gli strumenti di creazione Git e Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[Configurare localmente l’archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[Flusso di lavoro dei contributi GitHub per modifiche principali](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## Prerequisiti

L’esercitazione seguente richiede l’installazione di GitHub Desktop nel computer locale. Se non disponi di GitHub Desktop, puoi scaricare l’applicazione [qui](https://desktop.github.com/).

## Connettersi a GitHub e configurare l’ambiente di authoring locale

Il primo passaggio nella configurazione dell’ambiente di authoring locale consiste nel passare alla [Archivio GitHub Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.en).

![piattaforma-repo](../assets/platform-repo.png)

Nella pagina principale dell’archivio Platform GitHub, seleziona **Fork**.

![fork](../assets/fork.png)

Per duplicare l&#39;archivio nel computer locale, seleziona **Codice**. Dal menu a discesa visualizzato, seleziona **HTTPS** quindi seleziona **Apri con GitHub Desktop**.

>[!TIP]
>
>Per ulteriori informazioni, consulta l’esercitazione su [configurazione locale dell’archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

Ora consenti a GitHub Desktop di duplicare il `experience-platform.en` archivio.

![clonazione](../assets/cloning.png)

Una volta completato il processo di clonazione, passa a GitHub Desktop per creare un nuovo ramo. Seleziona **Master** dalla navigazione in alto, quindi seleziona **Nuovo ramo**

![nuovo ramo](../assets/new-branch.png)

Nel pannello di selezione visualizzato, immettete un nome descrittivo per il ramo, quindi selezionate **Crea ramo**.

![create-branch-vs](../assets/create-branch-vs.png)

Quindi, seleziona **Pubblica ramo**.

![ramo di pubblicazione](../assets/publish-branch.png)

## Creare la pagina della documentazione della sorgente

Con l’archivio clonato nel computer locale e creato un nuovo ramo, ora puoi iniziare a creare la pagina di documentazione per la nuova sorgente tramite [editor di testo desiderato](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors).

Adobe consiglia di utilizzare [Codice di Visual Studio](https://code.visualstudio.com/) e di installare l’estensione Adobe Markdown Authoring . Per installare l&#39;estensione, avviare Visual Studio Code e quindi selezionare la **Estensioni** da navigazione a sinistra.

![ Estensione](../assets/extension.png)

Quindi, immetti `Adobe Markdown Authoring` nella barra di ricerca, quindi seleziona **Installa** dalla pagina visualizzata.

![installare](../assets/install.png)

Con il computer locale pronto, scarica il [modello di documentazione di origini](../assets/template.zip) ed estrarre il file in `experience-platform.en/help/sources/tutorials/api/create/...` con [`...`] rappresenta la categoria scelta. Ad esempio, se si sta creando un&#39;origine di database, selezionare la cartella di database.

Infine, segui le istruzioni descritte nel modello e modifica il modello con le informazioni rilevanti relative alla tua origine.

![edit-template](../assets/edit-template.png)

## Invia la documentazione per la revisione

Per creare una richiesta di pull (PR) e inviare la documentazione per la revisione, salva prima il tuo lavoro in [!DNL Visual Studio Code] (o l&#39;editor di testo scelto). Successivamente, utilizzando GitHub Desktop, immetti un messaggio di commit e seleziona **Impegno a creare-sorgente-documentazione**.

![commit-vs](../assets/commit-vs.png)

Quindi, seleziona **Origine push** per caricare il lavoro sul ramo remoto.

![origine push](../assets/push-origin.png)

Per creare una richiesta di pull, seleziona **Crea richiesta di pull**.

![create-pr-vs](../assets/create-pr-vs.png)

Assicurati che i rami di base e di confronto siano corretti. Aggiungi una nota al PR, descrivendo l&#39;aggiornamento, quindi seleziona **Creare una richiesta di pull**. Viene aperto un PR per unire il ramo di lavoro del lavoro nel ramo principale dell’archivio Adobe.

>[!TIP]
>
>Lascia la **Consenti modifiche da parte dei manutentori** seleziona questa casella di controllo per assicurarti che il team della documentazione di Adobe possa apportare modifiche al PR.

![create-pr](../assets/create-pr.png)

Puoi confermare che la richiesta di pull è stata inviata controllando la scheda delle richieste di pull in https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
