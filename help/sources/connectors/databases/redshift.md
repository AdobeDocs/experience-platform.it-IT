---
title: Panoramica del connettore Source Amazon Redshift
description: Scopri come collegare Amazon Redshift a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Origine [!DNL Amazon Redshift]

>[!IMPORTANT]
>
>- L&#39;origine [!DNL Amazon Redshift] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time CDP Ultimate.
>
>- È ora possibile utilizzare l&#39;origine [!DNL Amazon Redshift] quando si esegue Adobe Experience Platform su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../landing/multi-cloud.md).


Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un database di terze parti. Experience Platform può connettersi a diversi tipi di database, ad esempio database relazionali, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Amazon Redshift].

## Configura l&#39;origine [!DNL Amazon Redshift] per Experience Platform su Azure {#azure}

Segui i passaggi seguenti per scoprire come configurare l&#39;account [!DNL Amazon Redshift] per Experience Platform su Azure.

### ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Configura l&#39;origine [!DNL Amazon Redshift] per Experience Platform su Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../landing/multi-cloud.md).

### Indirizzo IP da inserire nell&#39;elenco Consentiti per la connessione su AWS

Prima di collegare le origini a Experience Platform su AWS, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida su [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform su AWS](../../ip-address-allow-list.md).

## Connetti [!DNL Amazon Redshift] ad Experience Platform tramite API

- [Connettere Amazon Redshift ad Experience Platform utilizzando l’API del servizio Flow](../../tutorials/api/create/databases/redshift.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

## Connetti [!DNL Amazon Redshift] ad Experience Platform tramite l&#39;interfaccia utente

- [Creare una connessione sorgente Amazon Redshift nell’interfaccia utente](../../tutorials/ui/create/databases/redshift.md)
- [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
