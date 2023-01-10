---
keywords: Experience Platform;home;argomenti comuni;connettore Attributi del cliente
solution: Experience Platform
title: Panoramica del connettore origine per gli attributi del cliente
description: Scopri come collegare gli attributi del cliente a Adobe Experience Platform utilizzando le API o l’interfaccia utente
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 8%

---

# Connettore Attributi del cliente

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) in Experience Cloud consente di caricare i dati aziendali acquisiti da un database di gestione delle relazioni con i clienti (Customer Relationship Management, CRM). Puoi caricare i dati in un’origine dati di attributi cliente in Experience Cloud, quindi utilizzarli in Adobe Analytics e Adobe Target.

Experience Platform fornisce il supporto per l’acquisizione [!DNL Customer Attributes] dati di profilo in Adobe Experience Platform.

## Set di dati e schemi

La [!DNL Customer Attributes] source crea automaticamente il set di dati in cui inserire i dati. Questo set di dati creato automaticamente è fisso e non può essere selezionato manualmente. L’origine crea inoltre automaticamente lo schema per il set di dati in base all’origine dati di input. Questo processo comporta anche la creazione automatica delle mappature necessarie tra lo schema e i dati di origine.

## Identità

L’identità principale di un set di dati è contenuta nella prima colonna del file CSV dei dati di origine. La [!DNL Customer Attributes] l&#39;origine presuppone che l&#39;identità sia sempre mappata al [`CORE` namespace](../../../identity-service/namespaces.md), uno spazio dei nomi generato dal sistema supportato da [[!DNL Identity Service]](../../../identity-service/home.md).

Non è possibile selezionare uno spazio dei nomi esistente per l&#39;identità quando si utilizza [!DNL Customer Attributes] sorgente perché [!DNL Customer Attributes] presuppone che l&#39;identità principale per lo schema sia sempre nella mappa di identità. [!DNL Customer Attributes] crea quindi la mappatura dell&#39;ID sorgente all&#39;UUID della mappa di identità in modo automatico.

Per [!DNL Customer Attributes] dati da collegare ad altri [!DNL Profile] i set di dati, i relativi dati e identità devono essere in grado di corrispondere a un ID Experience Cloud.

È possibile stabilire `CORE` namespace impostando l’ID Experience Cloud per il visitatore utilizzando [SDK per web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [SDK per dispositivi mobili](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)o [API del servizio ID di Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it).

La [!DNL Customer Attributes] il file non compila ulteriormente altre relazioni di identità. Ad esempio, se un [!DNL Customer Attributes] il set di dati di origine contiene **E-mail** e **ID fedeltà** tali campi devono essere etichettati come campi di identità nello schema per essere elaborati in [!DNL Identity Service].

Guarda l’esercitazione su [creazione di un [!DNL Customer Attributes] connessione sorgente nell’interfaccia utente](../../tutorials/ui/create/adobe-applications/customer-attributes.md) per ulteriori informazioni.
