---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Apache Hive sul connettore Azure HDInsights
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# (Beta) [!DNL Apache Hive] su [!DNL Azure HDInsights] connettore

>[!NOTE]
>
>L&#39;Apache Hive sul connettore Azure HDInsights è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../home.md#terms-and-conditions) Origini.

Adobe Experience Platform consente l&#39;acquisizione di dati da origini esterne, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, database e molti altri.

[!DNL Experience Platform] fornisce il supporto per l&#39;acquisizione di dati da un database di terze parti. [!DNL Platform] può connettersi a diversi tipi di database, ad esempio relazionali, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Apache Hive] on [!DNL Azure HDInsights].

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

La documentazione seguente fornisce informazioni su come connettersi [!DNL Apache Hive] a [!DNL Azure HDInsights] mediante l&#39; [!DNL Platform] utilizzo delle API o dell&#39;interfaccia utente:

## Connettersi [!DNL Apache Hive] in [!DNL Azure HDInsights] modo da [!DNL Platform] utilizzare le API

- [Creare un Hive Apache sul connettore Azure HDInsights utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/databases/hive.md)
- [Esplora un sistema di database utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/database-nosql.md)
- [Raccolta di dati da un database tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/database-nosql.md)

## Connessione [!DNL Apache Hive] all’ [!DNL Azure HDInsights] interfaccia [!DNL Platform] utente

- [Creare un Apache Hive sul connettore di origine Azure HDInsights nell&#39;interfaccia utente](../../tutorials/ui/create/databases/hive.md)
- [Configurare un flusso di dati per un connettore di database nell&#39;interfaccia utente](../../tutorials/ui/dataflow/databases.md)