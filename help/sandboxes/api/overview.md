---
keywords: Experience Platform;home;argomenti popolari;guida per gli sviluppatori sandbox
solution: Experience Platform
title: Guida all’API per sandbox
description: Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione.
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Guida dell’API di [!DNL Sandbox]

La [!DNL Sandbox] API fornisce diversi endpoint che consentono di gestire in modo programmatico tutte le sandbox disponibili all’interno dell’organizzazione IMS. Questi endpoint sono descritti di seguito. Per informazioni dettagliate, visita le singole guide dell’endpoint e fai riferimento alla sezione [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [[!DNL Sandbox] Riferimento API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Sandbox disponibili

L’endpoint sandbox disponibile consente di visualizzare un elenco di tutte le sandbox disponibili per l’utente corrente, incluse informazioni sul nome, il titolo, lo stato, il tipo e la regione di ciascuna sandbox. L’endpoint sandbox disponibile nel [!DNL Sandbox] L’API è accessibile a tutti gli utenti, inclusi quelli senza autorizzazioni di accesso di amministrazione sandbox. Consulta la sezione [guida all’endpoint sandbox disponibile](./available.md) per scoprire come visualizzare le sandbox disponibili nell’API.

## Gestione sandbox

Una sandbox è una partizione virtuale all’interno di una singola istanza di Adobe Experience Platform, che consente un’integrazione diretta con il processo di sviluppo delle applicazioni di esperienza digitale. Puoi creare, visualizzare, modificare, ripristinare ed eliminare le sandbox di produzione e sviluppo utilizzando `/sandboxes` punto finale. Per informazioni su come utilizzare questo endpoint, consulta la sezione [guida all’endpoint sandbox](./sandboxes.md).

## Tipi di sandbox

Attualmente, i tipi di sandbox supportati su Experience Platform sono sandbox di produzione e sviluppo. Una licenza Platform predefinita ti consente di ottenere un totale di cinque sandbox, classificabili come produzione o sviluppo. È possibile concedere in licenza pacchetti aggiuntivi di 10 sandbox fino a un massimo di 75 sandbox in totale. Consulta la sezione [guida all’endpoint per i tipi di sandbox](./types.md) per scoprire come visualizzare i tipi di sandbox supportati per la tua organizzazione nell’API.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Sandbox] API, leggi [guida introduttiva](./getting-started.md) quindi seleziona una delle guide dell’endpoint per scoprire come utilizzare endpoint specifici.
