---
keywords: Experience Platform;home;argomenti popolari;guida per sviluppatori sandbox
solution: Experience Platform
title: Guida alle API sandbox
description: Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 2%

---

# Guida dell’API di [!DNL Sandbox]

L&#39;API [!DNL Sandbox] fornisce diversi endpoint che consentono di gestire in modo programmatico tutte le sandbox disponibili all&#39;interno dell&#39;organizzazione. Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura delle chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [[!DNL Sandbox] riferimento API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Sandbox disponibili

L’endpoint sandbox disponibile consente di visualizzare un elenco di tutte le sandbox disponibili per l’utente corrente, incluse informazioni su nome, titolo, stato, tipo e area della sandbox. L&#39;endpoint sandbox disponibile nell&#39;API [!DNL Sandbox] è accessibile a tutti gli utenti, inclusi quelli senza autorizzazioni di accesso all&#39;amministrazione sandbox. Per informazioni su come visualizzare le sandbox disponibili nell&#39;API, consulta la [guida dell&#39;endpoint &quot;sandboxes&quot;](./available.md).

## Gestione sandbox

Una sandbox è una partizione virtuale all’interno di una singola istanza di Adobe Experience Platform che consente l’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale. È possibile creare, visualizzare, modificare, reimpostare ed eliminare sandbox di produzione e di sviluppo utilizzando l&#39;endpoint `/sandboxes`. Per informazioni su come utilizzare questo endpoint, consulta la [guida dell&#39;endpoint sandboxes](./sandboxes.md).

## Tipi di sandbox

Attualmente, i tipi di sandbox supportati in Experience Platform sono sandbox di produzione e di sviluppo. Una licenza predefinita di Platform consente di ottenere un totale di cinque sandbox, che puoi classificare come produzione o sviluppo. Puoi concedere in licenza pacchetti aggiuntivi di 10 sandbox per un massimo di 75 sandbox in totale. Per informazioni su come visualizzare i tipi di sandbox supportati per la tua organizzazione nell&#39;API, consulta la [guida dell&#39;endpoint &quot;sandbox types&quot;](./types.md).

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Sandbox], leggere la [guida introduttiva](./getting-started.md), quindi selezionare una delle guide degli endpoint per scoprire come utilizzare endpoint specifici.
