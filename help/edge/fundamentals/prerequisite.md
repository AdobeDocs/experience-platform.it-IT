---
title: Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK
seo-title: Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK
description: Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK
seo-description: Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: a0ede8c7d3088fe80d6ea014b4a4f9f08ee8a7aa
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK

Per utilizzare questo SDK, devi prima:

- Effettuare il provisioning dell&#39;organizzazione per questa funzione. (Se desideri essere inserito nella lista d&#39;attesa, contatta il tuo software manager certificato (CSM).
- Accertati che sia attivato un dominio di prime parti (CNAME). Se hai già un CNAME per  Adobe Analytics, devi usarlo. Il test in fase di sviluppo funziona senza un CNAME, ma ne hai bisogno prima di andare in produzione.

>[!IMPORTANT]
>
>**A partire dal 20/11/10, le implementazioni CNAME di prime parti avranno una scadenza di 7 giorni su tutti i browser Safari e i dispositivi iOS mobili.**

- Avere diritto ad Adobe Experience Platform. Se non hai acquistato Adobe Experience Platform,  Adobe ti fornirà  Data Services Foundation da utilizzare in modo limitato con l&#39;SDK senza costi aggiuntivi.
- Se il sito Web utilizza già il servizio [ID Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) sul sito Web, tramite l’API del visitatore o l’estensione  del servizio ID Experience Cloud in  Adobe Experience Platform Launch, e desiderate continuare a usarlo durante la migrazione all’SDK Web di Adobe Experience Platform, dovete utilizzare la versione più recente dell’API del visitatore o l’estensione  del servizio ID Experience Cloud. Per ulteriori informazioni, consulta Migrazione [degli](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) ID.
