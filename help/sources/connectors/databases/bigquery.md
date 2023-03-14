---
keywords: Experience Platform;home;argomenti popolari;BigQuery;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Panoramica del connettore di origine BigQuery Google
description: Scopri come collegare Google BigQuery a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# [!DNL Google BigQuery]

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

[!DNL Experience Platform] fornisce supporto per l’acquisizione di dati da un database di terze parti. Platform può connettersi a diversi tipi di database, ad esempio database relazionali, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Google BigQuery].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Prerequisiti

La sezione seguente fornisce ulteriori informazioni sui prerequisiti necessari per la creazione di un [!DNL Google BigQuery] connessione sorgente.

### Genera il [!DNL Google BigQuery] credenziali

Per connettersi [!DNL Google BigQuery] In Platform, devi generare i valori per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `project` | Il progetto è l&#39;entità organizzativa di base per il [!DNL Google Cloud] risorse, tra cui [!DNL Google BigQuery]. |
| `clientID` | L&#39;ID client è la metà del [!DNL Google BigQuery] Credenziali OAuth 2.0. |
| `clientSecret` | Il segreto cliente è l&#39;altra metà del tuo [!DNL Google BigQuery] Credenziali OAuth 2.0. |
| `refreshToken` | Il token di aggiornamento consente di ottenere nuovi token di accesso per l’API. I token di accesso hanno una durata limitata e possono scadere nel corso del progetto. Puoi utilizzare il token di aggiornamento per autenticare e richiedere token di accesso successivi per il progetto, quando necessario. |
| `largeResultsDataSetId` | Il predefinito  [!DNL Google BigQuery] ID del set di dati necessario per abilitare il supporto per set di risultati di grandi dimensioni. |

Per istruzioni dettagliate su come generare credenziali OAuth 2.0 per [!DNL Google] API, vedi quanto segue [[!DNL Google] Guida all’autenticazione di OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

## Connetti [!DNL Google BigQuery] alla piattaforma

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Google BigQuery] in Platform tramite API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di base BigQuery Google utilizzando l’API del servizio Flow](../../tutorials/api/create/databases/bigquery.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

### Utilizzo dell’interfaccia utente

- [Creare una connessione sorgente BigQuery Google nell’interfaccia utente](../../tutorials/ui/create/databases/bigquery.md)
- [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
