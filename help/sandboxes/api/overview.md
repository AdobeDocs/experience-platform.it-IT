---
keywords: Experience Platform;home;argomenti popolari;guida per sviluppatori sandbox
solution: Experience Platform
title: Guida alle API sandbox
description: Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione.
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---

# Guida dell’API di [!DNL Sandbox]

Il [!DNL Sandbox] API fornisce diversi endpoint che ti consentono di gestire in modo programmatico tutte le sandbox disponibili all’interno della tua organizzazione. Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento a [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, leggi le chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visitare il [[!DNL Sandbox] Riferimento API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Sandbox disponibili

L’endpoint sandbox disponibile consente di visualizzare un elenco di tutte le sandbox disponibili per l’utente corrente, incluse informazioni su nome, titolo, stato, tipo e area della sandbox. L’endpoint sandbox disponibile nel [!DNL Sandbox] Tutti gli utenti possono accedere alle API, inclusi quelli senza autorizzazioni di accesso all’amministrazione della sandbox. Consulta la [guida dell’endpoint sandbox disponibile](./available.md) per scoprire come visualizzare le sandbox disponibili nell’API.

## Gestione sandbox

Una sandbox è una partizione virtuale all’interno di una singola istanza di Adobe Experience Platform che consente l’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale. Puoi creare, visualizzare, modificare, reimpostare ed eliminare le sandbox di produzione e di sviluppo utilizzando `/sandboxes` endpoint. Per informazioni su come utilizzare questo endpoint, consulta [guida dell’endpoint &quot;sandboxes&quot;](./sandboxes.md).

## Tipi di sandbox

Attualmente, i tipi di sandbox supportati in Experience Platform sono sandbox di produzione e di sviluppo. Una licenza predefinita di Platform consente di ottenere un totale di cinque sandbox, che puoi classificare come produzione o sviluppo. Puoi concedere in licenza pacchetti aggiuntivi di 10 sandbox per un massimo di 75 sandbox in totale. Consulta la [guida dell’endpoint &quot;sandbox types&quot;](./types.md) per scoprire come visualizzare i tipi di sandbox supportati per la tua organizzazione nell’API.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Sandbox] API, leggi [guida introduttiva](./getting-started.md) quindi seleziona una delle guide degli endpoint per scoprire come utilizzare endpoint specifici.
