---
keywords: Experience Platform;home;argomenti popolari;BigQuery;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Panoramica del connettore sorgente BigQuery Google
topic-legacy: overview
description: Scopri come collegare Google BigQuery a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 7a62dcf1e9712d3c0c0d148b953e50dc11c91f1b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Google BigQuery]

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[!DNL Experience Platform] fornisce il supporto per l’acquisizione di dati da un database di terze parti. Platform può connettersi a diversi tipi di database, ad esempio relazionale, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Google BigQuery].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Consulta la sezione [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Prerequisiti

La sezione seguente fornisce ulteriori informazioni sulla configurazione dei prerequisiti necessaria per creare un [!DNL Google BigQuery] connessione di origine.

### Genera il tuo [!DNL Google BigQuery] credenziali

Connessione [!DNL Google BigQuery] in Platform, devi generare valori per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `project` | Il progetto è l’entità organizzativa a livello di base per il tuo [!DNL Google Cloud] risorse, comprese [!DNL Google BigQuery]. |
| `clientID` | L&#39;ID cliente è la metà del tuo [!DNL Google BigQuery] Credenziali OAuth 2.0. |
| `clientSecret` | Il segreto cliente è l&#39;altra metà del tuo [!DNL Google BigQuery] Credenziali OAuth 2.0. |
| `refreshToken` | Il token di aggiornamento ti consente di ottenere nuovi token di accesso per la tua API. I token di accesso hanno una durata limitata e possono scadere nel corso del progetto. Puoi utilizzare il token di aggiornamento per l’autenticazione e richiedere token di accesso successivi per il progetto, se necessario. |
| `largeResultsDataSetId` | Il pre-creato  [!DNL Google BigQuery] ID set di dati necessario per abilitare il supporto per set di risultati di grandi dimensioni. |

Per istruzioni dettagliate su come generare le credenziali OAuth 2.0 per [!DNL Google] API, vedi quanto segue [[!DNL Google] Guida all’autenticazione di OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

## Connetti [!DNL Google BigQuery] su Platform

La documentazione seguente fornisce informazioni su come connettersi [!DNL Google BigQuery] su Platform utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di base Google BigQuery utilizzando l’API del servizio di flusso](../../tutorials/api/create/databases/bigquery.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio di flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio di flusso](../../tutorials/api/collect/database-nosql.md)

### Utilizzo dell’interfaccia

- [Creare una connessione sorgente Google BigQuery nell’interfaccia utente](../../tutorials/ui/create/databases/bigquery.md)
- [Creazione di un flusso di dati per una connessione sorgente del database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
