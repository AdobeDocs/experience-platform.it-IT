---
keywords: Experience Platform;home;argomenti comuni;Microsoft SQL;microsoft sql;SQL;sql
solution: Experience Platform
title: Panoramica del connettore di origine SQL Server
topic: ' - Panoramica'
description: Scopri come collegare Microsoft SQL Server a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# (Beta) [!DNL Microsoft] Connettore SQL Server

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo utilizzando i servizi [!DNL Platform] . È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[!DNL Experience Platform] fornisce il supporto per l’acquisizione di dati da un database di terze parti. [!DNL Platform] può connettersi a diversi tipi di database, ad esempio relazionale, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Microsoft] SQL Server.

## Elenco indirizzi IP consentiti

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco di indirizzi IP un elenco di indirizzi IP consentiti . Se non aggiungi gli indirizzi IP specifici per l’area geografica all’elenco Consentiti, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [Elenco indirizzi IP consentiti](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Il [!DNL Microsoft] connettore di origine di SQL Server non supporta attualmente la connettività della stessa regione a Platform. Ciò significa che, se l’istanza di Azure utilizza la stessa area di rete di Platform, non è possibile stabilire una connessione alle origini di Platform. Al momento, è supportata solo la connettività tra aree geografiche. Per ulteriori informazioni, contatta il tuo Adobe account manager.

La documentazione seguente fornisce informazioni su come collegare [!DNL Microsoft] SQL Server a [!DNL Platform] utilizzando le API o l&#39;interfaccia utente:

## Collegare [!DNL Microsoft] SQL Server a [!DNL Platform] utilizzando le API

- [Creare una connessione di origine Microsoft SQL Server utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/databases/sql-server.md)
- [Esplorare un sistema di database utilizzando l’API del servizio di flusso](../../tutorials/api/explore/database-nosql.md)
- [Raccogliere dati da un database utilizzando l’API del servizio di flusso](../../tutorials/api/collect/database-nosql.md)

## Collegare [!DNL Microsoft] SQL Server a [!DNL Platform] utilizzando l&#39;interfaccia utente

- [Creare una connessione di origine Microsoft SQL Server nell&#39;interfaccia utente](../../tutorials/ui/create/databases/sql-server.md)
- [Configurare un flusso di dati per una connessione al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)