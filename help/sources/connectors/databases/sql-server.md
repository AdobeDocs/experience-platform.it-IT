---
keywords: Experience Platform;home;argomenti comuni;Microsoft SQL;microsoft sql;SQL;sql
solution: Experience Platform
title: Panoramica del connettore di origine SQL Server
topic-legacy: overview
description: Scopri come collegare Microsoft SQL Server a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 8a77f108-7e82-4e14-a470-a4ea97def89d
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# [!DNL Microsoft] Connettore SQL Server

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo utilizzando i servizi [!DNL Platform] . È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[!DNL Experience Platform] fornisce il supporto per l’acquisizione di dati da un database di terze parti. [!DNL Platform] può connettersi a diversi tipi di database, ad esempio relazionale, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Microsoft] SQL Server.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Il [!DNL Microsoft] connettore di origine di SQL Server non supporta attualmente la connettività della stessa regione a Platform. Ciò significa che, se l’istanza di Azure utilizza la stessa area di rete di Platform, non è possibile stabilire una connessione alle origini di Platform. Al momento, è supportata solo la connettività tra aree geografiche. Per ulteriori informazioni, contatta il tuo Adobe account manager.

La documentazione seguente fornisce informazioni su come collegare [!DNL Microsoft] SQL Server a [!DNL Platform] utilizzando le API o l&#39;interfaccia utente:

## Collegare [!DNL Microsoft] SQL Server a [!DNL Platform] utilizzando le API

- [Creare una connessione di base di Microsoft SQL Server utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/databases/sql-server.md)
- [Esplorare la struttura dati e il contenuto di un’origine di database utilizzando l’API del servizio di flusso](../../tutorials/api/explore/database-nosql.md)
- [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio di flusso](../../tutorials/api/collect/database-nosql.md)

## Collegare [!DNL Microsoft] SQL Server a [!DNL Platform] utilizzando l&#39;interfaccia utente

- [Creare una connessione di origine Microsoft SQL Server nell&#39;interfaccia utente](../../tutorials/ui/create/databases/sql-server.md)
- [Creazione di un flusso di dati per una connessione sorgente del database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
