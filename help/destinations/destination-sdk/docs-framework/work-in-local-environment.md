---
title: Utilizza un editor di testo nel tuo ambiente locale per creare una pagina di documentazione di destinazione
description: Le istruzioni riportate in questa pagina mostrano come utilizzare un editor di testo per lavorare nell’ambiente locale per creare una pagina di documentazione per la destinazione dell’Experience Platform e inviarla per la revisione.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# Utilizza un editor di testo nel tuo ambiente locale per creare una pagina di documentazione di destinazione {#local-authoring}

Le istruzioni presenti in questa pagina mostrano come utilizzare un editor di testo per lavorare nel proprio ambiente locale per creare la documentazione e inviare una richiesta di pull (PR). Prima di eseguire i passaggi qui indicati, assicurati di leggere [Documentare la destinazione in Adobe Experience Platform Destinations](./documentation-instructions.md).

>[!TIP]
>
>Consulta anche la documentazione di supporto nella guida per i collaboratori di Adobe:
>* [Installare gli strumenti di creazione Git e Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configurare localmente l’archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Flusso di lavoro dei contributi GitHub per modifiche principali](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Connettersi a GitHub e configurare l’ambiente di authoring locale {#set-up-environment}

1. Nel browser, accedi a `https://github.com/AdobeDocs/experience-platform.en`
2. A [fork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) archivio, fai clic su **Fork** come mostrato di seguito. In questo modo viene creata una copia dell’archivio Experience Platform nel tuo account GitHub.

   ![Archivio della documentazione di Adobe fork](../assets/docs-framework/ssd-fork-repository.gif)

3. Clonare l’archivio sul computer locale. Seleziona **Codice > HTTPS > Apri con GitHub Desktop**, come illustrato di seguito. Assicurati di [Desktop GitHub](https://desktop.github.com/) installato. Per ulteriori riferimenti, leggere [Creare un clone locale dell’archivio](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) nella guida per i collaboratori di Adobe.

   ![Clona l’archivio della documentazione di Adobe in ambiente locale](../assets/docs-framework/clone-local.png)

4. Nella struttura del file locale, passa a `experience-platform.en/help/destinations/catalog/[...]`, dove `[...]` è la categoria desiderata per la destinazione. Ad Experience Platform, se aggiungi una destinazione di personalizzazione, seleziona la `personalization` cartella.

## Creare la pagina della documentazione per la destinazione {#author-documentation}

1. La pagina della documentazione si basa sul [modello di destinazione self-service](../docs-framework/self-service-template.md). Scarica la [modello di destinazione](../assets/docs-framework/yourdestination-template.zip). Decomprimi ed estrai il file `yourdestination-template.md` alla directory indicata al punto 4.  Rinomina il file `YOURDESTINATION.md`, dove YOURDESTINATION è il nome della destinazione in Adobe Experience Platform. Ad esempio, se la tua azienda si chiama Moviestar, dai un nome al tuo file `moviestar.md`.
2. Apri il nuovo file nel [editor di testo selezionato](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). Adobe consiglia di utilizzare [Codice di Visual Studio](https://code.visualstudio.com/) e installa l’estensione Adobe Markdown Authoring . Per installare l&#39;estensione, apri Codice di Visual Studio e seleziona la **[!DNL Extensions]** a sinistra dello schermo e cerca `adobe markdown authoring`. Seleziona l’estensione e fai clic su **[!DNL Install]**.
   ![Installare l’estensione Adobe Markdown Authoring](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Modifica il modello con le informazioni rilevanti per la destinazione. Segui le istruzioni contenute nel modello .
4. Per tutte le schermate o immagini che intendi aggiungere alla documentazione, vai a `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, dove `[...]` è la categoria desiderata per la destinazione. Ad Experience Platform, se aggiungi una destinazione di personalizzazione, seleziona la `personalization` cartella. Crea una nuova cartella per la tua destinazione e salva le immagini qui. Devi effettuare un collegamento a tali elementi dalla pagina che stai creando. Vedi [istruzioni su come collegarsi alle immagini](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. Quando sei pronto, salva il file su cui stai lavorando.

## Invia la documentazione per la revisione {#submit-review}

>[!TIP]
>
>Notate che non c&#39;è niente che potete rompere qui. Seguendo le istruzioni contenute in questa sezione, ti consigliamo semplicemente un aggiornamento della documentazione. L’aggiornamento consigliato verrà approvato o modificato dal team di documentazione di Adobe Experience Platform.

1. In GitHub Desktop, crea un ramo di lavoro per gli aggiornamenti e seleziona **Pubblica ramo** per pubblicare il ramo su GitHub.

![Nuovo ramo locale](../assets/docs-framework/new-branch-local.gif)

1. In GitHub Desktop, [commettere](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) il tuo lavoro, come mostrato di seguito.

   ![Conferma locale](../assets/docs-framework/commit-local.png)

1. In GitHub Desktop, [push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) il tuo lavoro [remoto](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) come illustrato di seguito.

   ![Spingi il tuo commit](../assets/docs-framework/push-local-to-remote.png)

1. Nell’interfaccia web GitHub, apri una richiesta di pull (PR) per unire il ramo di lavoro al ramo principale dell’archivio della documentazione di Adobe. Assicurati che il ramo su cui hai lavorato sia selezionato e seleziona **Contribute > Apri richiesta di pull**.

   ![Creare una richiesta di pull](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Assicurati che i rami di base e di confronto siano corretti. Aggiungi una nota al PR, descrivendo l&#39;aggiornamento e seleziona **Creare una richiesta di pull**. Viene aperto un PR per unire il ramo di lavoro del fork nel ramo principale dell’archivio Adobe.
   >[!TIP]
   >
   >Lascia la **Consenti modifiche da parte dei manutentori** seleziona questa casella di controllo in modo che il team della documentazione di Adobe possa apportare modifiche al PR.

   ![Creare una richiesta di pull all’archivio della documentazione di Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. A questo punto, viene visualizzata una notifica che richiede la firma del contratto di licenza da collaboratore (CLA) Adobe. Si tratta di un passaggio obbligatorio. Dopo aver firmato il Contratto di licenza da collaboratore, aggiorna la pagina PR e invia la richiesta di pull.

1. Puoi confermare che la richiesta di pull è stata inviata controllando il **Richieste di pull** scheda in `https://github.com/AdobeDocs/experience-platform.en`.

![PR riuscito](../assets/docs-framework/ssd-pr-successful.png)

1. Grazie. Il team di documentazione di Adobe contatterà la PR nel caso siano necessarie modifiche e per informarti quando verrà pubblicata la documentazione.

>[!TIP]
>
>Per aggiungere immagini e collegamenti alla tua documentazione e per qualsiasi altra domanda su Markdown, leggi [Utilizzo di Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) nella guida collaborativa alla scrittura in Adobe.
