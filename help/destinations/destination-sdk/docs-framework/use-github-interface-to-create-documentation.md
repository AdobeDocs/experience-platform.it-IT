---
title: 'Utilizza l’interfaccia web GitHub per creare una pagina di documentazione di destinazione '
description: Le istruzioni presenti in questa pagina mostrano come utilizzare l’interfaccia web GitHub per creare una pagina di documentazione per la destinazione dell’Experience Platform e inviarla per la revisione.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: 83539a9aa2fddcae0c9a44302d8bfa9d9f56de0c
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# Utilizza l’interfaccia web GitHub per creare una pagina di documentazione di destinazione {#github-interface}

Le istruzioni seguenti mostrano come utilizzare l’interfaccia web GitHub per creare la documentazione e inviare una richiesta di pull (PR). Prima di eseguire i passaggi qui indicati, leggi [Documentare la destinazione in Adobe Experience Platform Destinations](./documentation-instructions.md).

>[!TIP]
>
>Consulta anche la documentazione di supporto nella guida per i collaboratori di Adobe:
>* [Installare gli strumenti di creazione Git e Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configurare localmente l’archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Flusso di lavoro dei contributi GitHub per modifiche principali](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Configurare l’ambiente di authoring GitHub {#set-up-environment}

1. Nel browser, passa a `https://github.com/AdobeDocs/experience-platform.en`.
2. Per [fork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) il repository, fai clic su **Fork** come mostrato nell&#39;immagine seguente.

   ![Archivio della documentazione di Adobe fork](./assets/ssd-fork-repository.gif)

3. Nel fork dell’archivio, crea un nuovo ramo per il progetto, come mostrato di seguito. Utilizza questo nuovo ramo per il tuo lavoro.

   ![Creare un nuovo ramo GitHub](./assets/new-branch-github.gif)

4. Nella struttura di cartelle GitHub dell’archivio con fork, passa a `experience-platform.en/help/destinations/catalog/[...]`, dove `[...]` è la categoria desiderata per la destinazione. Ad Experience Platform, se aggiungi una destinazione di personalizzazione, seleziona la categoria `personalization` . Selezionare **Aggiungi file > Crea nuovo file**.

   ![Aggiungi nuovo file](./assets/github-navigate-and-create-file.gif)

5. Denomina la destinazione `YOURDESTINATION.md`, dove YOURDESTINATION è il nome della destinazione in Adobe Experience Platform. Ad esempio, se l’azienda si chiama Moviestar, devi assegnare un nome al file `moviestar.md`.

## Creare la pagina della documentazione per la destinazione {#author-documentation}

1. Il contenuto della pagina di destinazione verrà creato in base al [modello self-service della documentazione](./self-service-template.md). **[](assets/yourdestination-template.zip)** Scarica il modello e decomprimilo per estrarre il modello di  `.md` file.
2. Incolla e modifica il contenuto del modello con le informazioni pertinenti per la destinazione in un editor markdown online, ad esempio [dillinger.io](https://dillinger.io/). Segui le istruzioni riportate nel modello per informazioni dettagliate su cosa devi compilare e quali paragrafi possono essere rimossi.

   >[!TIP]
   >
   >È possibile chiudere la finestra del browser in qualsiasi momento e riaprirla in un secondo momento. Il tuo lavoro viene salvato automaticamente e ti aspetterà quando riapri il browser.
3. Copia il contenuto dall’editor markdown nel nuovo file in GitHub.
4. Per tutte le schermate o immagini che intendi utilizzare, utilizza l’interfaccia GitHub per caricare i file in `experience-platform.en/help/destinations/assets/catalog/[...]`, dove `[...]` è la categoria desiderata per la destinazione. Ad Experience Platform, se aggiungi una destinazione di personalizzazione, seleziona la categoria `personalization` . Devi impostare un collegamento alle immagini dalla pagina che stai creando. Consulta [istruzioni su come collegare immagini](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![Caricare immagini su GitHub](./assets/upload-image.gif)

5. Quando sei pronto, salva il file nel ramo.

![Conferma creazione file](./assets/ssd-confirm-file-creation.png)

## Invia la documentazione per la revisione {#submit-review}

>[!TIP]
>
>Notate che non c&#39;è niente che potete rompere qui. Seguendo le istruzioni contenute in questa sezione, ti consigliamo semplicemente un aggiornamento della documentazione. L’aggiornamento consigliato verrà approvato o modificato dal team di documentazione di Adobe Experience Platform.

1. Dopo aver salvato il file e caricato le immagini desiderate, puoi aprire una richiesta di pull (PR) per unire il ramo di lavoro al ramo principale dell’archivio della documentazione di Adobe. Assicurati che il ramo su cui hai lavorato sia selezionato e seleziona **Contribute > Pull request**.

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
