---
keywords: Experience Platform;home;argomenti popolari;archiviazione tabella di Azure;archiviazione tabella di Azure;ATS;ats
solution: Experience Platform
title: Panoramica del connettore origine di archiviazione tabella di Azure
topic-legacy: overview
description: Scopri come collegare Azure Table Storage a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
source-git-commit: 7af79b9e0d6ed29b796ac7c98b4df1dda09f3513
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# [!DNL Azure Table Storage] connettore

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

Experience Platform supporta l’acquisizione di dati da un database di terze parti. Platform può connettersi a diversi tipi di database, ad esempio relazionale, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Azure Table Storage].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Il connettore di origine [!DNL Azure Table Storage] al momento non supporta la connettività della stessa regione a Platform. Ciò significa che, se l’istanza di Azure utilizza la stessa area di rete di Platform, non è possibile stabilire una connessione alle origini di Platform. Al momento, è supportata solo la connettività tra aree geografiche. Per ulteriori informazioni, contatta il tuo Adobe account manager.

La documentazione seguente fornisce informazioni su come connettersi a [!DNL Azure Table Storage] Platform utilizzando le API o l’interfaccia utente:

## Connetti [!DNL Azure Table Storage] alla piattaforma utilizzando le API

- [Creare una connessione di base Azure Table Storage utilizzando l’API del servizio di flusso](../../tutorials/api/create/databases/ats.md)
- [Esplorare la struttura dati e il contenuto di un’origine di database utilizzando l’API del servizio di flusso](../../tutorials/api/explore/database-nosql.md)
- [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio di flusso](../../tutorials/api/collect/database-nosql.md)

## Connetti [!DNL Azure Table Storage] alla piattaforma utilizzando l’interfaccia utente

- [Creare una connessione sorgente di archiviazione tabella di Azure nell’interfaccia utente](../../tutorials/ui/create/databases/ats.md)
- [Creazione di un flusso di dati per una connessione sorgente del database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
