---
title: Utilizza l’interfaccia web GitHub per creare una pagina della documentazione di destinazione
description: Le istruzioni in questa pagina mostrano come utilizzare l’interfaccia web GitHub per creare una pagina di documentazione per la destinazione dell’Experience Platform e inviarla per la revisione.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Utilizza l’interfaccia web GitHub per creare una pagina della documentazione di destinazione {#github-interface}

Le istruzioni seguenti mostrano come utilizzare l’interfaccia web GitHub per creare la documentazione e inviare una richiesta di pull (PR). Prima di eseguire i passaggi qui indicati, assicurati di aver letto [Documento la tua destinazione in Destinazioni Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Consulta anche la documentazione di supporto nella guida per i collaboratori di Adobe:
>* [Installare gli strumenti di creazione Git e Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=it)
>* [Configurazione locale dell&#39;archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=it)
>* [Flusso di lavoro dei contributi GitHub per modifiche principali](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=it).

## Configurare l’ambiente di authoring GitHub {#set-up-environment}

1. Nel browser, passa a `https://github.com/AdobeDocs/experience-platform.en`.
2. Per [eseguire il fork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=it#fork-the-repository) dell&#39;archivio, fare clic su **Effettuare il fork** come illustrato di seguito. In questo modo viene creata una copia dell’archivio di Experienci Platform nel tuo account GitHub.

   ![Archivio della documentazione di Fork Adobe](../assets/docs-framework/ssd-fork-repository.gif)

3. Nel fork dell’archivio, crea un nuovo ramo per il progetto, come illustrato di seguito. Utilizza questo nuovo ramo per il tuo lavoro.

   ![Crea nuovo ramo GitHub](../assets/docs-framework/new-branch-github.gif)

4. Nella struttura di cartelle GitHub dell&#39;archivio con fork, passa a `experience-platform.en/help/destinations/catalog/[...]`, dove `[...]` è la categoria desiderata per la destinazione. Se ad Experience Platform si aggiunge una destinazione di personalizzazione, selezionare la categoria `personalization`. Selezionare **Aggiungi file > Crea nuovo file**.

   ![Aggiungi nuovo file](../assets/docs-framework/github-navigate-and-create-file.gif)

5. Assegna un nome alla destinazione `YOURDESTINATION.md`, dove YOURDESTINATION è il nome della destinazione in Adobe Experience Platform. Se ad esempio la società si chiama Moviestar, il file verrà denominato `moviestar.md`.

## Creare la pagina della documentazione per la destinazione {#author-documentation}

1. Verrà creato il contenuto della pagina di destinazione in base al [modello self-service della documentazione](./self-service-template.md). **[Scarica](../assets/docs-framework/yourdestination-template.zip)** il modello e decomprimi per estrarre il modello di file `.md`.
2. Incolla e modifica il contenuto del modello con le informazioni rilevanti per la destinazione in un editor markdown online, ad esempio [dillinger.io](https://dillinger.io/). Seguire le istruzioni nel modello per i dettagli su cosa compilare e quali paragrafi possono essere rimossi.

   >[!TIP]
   >
   >Puoi chiudere la finestra del browser in qualsiasi momento e riaprirla in un secondo momento. Il tuo lavoro viene salvato automaticamente e ti aspetta quando riapri il browser.
3. Copia il contenuto dall’editor markdown nel nuovo file in GitHub.
4. Per qualsiasi schermata o immagine che intendi utilizzare, utilizza l&#39;interfaccia GitHub per caricare i file in `experience-platform.en/help/destinations/assets/catalog/[...]`, dove `[...]` è la categoria desiderata per la tua destinazione. Se ad Experience Platform si aggiunge una destinazione di personalizzazione, selezionare la categoria `personalization`. Devi collegare alle immagini dalla pagina che stai creando. Consulta [istruzioni su come collegare le immagini](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=it#link-to-images).

   ![Carica immagine in GitHub](../assets/docs-framework/upload-image.gif)

5. Quando sei pronto, salva il file nel ramo.

![Conferma creazione file](../assets/docs-framework/ssd-confirm-file-creation.png)

## Inviare la documentazione per la revisione {#submit-review}

>[!TIP]
>
>Tieni presente che qui non è possibile interrompere nulla. Attenendoti alle istruzioni riportate in questa sezione, ti basta suggerire un aggiornamento della documentazione. L’aggiornamento suggerito verrà approvato o modificato dal team di documentazione di Adobe Experience Platform.

1. Dopo aver salvato il file e caricato le immagini desiderate, puoi aprire una richiesta di pull (PR) per unire il ramo di lavoro nel ramo principale dell’archivio della documentazione di Adobe. Assicurati che il ramo su cui hai lavorato sia selezionato e seleziona **Contribute > Apri richiesta di pull**.

![Crea richiesta di pull](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Assicurati che i rami di base e di confronto siano corretti. Aggiungi una nota alla PR con la descrizione dell&#39;aggiornamento e seleziona **Crea richiesta di pull**. Viene aperto un PR per unire il ramo di lavoro del fork nel ramo principale dell’archivio di Adobi.

   >[!TIP]
   >
   >Lascia selezionata la casella di controllo **Consenti modifiche da parte dei gestori** in modo che il team della documentazione di Adobe possa apportare modifiche all&#39;PR.

   ![Crea una richiesta di pull nell&#39;archivio della documentazione Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. A questo punto, viene visualizzata una notifica che richiede di firmare il Contratto di licenza da collaboratore (CLA) di Adobe. Questo è un passaggio obbligatorio. Dopo aver firmato il contratto di licenza, aggiorna la pagina PR e invia la richiesta di pull.

1. Puoi confermare che la richiesta di pull è stata inviata esaminando la scheda **Richieste pull** in `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR completato](../assets/docs-framework/ssd-pr-successful.png)

1. Grazie. Il team di documentazione di Adobe si rivolgerà al PR nel caso siano necessarie modifiche e ti informerà di quando la documentazione verrà pubblicata.

>[!TIP]
>
>Per aggiungere immagini e collegamenti alla documentazione e per eventuali altre domande su Markdown, leggi [Utilizzo di Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=it) nella guida alla scrittura collaborativa di Adobe.
