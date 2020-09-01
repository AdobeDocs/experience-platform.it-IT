---
keywords: Experience Platform;home;popular topics;Microsoft SQL;microsoft sql;SQL;sql
solution: Experience Platform
title: Connettore SQL Server
topic: overview
description: La documentazione seguente fornisce informazioni su come collegare Microsoft SQL Server alla piattaforma utilizzando le API o l'interfaccia utente.
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# (Beta) Connettore [!DNL Microsoft] SQL Server

Adobe Experience Platform consente l&#39;acquisizione di dati da origini esterne, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, database e molti altri.

[!DNL Experience Platform] fornisce il supporto per l&#39;acquisizione di dati da un database di terze parti. [!DNL Platform] può connettersi a diversi tipi di database, ad esempio relazionali, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Microsoft] SQL Server.

## Indirizzo IP  elenco consentiti

I seguenti indirizzi IP devono essere aggiunti a un elenco consentiti  prima di utilizzare i connettori di origine. Se non si aggiungono al elenco consentiti  gli indirizzi IP specifici per la regione, potrebbero verificarsi errori o prestazioni insufficienti quando si utilizzano le origini.

### Regione degli Stati Uniti d&#39;America

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Europa occidentale

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australia Est

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

La documentazione seguente fornisce informazioni su come collegare [!DNL Microsoft] SQL Server all&#39; [!DNL Platform] utilizzo delle API o dell&#39;interfaccia utente:

## Collegare [!DNL Microsoft] SQL Server all&#39; [!DNL Platform] utilizzo delle API

- [Creare un connettore di Microsoft SQL Server utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/databases/sql-server.md)
- [Esplora un sistema di database utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/database-nosql.md)
- [Raccolta di dati da un database tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/database-nosql.md)

## Connessione di [!DNL Microsoft] SQL Server all&#39; [!DNL Platform] interfaccia utente

- [Creare un connettore di origine Microsoft SQL Server nell&#39;interfaccia utente](../../tutorials/ui/create/databases/sql-server.md)
- [Configurare un flusso di dati per un connettore di database nell&#39;interfaccia utente](../../tutorials/ui/dataflow/databases.md)