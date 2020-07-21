---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore Azure Data Explorer
topic: overview
translation-type: tm+mt
source-git-commit: 3b5e76afea5689dbd59f64f6192e6ef2a6acb7d3
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Connettore (Beta) [!DNL Azure Data Explorer]

>[!NOTE]
>Il [!DNL Azure Data Explorer] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../home.md#terms-and-conditions) Origini.

 Adobe Experience Platform fornisce connettività nativa per provider di database come [!DNL Microsoft], MySQL e [!DNL Azure]. È possibile inserire i dati da questi sistemi in [!DNL Platform].

Sono supportati diversi tipi di database di terze parti, tra cui relazionale, NoSQL o date warehouse. Il supporto per i provider di database include [!DNL Azure Data Explorer].

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

La documentazione seguente fornisce informazioni su come connettersi [!DNL Azure Data Explorer] all&#39; [!DNL Platform] utilizzo delle API o dell&#39;interfaccia utente:

## Connessione [!DNL Azure Data Explorer] all&#39; [!DNL Platform] utilizzo delle API

- [Creare un connettore Azure Data Explorer utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/databases/data-explorer.md)
- [Esplora un sistema di database utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/database-nosql.md)
- [Raccolta di dati da un database tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/database-nosql.md)

## Connessione [!DNL Azure Data Explorer] all’ [!DNL Platform] interfaccia utente

- [Creare un connettore di origine Azure Data Explorer nell&#39;interfaccia utente](../../tutorials/ui/create/databases/data-explorer.md)
- [Configurare un flusso di dati per un connettore di database nell&#39;interfaccia utente](../../tutorials/ui/dataflow/databases.md)