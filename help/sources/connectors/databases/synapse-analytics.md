---
keywords: Experience Platform;home;argomenti popolari;Azure synapse Analytics;analisi delle azure synapse;Synapse;sinapse
solution: Experience Platform
title: Panoramica del connettore di origine di Azure synapse Analytics
topic-legacy: overview
description: Scopri come collegare Azure synapse Analytics a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# [!DNL Azure Synapse Analytics] connettore

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo utilizzando i servizi [!DNL Platform] . È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[!DNL Experience Platform] fornisce il supporto per l’acquisizione di dati da un database di terze parti. [!DNL Platform] può connettersi a diversi tipi di database, ad esempio relazionale, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Azure Synapse Analytics].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md) .

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
