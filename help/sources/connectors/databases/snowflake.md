---
title: Panoramica del connettore Source di Snowflake
description: Scopri come collegare il Snowflake a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8b0f6eca87deedd8090830e3375d5099bfb0dfc0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Origine [!DNL Snowflake]

>[!IMPORTANT]
>
>* L&#39;origine [!DNL Snowflake] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.
>* Per impostazione predefinita, l&#39;origine [!DNL Snowflake] interpreta `null` come una stringa vuota. Contatta il tuo rappresentante di Adobe per assicurarti che i valori `null` siano scritti correttamente come `null` in Adobe Experience Platform.
>* Ad Experience Platform, per acquisire i dati, i fusi orari per tutte le origini batch basate su tabelle devono essere configurati in formato UTC. L&#39;unico indicatore orario supportato per l&#39;origine [!DNL Snowflake] è TIMESTAMP_NTZ con ora UTC.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un database di terze parti. Platform può connettersi a diversi tipi di database, ad esempio database relazionali, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Snowflake].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

La documentazione seguente fornisce informazioni su come connettere [!DNL Snowflake] a Platform tramite API o tramite l&#39;interfaccia utente:

## Connetti [!DNL Snowflake] a Platform tramite API

* [Creare una connessione di base al Snowflake utilizzando l’API del servizio Flusso](../../tutorials/api/create/databases/snowflake.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

## Connetti [!DNL Snowflake] a Platform tramite l&#39;interfaccia utente

* [Creare una connessione sorgente del Snowflake nell’interfaccia utente](../../tutorials/ui/create/databases/snowflake.md)
* [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
