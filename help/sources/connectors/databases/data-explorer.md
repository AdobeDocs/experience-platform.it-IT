---
keywords: Experience Platform;home;argomenti popolari;Azure Data Explorer;azure data explorer
solution: Experience Platform
title: Panoramica del connettore di origine di Azure Data Explorer
topic: ' - Panoramica'
description: Scopri come collegare Azure Data Explorer a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# (Beta) Connettore [!DNL Azure Data Explorer]

>[!NOTE]
>
>Il connettore [!DNL Azure Data Explorer] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../home.md#terms-and-conditions) .

Adobe Experience Platform fornisce connettività nativa per provider di database come [!DNL Microsoft], MySQL e [!DNL Azure]. Puoi inserire i tuoi dati da questi sistemi in [!DNL Platform].

Sono supportati diversi tipi di database di terze parti, tra cui relazionale, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Azure Data Explorer].

## Elenco indirizzi IP consentiti

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco di indirizzi IP un elenco di indirizzi IP consentiti . Se non aggiungi gli indirizzi IP specifici per l’area geografica all’elenco Consentiti, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [Elenco indirizzi IP consentiti](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Il connettore di origine [!DNL Azure Data Explorer] al momento non supporta la connettività della stessa regione a Platform. Ciò significa che, se l’istanza di Azure utilizza la stessa area di rete di Platform, non è possibile stabilire una connessione alle origini di Platform. Al momento, è supportata solo la connettività tra aree geografiche. Per ulteriori informazioni, contatta il tuo Adobe account manager.

La documentazione seguente fornisce informazioni su come connettersi a [!DNL Azure Data Explorer] utilizzando le API o l&#39;interfaccia utente:[!DNL Platform]

## Connetti [!DNL Azure Data Explorer] a [!DNL Platform] utilizzando le API

- [Creare una connessione sorgente di Data Explorer di Azure utilizzando l’API del servizio di flusso](../../tutorials/api/create/databases/data-explorer.md)
- [Esplorare un sistema di database utilizzando l’API del servizio di flusso](../../tutorials/api/explore/database-nosql.md)
- [Raccogliere dati da un database utilizzando l’API del servizio di flusso](../../tutorials/api/collect/database-nosql.md)

## Connetti [!DNL Azure Data Explorer] a [!DNL Platform] utilizzando l’interfaccia utente

- [Creare una connessione sorgente di Data Explorer Azure nell’interfaccia utente](../../tutorials/ui/create/databases/data-explorer.md)
- [Configurare un flusso di dati per una connessione al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)