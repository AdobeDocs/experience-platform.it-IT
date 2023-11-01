---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
solution: Experience Platform
title: Utilizzare un editor di testo nell’ambiente locale per creare una pagina della documentazione di Sources
description: Questo documento descrive come utilizzare l’ambiente locale per creare la documentazione per la tua origine e inviare una richiesta di pull (PR).
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 3%

---

# Utilizza un editor di testo nell’ambiente locale per creare una pagina della documentazione delle sorgenti

Questo documento descrive come utilizzare l’ambiente locale per creare la documentazione per la tua origine e inviare una richiesta di pull (PR).

>[!TIP]
>
>I seguenti documenti della guida introduttiva di Adobe possono essere utilizzati per supportare ulteriormente la procedura di documentazione: <ul><li>[Installare gli strumenti di creazione Git e Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[Configurare localmente l’archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[Flusso di lavoro dei contributi GitHub per modifiche principali](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## Prerequisiti

Il seguente tutorial richiede che GitHub Desktop sia installato sul computer locale. Se non disponi di GitHub Desktop, puoi scaricare l’applicazione [qui](https://desktop.github.com/).

## Connessione a GitHub e configurazione dell’ambiente di authoring locale

Il primo passaggio nella configurazione dell’ambiente di authoring locale consiste nel passare alla [Archivio GitHub Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

Nella pagina principale dell’archivio GitHub di Platform, seleziona **Fork**.

![fork](../assets/fork.png)

Per clonare l’archivio sul computer locale, seleziona **Codice**. Dal menu a discesa visualizzato, seleziona **HTTPS** quindi, seleziona **Apri con GitHub Desktop**.

>[!TIP]
>
>Per ulteriori informazioni, consulta l’esercitazione su [configurazione locale dell’archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

Quindi, attendi alcuni istanti prima che GitHub Desktop cloni il `experience-platform.en` archivio.

![clonazione](../assets/cloning.png)

Una volta completato il processo di clonazione, passa a GitHub Desktop per creare un nuovo ramo. Seleziona **Principale** dalla navigazione in alto, quindi seleziona **Nuovo ramo**

![new-branch](../assets/new-branch.png)

Nel pannello a comparsa visualizzato, immetti un nome descrittivo per il ramo, quindi seleziona **Crea ramo**.

![create-branch-vs](../assets/create-branch-vs.png)

Quindi, seleziona **Pubblica ramo**.

![publish-branch](../assets/publish-branch.png)

## Creare la pagina della documentazione per la sorgente

Dopo aver clonato l’archivio nel computer locale e creato un nuovo ramo, puoi iniziare a creare la pagina della documentazione per la nuova origine tramite [editor di testo desiderato](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors).

L’Adobe consiglia di utilizzare [Codice di Visual Studio](https://code.visualstudio.com/) e installare l’estensione Adobe Markdown Authoring. Per installare l&#39;estensione, avviare Visual Studio Code, quindi selezionare **Estensioni** dal menu di navigazione a sinistra.

![ Estensione](../assets/extension.png)

Quindi, immetti `Adobe Markdown Authoring` nella barra di ricerca, quindi seleziona **Installa** dalla pagina visualizzata.

![installare](../assets/install.png)

Quando il computer locale è pronto, scarica il [modello di documentazione delle sorgenti](../assets/api-template.zip) ed estrarre il file in `experience-platform.en/help/sources/tutorials/api/create/...` con [`...`] rappresenta la categoria scelta. Se ad esempio si sta creando un&#39;origine di database, selezionare la cartella del database.

Infine, segui le istruzioni descritte nel modello e modifica il modello con le informazioni pertinenti relative alla tua origine.

![edit-template](../assets/edit-template.png)

## Inviare la documentazione per la revisione

Per creare una richiesta di pull (PR) e inviare la documentazione per la revisione, salva il lavoro in [!DNL Visual Studio Code] (o l’editor di testo scelto). Quindi, utilizzando GitHub Desktop, immetti un messaggio di commit e seleziona **Conferma creazione-origine-documentazione**.

![commit-vs](../assets/commit-vs.png)

Quindi, seleziona **Origine push** per caricare il lavoro nel ramo remoto.

![push-origin](../assets/push-origin.png)

Per creare una richiesta di pull, seleziona **Crea richiesta di pull**.

![create-pr-vs](../assets/create-pr-vs.png)

Assicurati che i rami di base e di confronto siano corretti. Aggiungi una nota alla PR, descrivendo l’aggiornamento, quindi seleziona **Creare una richiesta di pull**. Verrà aperta una PR per unire il ramo di lavoro nel ramo principale dell’archivio di Adobi.

>[!TIP]
>
>Lascia **Consenti modifiche da parte dei gestori** è stata selezionata una casella di controllo per garantire che il team della documentazione Adobe possa apportare modifiche alla PR.

![create-pr](../assets/create-pr.png)

Puoi confermare che la richiesta di pull è stata inviata esaminando la scheda delle richieste di pull in https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
