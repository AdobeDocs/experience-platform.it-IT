---
title: Prerequisiti per l’utilizzo dell’SDK per web di Adobe Experience Platform
description: Scopri i prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK.
keywords: dominio di prima parte;CNAME;schema;crea schema;launch;estensione sdk web aep;estensione;id di configurazione;strumento di configurazione;elemento dati;crea elemento dati;oggetto XDM;sendEvent;send Event;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 072e1968fa152454f4df6e88fcf7de5c03494030
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 2%

---

# Prerequisiti per l’utilizzo dell’SDK per web di Adobe Experience Platform

Per utilizzare l&#39;SDK per web Adobe Experience Platform, devi prima:

- Effettua il provisioning della tua organizzazione per questa funzione. Se desideri accedere, compila quanto segue [modulo](http://adobe.ly/websdkaccess) e Adobe ti fornirà l’accesso a Datatstreams e Adobe Experience Platform (se necessario). Tieni presente che Adobe ti fornirà l’accesso necessario per l’utilizzo limitato con l’SDK senza costi aggiuntivi.
- Si consiglia di abilitare il dominio di prima parte (CNAME). Se disponi già di un CNAME per Adobe Analytics, utilizza questo. Il test nello sviluppo funziona senza un CNAME, ma Adobe consiglia di averne uno prima di passare alla produzione. Sebbene un’implementazione CNAME non fornisca alcun vantaggio in termini di durata dei cookie, può impedire ad alcuni ad blocker e browser meno comuni di bloccare le richieste SDK. In questi casi, l’utilizzo di un CNAME potrebbe impedire l’interruzione della raccolta dati da parte degli utenti che utilizzano questi strumenti.

>[!IMPORTANT]
>
>**A partire dal 10/11/20, le implementazioni CNAME di prima parte hanno una scadenza di 7 giorni su tutti i browser Safari e i dispositivi mobili iOS.**

- Se il sito web utilizza già [Servizio Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) sul tuo sito web, tramite API visitatore o l’estensione del servizio Experience Cloud ID all’interno di Adobe Experience Platform Launch, e desideri continuare a utilizzarlo durante la migrazione all’SDK web di Adobe Experience Platform, devi utilizzare la versione più recente dell’API visitatore o l’estensione del servizio Experience Cloud ID. Vedi [Migrazione degli ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) per ulteriori informazioni.

## Gestione delle autorizzazioni per Adobe Experience Platform Web SDK

Per iniziare a utilizzare Adobe Experience Platform, devi disporre del diritto [permissions](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=it) per creare gli schemi e gestire le identità. Le autorizzazioni minime necessarie si trovano nella categoria Modellazione dati e identità .

![](../images/AEP-permission-categories.png)

All’interno della categoria Modellazione dati, concedere agli utenti le autorizzazioni Gestisci schemi e Visualizza schemi.

![](../images/data-modeling-permissions.png)

All’interno della categoria Identity Management, assegna agli utenti le autorizzazioni Gestisci spazi dei nomi identità e Visualizza spazi dei nomi identità .

![](../images/identity-management-permissions.png)
