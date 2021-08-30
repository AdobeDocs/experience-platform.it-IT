---
keywords: Experience Platform;home;argomenti popolari;guida per gli sviluppatori sandbox
solution: Experience Platform
title: Guida all’API per sandbox
topic-legacy: developer guide
description: Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione.
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Guida dell’API di [!DNL Sandbox]

L’ API [!DNL Sandbox] fornisce diversi endpoint che ti consentono di gestire in modo programmatico tutte le sandbox disponibili all’interno dell’organizzazione IMS. Questi endpoint sono descritti di seguito. Per informazioni dettagliate, visita le singole guide dell&#39;endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [[!DNL Sandbox] riferimento API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Sandbox disponibili

L’endpoint sandbox disponibile consente di visualizzare un elenco di tutte le sandbox disponibili per l’utente corrente, incluse informazioni sul nome, il titolo, lo stato, il tipo e la regione di ciascuna sandbox. L’endpoint sandbox disponibile nell’ API [!DNL Sandbox] è accessibile a tutti gli utenti, inclusi quelli senza le autorizzazioni di accesso di amministrazione sandbox. Per informazioni su come visualizzare le sandbox disponibili nell’API, consulta la [guida all’endpoint sandbox disponibile](./available.md) .

## Gestione sandbox

Una sandbox è una partizione virtuale all’interno di una singola istanza di Adobe Experience Platform, che consente un’integrazione diretta con il processo di sviluppo delle applicazioni di esperienza digitale. Puoi creare, visualizzare, modificare, ripristinare ed eliminare le sandbox di produzione e sviluppo utilizzando l’endpoint `/sandboxes` . Per informazioni su come utilizzare questo endpoint, consulta la [guida all’endpoint sandbox](./sandboxes.md).

## Tipi di sandbox

Attualmente, i tipi di sandbox supportati su Experience Platform sono sandbox di produzione e sviluppo. Una licenza Platform predefinita ti consente di ottenere un totale di cinque sandbox, classificabili come produzione o sviluppo. È possibile concedere in licenza pacchetti aggiuntivi di 10 sandbox fino a un massimo di 75 sandbox in totale. Per informazioni su come visualizzare i tipi di sandbox supportati per la tua organizzazione nell’API, consulta la [guida all’endpoint per i tipi di sandbox](./types.md) .

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Sandbox], leggi la [guida introduttiva](./getting-started.md) , quindi seleziona una delle guide dell&#39;endpoint per scoprire come utilizzare endpoint specifici.