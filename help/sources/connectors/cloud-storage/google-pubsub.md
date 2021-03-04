---
keywords: Experience Platform;home;argomenti popolari;Google PubSub;google pubsub
solution: Experience Platform
title: Panoramica del connettore di origine Google PubSub
topic: ' - Panoramica'
description: Scopri come collegare Google PubSub ad Adobe Experience Platform utilizzando le API o l’interfaccia utente.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# (Beta) Connettore [!DNL Google PubSub]

>[!NOTE]
>
>Il connettore [!DNL Google PubSub] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [panoramica sulle sorgenti](../../home.md#terms-and-conditions) .

Adobe Experience Platform fornisce connettività nativa per provider di cloud come [!DNL AWS], [!DNL Google Cloud Platform] e [!DNL Azure], consentendo di inserire i dati da questi sistemi in Platform per l’utilizzo in servizi e destinazioni a valle.

Le origini di archiviazione cloud possono importare i dati in Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni fase del processo viene integrata nel flusso di lavoro delle sorgenti. Platform ti consente di inserire dati da [!DNL Azure Event Hubs] in tempo reale.

## Elenco indirizzi IP consentiti

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco di indirizzi IP un elenco di indirizzi IP consentiti . Se non aggiungi gli indirizzi IP specifici per l’area geografica all’elenco Consentiti, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [Elenco indirizzi IP consentiti](../../ip-address-allow-list.md) .

## Connetti [!DNL Google PubSub] alla piattaforma

La documentazione seguente fornisce informazioni su come connettersi a [!DNL Google PubSub] Platform utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione sorgente Google PubSub utilizzando l’API del servizio di flusso](../../tutorials/api/create/cloud-storage/google-pubsub.md)
- [Raccogliere dati in streaming utilizzando l’API del servizio di flusso](../../tutorials/api/collect/streaming.md)

### Utilizzo dell’interfaccia

- [Creare una connessione sorgente Google PubSub nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
- [Configurare un flusso di dati per una connessione di archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)