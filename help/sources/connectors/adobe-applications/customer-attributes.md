---
keywords: Experience Platform;home;argomenti popolari;connettore Attributi del cliente
solution: Experience Platform
title: Panoramica del connettore di origine degli attributi del cliente
description: Scopri come collegare Attributi del cliente a Adobe Experience Platform utilizzando le API o l’interfaccia utente
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 8%

---

# Connettore Attributi del cliente

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html) in Experience Cloud consente di caricare i dati aziendali acquisiti da un database di gestione delle relazioni con i clienti (CRM). Puoi caricare i dati in un’origine dati di attributi cliente in Experience Cloud, quindi utilizzarli in Adobe Analytics e Adobe Target.

Experienci Platform fornisce supporto per l’acquisizione di [!DNL Customer Attributes] dati di profilo in Adobe Experience Platform.

## Set di dati e schemi

Il [!DNL Customer Attributes] origine crea automaticamente il set di dati in cui i dati devono arrivare. Questo set di dati creato automaticamente è fisso e non può essere selezionato manualmente. L’origine crea automaticamente anche lo schema per il set di dati in base all’origine dati di input. Questo processo comporta anche la creazione automatica delle mappature necessarie tra lo schema e i dati di origine.

## Identità

L’identità primaria di un set di dati è contenuta nella prima colonna del file CSV dei dati sorgente. Il [!DNL Customer Attributes] L&#39;origine presuppone che l&#39;identità sia sempre mappata al [`CORE` namespace](../../../identity-service/namespaces.md), spazio dei nomi generato dal sistema e supportato da [[!DNL Identity Service]](../../../identity-service/home.md).

Non è possibile selezionare uno spazio dei nomi esistente per l’identità quando si utilizza [!DNL Customer Attributes] origine perché [!DNL Customer Attributes] presuppone che l’identità primaria dello schema sia sempre nella mappa delle identità. [!DNL Customer Attributes] crea quindi la mappatura dell’ID sorgente all’UUID della mappa di identità in modo automatico.

Per [!DNL Customer Attributes] dati da collegare ad altri [!DNL Profile] i set di dati, i relativi dati e le identità devono poter essere associati a un ID Experience Cloud.

È possibile stabilire `CORE` dello spazio dei nomi impostando l’ID Experience Cloud per il visitatore tramite [SDK per web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html), [SDK per dispositivi mobili](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/)o [API del servizio ID Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it).

Il [!DNL Customer Attributes] Il file non popola ulteriormente altre relazioni di identità. Ad esempio, se un [!DNL Customer Attributes] il set di dati di origine contiene un **E-mail** e un **ID fedeltà** , questi campi devono essere etichettati come campi di identità nello schema per essere elaborati in [!DNL Identity Service].

Guarda il tutorial su [creazione di [!DNL Customer Attributes] connessione sorgente nell’interfaccia utente](../../tutorials/ui/create/adobe-applications/customer-attributes.md) per ulteriori informazioni.
