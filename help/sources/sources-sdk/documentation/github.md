---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
solution: Experience Platform
title: Utilizzare l’interfaccia Web GitHub per creare una pagina di documentazione sulle origini
topic-legacy: tutorial
description: Questo documento fornisce passaggi su come utilizzare l’interfaccia web GitHub per creare la documentazione e inviare una richiesta di pull (PR).
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: adf7dbe5e32310fee680f996ffbde0fd6ddd993a
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 2%

---

# Utilizza l’interfaccia web GitHub per creare una pagina di documentazione sorgente

Questo documento fornisce passaggi su come utilizzare l’interfaccia web GitHub per creare la documentazione e inviare una richiesta di pull (PR).

>[!TIP]
>
>Per supportare ulteriormente il processo di documentazione, puoi utilizzare i seguenti documenti della guida al contributo di Adobe: <ul><li>[Installare gli strumenti di creazione Git e Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[Configurare localmente l’archivio Git per la documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[Flusso di lavoro dei contributi GitHub per modifiche principali](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## Configurare l’ambiente GitHub

Il primo passaggio nella configurazione dell’ambiente GitHub consiste nell’accedere alla [Archivio GitHub Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.en).

![piattaforma-repo](../assets/platform-repo.png)

Quindi, seleziona **Fork**.

![fork](../assets/fork.png)

Una volta completata la forchetta, seleziona **maestro** e inserisci un nome per il nuovo ramo nel menu a discesa visualizzato. Assicurati di fornire un nome descrittivo per il ramo in quanto verrà utilizzato per contenere il lavoro, quindi seleziona **crea ramo**.

![crea-ramo](../assets/create-branch.png)

Nella struttura di cartelle GitHub dell’archivio con fork, passa a [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) quindi selezionare la categoria appropriata per l&#39;origine dall&#39;elenco. Ad esempio, se stai creando documentazione per una nuova origine CRM, seleziona **crm**.

>[!TIP]
>
>Se stai creando la documentazione per l&#39;interfaccia utente, passa a [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) e selezionare la categoria appropriata per l&#39;origine. Per aggiungere le immagini, passa a [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) quindi aggiungi le tue schermate al `sdk` cartella.

![crm](../assets/crm.png)

Viene visualizzata una cartella delle origini CRM esistenti. Per aggiungere documentazione per una nuova sorgente, seleziona **Aggiungi file** quindi seleziona **Crea nuovo file** dal menu a discesa visualizzato.

![create-new-file](../assets/create-new-file.png)

Assegnare un nome al file sorgente `YOURSOURCE.md` dove YOURSOURCE è il nome della sorgente in Platform. Ad esempio, se la tua azienda è ACME CRM, il tuo nome file deve essere `acme-crm.md`.

![git-interface](../assets/git-interface.png)

## Creare la pagina della documentazione della sorgente

Per iniziare a documentare la nuova origine, incolla il contenuto della [modello di documentazione di origini](./template.md) nell’editor web GitHub. Puoi anche scaricare il modello [qui](../assets/api-template.zip).

Con il modello copiato nell’interfaccia dell’editor web GitHub, segui le istruzioni descritte nel modello e modifica i valori contenenti informazioni rilevanti per la tua origine.

![incolla-template](../assets/paste-template.png)

Al termine, esegui il commit del file nel ramo.

![commettere](../assets/commit.png)

## Invia la documentazione per la revisione

Una volta eseguito il commit del file, puoi aprire una richiesta di pull (PR) per unire il ramo di lavoro al ramo principale dell’archivio della documentazione di Adobe. Assicurati che il ramo su cui stai lavorando sia selezionato, quindi seleziona **Confronta e richiedi pull**.

![compare-pr](../assets/compare-pr.png)

Assicurati che i rami di base e di confronto siano corretti. Aggiungi una nota al PR, descrivendo l&#39;aggiornamento, quindi seleziona **Creare una richiesta di pull**. Viene aperto un PR per unire il ramo di lavoro del lavoro nel ramo principale dell’archivio Adobe.

>[!TIP]
>
>Lascia la **Consenti modifiche da parte dei manutentori** seleziona questa casella di controllo per assicurarti che il team della documentazione di Adobe possa apportare modifiche al PR.

![create-pr](../assets/create-pr.png)

A questo punto, viene visualizzata una notifica che richiede la firma del contratto di licenza da collaboratore (CLA) Adobe. Si tratta di un passaggio obbligatorio. Dopo aver firmato il Contratto di licenza da collaboratore, aggiorna la pagina PR e invia la richiesta di pull.

Puoi confermare che la richiesta di pull è stata inviata controllando la scheda delle richieste di pull in https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
