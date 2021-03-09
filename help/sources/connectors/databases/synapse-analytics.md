---
keywords: Experience Platform;home;argomenti popolari;Azure synapse Analytics;analisi delle azure synapse;Synapse;sinapse
solution: Experience Platform
title: Panoramica del connettore di origine di Azure synapse Analytics
topic: ' - Panoramica'
description: Scopri come collegare Azure synapse Analytics a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# (Beta) Connettore [!DNL Azure Synapse Analytics]

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo utilizzando i servizi [!DNL Platform] . È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[!DNL Experience Platform] fornisce il supporto per l’acquisizione di dati da un database di terze parti. [!DNL Platform] può connettersi a diversi tipi di database, ad esempio relazionale, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Azure Synapse Analytics].

## Elenco indirizzi IP consentiti

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco di indirizzi IP un elenco di indirizzi IP consentiti . Se non aggiungi gli indirizzi IP specifici per l’area geografica all’elenco Consentiti, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [Elenco indirizzi IP consentiti](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Il connettore di origine [!DNL Azure Synapse Analytics] al momento non supporta la connettività della stessa regione a Platform. Ciò significa che, se l’istanza di Azure utilizza la stessa area di rete di Platform, non è possibile stabilire una connessione alle origini di Platform. Al momento, è supportata solo la connettività tra aree geografiche. Per ulteriori informazioni, contatta il tuo Adobe account manager.

La documentazione seguente fornisce informazioni su come connettersi a [!DNL Azure Synapse Analytics] utilizzando le API o l&#39;interfaccia utente:[!DNL Platform]

## Connetti [!DNL Azure Synapse Analytics] a [!DNL Platform] utilizzando le API

- [Creare una connessione sorgente Azure synapse Analytics tramite l’API del servizio di flusso](../../tutorials/api/create/databases/synapse-analytics.md)
- [Esplorare un sistema di database utilizzando l’API del servizio di flusso](../../tutorials/api/explore/database-nosql.md)
- [Raccogliere dati da un database utilizzando l’API del servizio di flusso](../../tutorials/api/collect/database-nosql.md)

## Connetti [!DNL Azure Synapse Analytics] a [!DNL Platform] utilizzando l’interfaccia utente

- [Creare una connessione sorgente Analytics di Azure synapse nell’interfaccia utente](../../tutorials/ui/create/databases/synapse-analytics.md)
- [Configurare un flusso di dati per una connessione al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)