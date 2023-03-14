---
title: Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK
description: Scopri i prerequisiti per utilizzare Adobe Experience Platform Web SDK.
keywords: dominio di prima parte;CNAME;schema;creare schema;lanciare;estensione web sdk;estensione;ID configurazione;strumento di configurazione;elemento dati;creare elemento dati;oggetto XDM;sendEvent;send Event;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 6a9882224cba08718c81a3aead237107b3e47726
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK

Per utilizzare Adobe Experience Platform Web SDK, devi prima:

- Disporre delle autorizzazioni appropriate per gli utenti dell’organizzazione. Tutti i clienti Experience Cloud hanno accesso agli strumenti di raccolta dati; ogni utente dell’organizzazione avrà solo bisogno di autorizzazioni per schemi, identità e flussi di dati. Per ulteriori informazioni su come impostare queste autorizzazioni, consulta la documentazione su [gestione autorizzazioni raccolta dati](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
- Si consiglia di abilitare il dominio di prima parte (CNAME). Se disponi già di un CNAME per Adobe Analytics, utilizza quello. Il test nello sviluppo funziona senza un CNAME, ma l’Adobe consiglia di averne uno prima di passare alla produzione. Anche se un’implementazione CNAME non offre vantaggi in termini di durata dei cookie, può impedire ad alcuni ad blocker e browser meno comuni di bloccare le richieste SDK. In questi casi, l’utilizzo di un CNAME potrebbe impedire l’interruzione della raccolta dati per gli utenti che utilizzano questi strumenti.

>[!IMPORTANT]
>
>**A partire dal 11/10/20, le implementazioni CNAME di prime parti scadranno dopo 7 giorni su tutti i browser Safari e i dispositivi mobili iOS.**

- Se il tuo sito web utilizza già [Servizio ID Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) sul sito web, tramite API Visitor o l’estensione del servizio ID Experience Cloud in Adobe Experience Platform Launch, e desideri continuare a utilizzarla durante la migrazione a Adobe Experience Platform Web SDK, devi utilizzare la versione più recente di API Visitor o l’estensione del servizio ID Experience Cloud. Consulta [Migrazione degli ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) per ulteriori informazioni.
