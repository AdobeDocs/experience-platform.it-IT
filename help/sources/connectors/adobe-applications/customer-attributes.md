---
keywords: Experience Platform;home;argomenti popolari;connettore Attributi del cliente
solution: Experience Platform
title: Panoramica del connettore Source per attributi cliente
description: Scopri come collegare Attributi del cliente a Adobe Experience Platform utilizzando le API o l’interfaccia utente
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 7%

---

# Connettore Attributi del cliente

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html) in Experience Cloud consente di caricare i dati aziendali acquisiti da un database di gestione delle relazioni con i clienti (CRM). Puoi caricare i dati in un’origine dati di attributi cliente in Experience Cloud, quindi utilizzarli in Adobe Analytics e Adobe Target.

Experience Platform fornisce supporto per l&#39;acquisizione dei dati del profilo [!DNL Customer Attributes] in Adobe Experience Platform.

## Set di dati e schemi

L&#39;origine [!DNL Customer Attributes] crea automaticamente il set di dati in cui inserire i dati. Questo set di dati creato automaticamente è fisso e non può essere selezionato manualmente. L’origine crea automaticamente anche lo schema per il set di dati in base all’origine dati di input. Questo processo comporta anche la creazione automatica delle mappature necessarie tra lo schema e i dati di origine.

## Identità

L’identità primaria di un set di dati è contenuta nella prima colonna del file CSV dei dati sorgente. L&#39;origine [!DNL Customer Attributes] presuppone che l&#39;identità sia sempre mappata allo spazio dei nomi [`CORE`](../../../identity-service/features/namespaces.md), uno spazio dei nomi generato dal sistema e supportato da [[!DNL Identity Service]](../../../identity-service/home.md).

Impossibile selezionare uno spazio dei nomi esistente per l&#39;identità quando si utilizza l&#39;origine [!DNL Customer Attributes] perché [!DNL Customer Attributes] presuppone che l&#39;identità primaria per lo schema sia sempre nella mappa delle identità. [!DNL Customer Attributes] crea quindi la mappatura dell&#39;ID di origine all&#39;UUID della mappa di identità in modo automatico.

Affinché i dati di [!DNL Customer Attributes] possano essere collegati ad altri set di dati di [!DNL Profile], i relativi dati e identità devono poter essere associati a un ID Experience Cloud.

È possibile stabilire lo spazio dei nomi `CORE` impostando l&#39;ID Experience Cloud per il visitatore tramite [Web SDK](/help/web-sdk/identity/overview.md), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/) o l&#39;API del servizio ID Experience Cloud [](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it).

Il file [!DNL Customer Attributes] non popola ulteriormente altre relazioni di identità. Ad esempio, se un set di dati di origine [!DNL Customer Attributes] contiene un campo **E-mail** e un campo **ID fedeltà**, questi campi devono essere etichettati come campi di identità nello schema per essere elaborati in [!DNL Identity Service].

Per ulteriori informazioni, consulta l&#39;esercitazione sulla [creazione di una connessione di origine [!DNL Customer Attributes] nell&#39;interfaccia utente](../../tutorials/ui/create/adobe-applications/customer-attributes.md).
