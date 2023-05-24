---
title: Utilizza un editor di testo nell’ambiente locale per creare una pagina della documentazione di destinazione
description: Le istruzioni in questa pagina mostrano come utilizzare un editor di testo per lavorare nel tuo ambiente locale per creare una pagina di documentazione per la tua destinazione di Experience Platform e inviarla per la revisione.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# Utilizza un editor di testo nell’ambiente locale per creare una pagina della documentazione di destinazione {#local-authoring}

Le istruzioni in questa pagina mostrano come utilizzare un editor di testo per lavorare nell’ambiente locale per creare la documentazione e inviare una richiesta di pull (PR). Prima di eseguire i passaggi qui indicati, assicurati di leggere [Documentare la destinazione in Destinazioni Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulta anche la documentazione di supporto nella guida per i collaboratori di Adobe:
>* [Installare gli strumenti di creazione Git e Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configurare localmente l’archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Flusso di lavoro dei contributi GitHub per modifiche principali](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Connessione a GitHub e configurazione dell’ambiente di authoring locale {#set-up-environment}

1. Nel browser, passa a `https://github.com/AdobeDocs/experience-platform.en`
2. A [fork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) nell’archivio, fai clic su **Fork** come mostrato di seguito. In questo modo viene creata una copia dell’archivio di Experienci Platform nel tuo account GitHub.

   ![Archivio della documentazione di Fork Adobe](../assets/docs-framework/ssd-fork-repository.gif)

3. Clonare l’archivio sul computer locale. Seleziona **Codice > HTTPS > Apri con desktop GitHub**, come illustrato di seguito. Assicurati di avere [Desktop GitHub](https://desktop.github.com/) installato. Per ulteriori informazioni, leggere [Creare un clone locale dell’archivio](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) nella guida per i collaboratori Adobe.

   ![Clona l’archivio della documentazione di Adobe nell’ambiente locale](../assets/docs-framework/clone-local.png)

4. Nella struttura del file locale, passa a `experience-platform.en/help/destinations/catalog/[...]`, dove `[...]` è la categoria desiderata per la destinazione. Ad Experience Platform, se stai aggiungendo una destinazione di personalizzazione a, seleziona la `personalization` cartella.

## Creare la pagina della documentazione per la destinazione {#author-documentation}

1. La pagina della documentazione si basa su [modello di destinazione self-service](../docs-framework/self-service-template.md). Scarica il file [modello di destinazione](../assets/docs-framework/yourdestination-template.zip). Decomprimi ed estrai il file `yourdestination-template.md` nella directory indicata al punto 4.  Rinomina il file `YOURDESTINATION.md`, dove YOURDESTINATION è il nome della destinazione in Adobe Experience Platform. Ad esempio, se la tua società si chiama Moviestar, dovrai denominare il file `moviestar.md`.
2. Apri il nuovo file nel tuo [editor di testo preferito](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). L’Adobe consiglia di utilizzare [Codice di Visual Studio](https://code.visualstudio.com/) e installa l’estensione Adobe Markdown Authoring. Per installare l&#39;estensione, aprire Visual Studio Code, selezionare **[!DNL Extensions]** sulla sinistra dello schermo e cerca `adobe markdown authoring`. Seleziona l’estensione e fai clic su **[!DNL Install]**.
   ![Installare l’estensione Adobe Markdown Authoring](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Modifica il modello con le informazioni rilevanti per la destinazione. Segui le istruzioni nel modello.
4. Per le schermate o le immagini da aggiungere alla documentazione, vai a `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, dove `[...]` è la categoria desiderata per la destinazione. Ad Experience Platform, se stai aggiungendo una destinazione di personalizzazione a, seleziona la `personalization` cartella. Crea una nuova cartella per la destinazione e salva qui le immagini. Devi creare un collegamento a tali elementi dalla pagina in cui vengono creati. Consulta [istruzioni su come collegare le immagini](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. Quando si è pronti, salvare il file su cui si sta lavorando.

## Inviare la documentazione per la revisione {#submit-review}

>[!TIP]
>
>Tieni presente che qui non è possibile interrompere nulla. Attenendoti alle istruzioni riportate in questa sezione, ti basta suggerire un aggiornamento della documentazione. L’aggiornamento suggerito verrà approvato o modificato dal team di documentazione di Adobe Experience Platform.

1. In GitHub Desktop, crea un ramo di lavoro per gli aggiornamenti e seleziona **Pubblica ramo** per pubblicare il ramo su GitHub.

![Nuovo ramo locale](../assets/docs-framework/new-branch-local.gif)

1. Nel desktop GitHub, [commit](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) il tuo lavoro, come illustrato di seguito.

   ![Conferma locale](../assets/docs-framework/commit-local.png)

1. Nel desktop GitHub, [push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) il tuo lavoro per [remoto](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) come mostrato di seguito.

   ![Effettua push del commit](../assets/docs-framework/push-local-to-remote.png)

1. Nell’interfaccia web GitHub, apri una richiesta di pull (PR) per unire il ramo di lavoro nel ramo principale dell’archivio della documentazione di Adobe. Assicurati che il ramo su cui hai lavorato sia selezionato e seleziona **Contribute > Apri richiesta pull**.

   ![Creare una richiesta di pull](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Assicurati che i rami di base e di confronto siano corretti. Aggiungi una nota alla PR, descrivendo l’aggiornamento, e seleziona **Creare una richiesta di pull**. Viene aperto un PR per unire il ramo di lavoro del fork nel ramo principale dell’archivio di Adobi.
   >[!TIP]
   >
   >Lascia **Consenti modifiche da parte dei gestori** è stata selezionata una casella di controllo che consente al team della documentazione di Adobe di apportare modifiche alla PR.

   ![Creazione di una richiesta di pull nell’archivio della documentazione Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. A questo punto, viene visualizzata una notifica che richiede di firmare il Contratto di licenza da collaboratore (CLA) di Adobe. Questo è un passaggio obbligatorio. Dopo aver firmato il contratto di licenza, aggiorna la pagina PR e invia la richiesta di pull.

1. Puoi confermare che la richiesta di pull è stata inviata esaminando **Richieste pull** scheda in `https://github.com/AdobeDocs/experience-platform.en`.

![PR riuscito](../assets/docs-framework/ssd-pr-successful.png)

1. Grazie. Il team di documentazione di Adobe si rivolgerà al PR nel caso siano necessarie modifiche e ti informerà di quando la documentazione verrà pubblicata.

>[!TIP]
>
>Per aggiungere immagini e collegamenti alla documentazione e per eventuali altre domande su Markdown, leggi [Utilizzo di Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) nella guida alla scrittura collaborativa di Adobe.
