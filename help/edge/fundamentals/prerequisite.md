---
title: Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK
seo-title: Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK
description: Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK
seo-description: Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK
keywords: dominio di prime parti;CNAME;schema;creare schema;avvio;estensione di sdk web aep;extension;configuration id;tool di configurazione;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: a19b4384e2ea64eb9ab5f0f5443fd329ec44a2a0
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# Prerequisiti per l’utilizzo di Adobe Experience Platform Web SDK

Per utilizzare l&#39;SDK Web per la piattaforma, devi prima:

- Il provisioning dell&#39;organizzazione per questa funzione. (L&#39;accesso all&#39;SDK Web della piattaforma è gratuito, se desiderate accedere contattate il vostro Customer Success Manager (CSM).
- Accertati che sia attivato un dominio di prime parti (CNAME). Se hai già un CNAME per  Adobe Analytics, devi usarlo. Il test in fase di sviluppo funziona senza un CNAME, ma ne hai bisogno prima di andare in produzione.

>[!IMPORTANT]
>
>**A partire dal 20/11/10, le implementazioni CNAME di prime parti avranno una scadenza di 7 giorni su tutti i browser Safari e i dispositivi iOS mobili.**

- Avere diritto ad Adobe Experience Platform. Se non avete acquistato Adobe Experience Platform,  Adobe vi fornirà l’accesso necessario per l’utilizzo limitato con l’SDK senza costi aggiuntivi.
- Se il sito Web utilizza già il [ servizio ID Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) sul sito Web, tramite l&#39;API del visitatore o l&#39;estensione  servizio ID Experience Cloud in  Adobe Experience Platform Launch, e desiderate continuare a usarlo durante la migrazione all&#39;SDK Web di Adobe Experience Platform, dovete utilizzare la versione più recente dell&#39;API del visitatore o l&#39;estensione  servizio ID Experience Cloud. Per ulteriori informazioni, vedi [Migrazione ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity).
