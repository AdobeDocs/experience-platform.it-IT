---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;source connectors;sources sdk;sdk;SDK
solution: Experience Platform
title: Utilizzare l’interfaccia web GitHub per creare una pagina della documentazione sulle origini
description: Questo documento descrive come utilizzare l’interfaccia web GitHub per creare la documentazione e inviare una richiesta di pull (PR).
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Utilizza l’interfaccia web GitHub per creare una pagina della documentazione di origine

Questo documento descrive come utilizzare l’interfaccia web GitHub per creare la documentazione e inviare una richiesta di pull (PR).

>[!TIP]
>
>Per supportare ulteriormente il processo di documentazione, puoi utilizzare i seguenti documenti della guida per i collaboratori di Adobe: <ul><li>[Installare gli strumenti di creazione Git e Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[Configurazione locale dell&#39;archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[Flusso di lavoro contributi GitHub per modifiche principali](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## Configurare l’ambiente GitHub

Il primo passaggio nella configurazione dell&#39;ambiente GitHub consiste nel passare all&#39;[archivio GitHub di Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.en).

![repository-piattaforma](../assets/platform-repo.png)

Quindi, seleziona **Fork**.

![fork](../assets/fork.png)

Una volta completato il fork, seleziona **master** e immetti un nome per il nuovo ramo nel menu a discesa visualizzato. Assicurati di fornire un nome descrittivo per il ramo, in quanto verrà utilizzato per contenere il lavoro, quindi seleziona **crea ramo**.

![create-branch](../assets/create-branch.png)

Nella struttura di cartelle GitHub dell&#39;archivio con fork, passa a [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) e seleziona la categoria appropriata per l&#39;origine dall&#39;elenco. Ad esempio, se stai creando la documentazione per una nuova origine CRM, seleziona **crm**.

>[!TIP]
>
>Se stai creando la documentazione per l&#39;interfaccia utente, passa a [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) e seleziona la categoria appropriata per la tua origine. Per aggiungere le immagini, passa a [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) e aggiungi le tue schermate alla cartella `sdk`.

![crm](../assets/crm.png)

Viene visualizzata una cartella delle origini CRM esistenti. Per aggiungere la documentazione per una nuova origine, selezionare **Aggiungi file**, quindi selezionare **Crea nuovo file** dal menu a discesa visualizzato.

![create-new-file](../assets/create-new-file.png)

Denomina il file di origine `YOURSOURCE.md` dove YOURSOURCE è il nome dell&#39;origine in Experience Platform. Ad esempio, se la società è ACME CRM, il nome file deve essere `acme-crm.md`.

![git-interface](../assets/git-interface.png)

## Creare la pagina della documentazione per la sorgente

Per iniziare a documentare la nuova origine, incolla il contenuto del [modello di documentazione origini](./template.md) nell&#39;editor Web GitHub. Puoi scaricare il modello [qui](../assets/api-template.zip).

Con il modello copiato nell’interfaccia dell’editor web GitHub, segui le istruzioni descritte nel modello e modifica i valori contenenti le informazioni rilevanti per la tua origine.

![incolla-modello](../assets/paste-template.png)

Al termine, esegui il commit del file nel ramo.

![commit](../assets/commit.png)

## Inviare la documentazione per la revisione

Una volta eseguito il commit del file, puoi aprire una richiesta di pull (PR) per unire il ramo di lavoro nel ramo principale dell’archivio della documentazione di Adobe. Assicurati che il ramo su cui stai lavorando sia selezionato, quindi seleziona **Confronta e richiedi pull**.

![confronto-pr](../assets/compare-pr.png)

Assicurati che i rami di base e di confronto siano corretti. Aggiungi una nota alla PR, descrivendo l&#39;aggiornamento, quindi seleziona **Crea richiesta di pull**. Verrà aperto un PR per unire il ramo di lavoro nel ramo principale dell’archivio Adobe.

>[!TIP]
>
>Lascia selezionata la casella di controllo **Consenti modifiche da parte dei responsabili della manutenzione** per garantire che il team di documentazione di Adobe possa apportare modifiche alla PR.

![create-pr](../assets/create-pr.png)

A questo punto, viene visualizzata una notifica che richiede di firmare il Contratto di licenza da collaboratore (CLA) di Adobe. Questo è un passaggio obbligatorio. Dopo aver firmato il contratto di licenza, aggiorna la pagina PR e invia la richiesta di pull.

Puoi confermare che la richiesta di pull è stata inviata esaminando la scheda delle richieste di pull in https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
