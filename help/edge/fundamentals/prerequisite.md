---
title: Prerequisiti per l’utilizzo dell’SDK per web di Adobe Experience Platform
description: Scopri i prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK.
keywords: dominio di prima parte;CNAME;schema;crea schema;launch;estensione sdk web aep;estensione;id di configurazione;strumento di configurazione;elemento dati;crea elemento dati;oggetto XDM;sendEvent;send Event;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 5f3b82edbc52d96cad13932be1d201e275780f3c
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Prerequisiti per l’utilizzo dell’SDK per web di Adobe Experience Platform

Per utilizzare l’SDK per web di Platform, devi prima:

- Effettua il provisioning della tua organizzazione per questa funzione. L’accesso all’SDK web per Platform è gratuito. Per accedere, contatta il tuo Customer Success Manager (CSM).
- Si consiglia di abilitare il dominio di prima parte (CNAME). Se disponi già di un CNAME per Adobe Analytics, utilizza questo. Il test nello sviluppo funziona senza un CNAME, ma Adobe consiglia di averne uno prima di passare alla produzione. Sebbene un’implementazione CNAME non fornisca alcun vantaggio in termini di durata dei cookie, può impedire ad alcuni ad blocker e browser meno comuni di bloccare le richieste SDK. In questi casi, l’utilizzo di un CNAME potrebbe impedire l’interruzione della raccolta dati da parte degli utenti che utilizzano questi strumenti.

>[!IMPORTANT]
>
>**A partire dal 10/11/20, le implementazioni CNAME di prima parte hanno una scadenza di 7 giorni su tutti i browser Safari e i dispositivi iOS mobili.**

- Avere diritto a Adobe Experience Platform. Se non hai acquistato Adobe Experience Platform, Adobe ti fornirà l’accesso necessario da utilizzare in modo limitato con l’SDK senza alcun costo aggiuntivo.
- Se il tuo sito web utilizza già il [servizio ID Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) sul tuo sito web, tramite l&#39;API visitatore o l&#39;estensione del servizio ID Experience Cloud all&#39;interno di Adobe Experience Platform Launch, e desideri continuare a usarlo durante la migrazione all&#39;SDK per web di Adobe Experience Platform, devi utilizzare la versione più recente dell&#39;API visitatore o l&#39;estensione del servizio ID di Experience Cloud. Per ulteriori informazioni, consulta [Migrazione ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) .
