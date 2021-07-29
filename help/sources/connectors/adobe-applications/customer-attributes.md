---
keywords: Experience Platform;home;argomenti comuni;connettore Attributi del cliente
solution: Experience Platform
title: Panoramica del connettore origine per gli attributi del cliente
topic-legacy: overview
description: Scopri come collegare gli attributi del cliente a Adobe Experience Platform utilizzando le API o l’interfaccia utente
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 541cc87f218a6ef3dcca37573f6d0f9cf560edfb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Connettore Attributi del cliente

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) in Experience Cloud consente di caricare i dati aziendali acquisiti da un database di gestione delle relazioni con i clienti (Customer Relationship Management, CRM). Puoi caricare i dati in un&#39;origine dati Attributi del cliente nell&#39;Experience Cloud, quindi utilizzarli in Adobe Analytics e Adobe Target.

Experience Platform supporta l’acquisizione di dati di profilo [!DNL Customer Attributes] in Adobe Experience Platform.

## Set di dati e schemi

L&#39;origine [!DNL Customer Attributes] crea automaticamente il set di dati in cui inserire i dati. Questo set di dati creato automaticamente è fisso e non può essere selezionato manualmente. L’origine crea inoltre automaticamente lo schema per il set di dati in base all’origine dati di input. Questo processo comporta anche la creazione automatica delle mappature necessarie tra lo schema e i dati di origine.

## Identità

L’identità principale di un set di dati è contenuta nella prima colonna del file CSV dei dati di origine. L&#39;origine [!DNL Customer Attributes] presuppone che l&#39;identità sia sempre mappata allo spazio dei nomi [`CORE`](../../../identity-service/namespaces.md), uno spazio dei nomi generato dal sistema supportato da [[!DNL Identity Service]](../../../identity-service/home.md).

Non è possibile selezionare uno spazio dei nomi esistente per l&#39;identità quando si utilizza l&#39;origine [!DNL Customer Attributes] perché [!DNL Customer Attributes] presuppone che l&#39;identità principale per lo schema sia sempre nella mappa di identità. [!DNL Customer Attributes] crea quindi la mappatura dell&#39;ID sorgente all&#39;UUID della mappa di identità in modo automatico.

Affinché i dati [!DNL Customer Attributes] possano essere collegati ad altri set di dati [!DNL Profile], i relativi dati e identità devono essere in grado di essere associati a un ID Experience Cloud.

Puoi stabilire lo spazio dei nomi `CORE` impostando l&#39;ID Experience Cloud per il visitatore utilizzando [SDK web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [SDK mobile](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity) o l&#39; [API del servizio ID Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

Il file [!DNL Customer Attributes] non compila ulteriormente altre relazioni di identità. Ad esempio, se un set di dati di origine [!DNL Customer Attributes] contiene un campo **E-mail** e un campo **ID fedeltà**, questi campi devono essere etichettati come campi di identità nello schema per essere elaborati in [!DNL Identity Service].

Per ulteriori informazioni, consulta l’esercitazione su [creazione di una connessione sorgente [!DNL Customer Attributes] nell’interfaccia utente](../../tutorials/ui/create/adobe-applications/customer-attributes.md) .
