---
title: Utilizza un editor di testo nel tuo ambiente locale per creare una pagina di documentazione di destinazione
description: Le istruzioni riportate in questa pagina mostrano come utilizzare un editor di testo per lavorare nell’ambiente locale per creare una pagina di documentazione per la destinazione dell’Experience Platform e inviarla per la revisione.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: 1bbff0fa54f1b7ef1ee70efd2a85cd43b34b2f5a
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# Utilizza un editor di testo nel tuo ambiente locale per creare una pagina di documentazione di destinazione {#local-authoring}

Le istruzioni presenti in questa pagina mostrano come utilizzare un editor di testo per lavorare nel proprio ambiente locale per creare la documentazione e inviare una richiesta di pull (PR). Prima di eseguire i passaggi qui indicati, leggi [Documentare la destinazione in Adobe Experience Platform Destinations](./documentation-instructions.md).

>[!TIP]
>
>Consulta anche la documentazione di supporto nella guida per i collaboratori di Adobe:
>* [Installare gli strumenti di creazione Git e Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configurare localmente l’archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Flusso di lavoro dei contributi GitHub per modifiche principali](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Connettersi a GitHub e configurare l’ambiente di authoring locale {#set-up-environment}

1. Nel browser, passa a `https://github.com/AdobeDocs/experience-platform.en`
2. Per [fork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) l&#39;archivio, fai clic su **Fork** come mostrato di seguito. In questo modo viene creata una copia dell’archivio Experience Platform nel tuo account GitHub.

   ![Archivio della documentazione di Adobe fork](./assets/ssd-fork-repository.gif)

3. Clonare l’archivio sul computer locale. Seleziona **Codice > HTTPS > Apri con GitHub Desktop**, come mostrato di seguito. Assicurati di aver installato [GitHub Desktop](https://desktop.github.com/). Per ulteriori riferimenti, consulta [Creare un clone locale dell’archivio](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) nella guida per i collaboratori di Adobe .

   ![Clona l’archivio della documentazione di Adobe in ambiente locale](./assets/clone-local.png)

4. Nella struttura del file locale, passa a `experience-platform.en/help/destinations/catalog/[...]`, dove `[...]` è la categoria desiderata per la destinazione. Ad Experience Platform, se aggiungi una destinazione di personalizzazione, seleziona la cartella `personalization` .

## Creare la pagina della documentazione per la destinazione {#author-documentation}

1. La pagina della documentazione si basa sul [modello di destinazione self-service](./self-service-template.md). Scarica il [modello di destinazione](assets/yourdestination-template.zip). Decomprimetela ed estraete il file `yourdestination-template.md` nella directory indicata al punto 4.  Rinomina il file `YOURDESTINATION.md`, dove YOURDESTINATION è il nome della destinazione in Adobe Experience Platform. Ad esempio, se l’azienda si chiama Moviestar, devi assegnare un nome al file `moviestar.md`.
2. Apri il nuovo file nell&#39; [editor di testo selezionato](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). Adobe consiglia di utilizzare [Codice di Visual Studio](https://code.visualstudio.com/) e installare l&#39;estensione Adobe Markdown Authoring. Per installare l&#39;estensione, apri Codice di Visual Studio, seleziona la scheda **[!DNL Extensions]** a sinistra dello schermo e cerca `adobe markdown authoring`. Seleziona l’estensione e fai clic su **[!DNL Install]**.
   ![Installare l’estensione Adobe Markdown Authoring](./assets/install-adobe-markdown-extension.gif)
3. Modifica il modello con le informazioni rilevanti per la destinazione. Segui le istruzioni contenute nel modello .
4. Per tutte le schermate o immagini che intendi aggiungere alla documentazione, passa a `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, dove `[...]` è la categoria desiderata per la destinazione. Ad Experience Platform, se aggiungi una destinazione di personalizzazione, seleziona la cartella `personalization` . Crea una nuova cartella per la tua destinazione e salva le immagini qui. Devi effettuare un collegamento a tali elementi dalla pagina che stai creando. Consulta [istruzioni su come collegare immagini](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. Quando sei pronto, salva il file su cui stai lavorando.

## Invia la documentazione per la revisione {#submit-review}

>[!TIP]
>
>Notate che non c&#39;è niente che potete rompere qui. Seguendo le istruzioni contenute in questa sezione, ti consigliamo semplicemente un aggiornamento della documentazione. L’aggiornamento consigliato verrà approvato o modificato dal team di documentazione di Adobe Experience Platform.

1. In GitHub Desktop, crea un ramo di lavoro per gli aggiornamenti e seleziona **Pubblica ramo** per pubblicare il ramo in GitHub.

![Nuovo ramo locale](./assets/new-branch-local.gif)

1. In GitHub Desktop, [esegui il commit](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) del tuo lavoro, come mostrato di seguito.

   ![Conferma locale](./assets/commit-local.png)

1. In GitHub Desktop, [invia](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) il lavoro al ramo [remoto](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote), come mostrato di seguito.

   ![Spingi il tuo commit](./assets/push-local-to-remote.png)

1. Nell’interfaccia web GitHub, apri una richiesta di pull (PR) per unire il ramo di lavoro al ramo principale dell’archivio della documentazione di Adobe. Assicurati che il ramo su cui hai lavorato sia selezionato e seleziona **Contribute > Apri richiesta di pull**.

   ![Creare una richiesta di pull](./assets/ssd-create-pull-request-1.gif)

1. Assicurati che i rami di base e di confronto siano corretti. Aggiungi una nota alla PR, descrivendo l&#39;aggiornamento, e seleziona **Crea richiesta di pull**. Viene aperto un PR per unire il ramo di lavoro del fork nel ramo principale dell’archivio Adobe.
   >[!TIP]
   >
   >Lascia selezionata la casella di controllo **Consenti modifiche da parte dei manutentori** in modo che il team della documentazione di Adobe possa apportare modifiche alla PR.

   ![Creare una richiesta di pull all’archivio della documentazione di Adobe](./assets/ssd-create-pull-request-2.png)

1. A questo punto, viene visualizzata una notifica che richiede la firma del contratto di licenza da collaboratore (CLA) Adobe. Si tratta di un passaggio obbligatorio. Dopo aver firmato il Contratto di licenza da collaboratore, aggiorna la pagina PR e invia la richiesta di pull.

1. Puoi confermare che la richiesta di pull è stata inviata controllando la scheda **Richieste di pull** in `https://github.com/AdobeDocs/experience-platform.en`.

![PR riuscito](./assets/ssd-pr-successful.png)

1. Grazie. Il team di documentazione di Adobe contatterà la PR nel caso siano necessarie modifiche e per informarti quando verrà pubblicata la documentazione.

>[!TIP]
>
>Per aggiungere immagini e collegamenti alla documentazione e per qualsiasi altra domanda su Markdown, leggi [Utilizzo di Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) nella guida collaborativa alla scrittura di Adobe.
