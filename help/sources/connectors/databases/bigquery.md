---
keywords: Experience Platform;home;argomenti popolari;BigQuery;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Panoramica del connettore di origine Google BigQuery
topic-legacy: overview
description: Scopri come collegare Google BigQuery a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# (Beta) Connettore [!DNL Google BigQuery]

>[!NOTE]
>
>Il [!DNL Google BigQuery] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../home.md#terms-and-conditions) .

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[!DNL Experience Platform] fornisce il supporto per l’acquisizione di dati da un database di terze parti. Platform può connettersi a diversi tipi di database, ad esempio relazionale, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Google BigQuery].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md) .

## Prerequisiti

La sezione seguente fornisce ulteriori informazioni sulla configurazione dei prerequisiti necessaria per creare una connessione sorgente [!DNL Google BigQuery].

### Genera le tue credenziali [!DNL Google BigQuery]

Per connettersi a [!DNL Google BigQuery] Platform, è necessario generare valori per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `project` | Il progetto è l’entità organizzativa a livello di base per le risorse [!DNL Google Cloud], incluso [!DNL Google BigQuery]. |
| `clientID` | L’ID client è la metà delle tue credenziali [!DNL Google BigQuery] OAuth 2.0. |
| `clientSecret` | Il segreto client è l’altra metà delle tue credenziali [!DNL Google BigQuery] OAuth 2.0. |
| `refreshToken` | Il token di aggiornamento ti consente di ottenere nuovi token di accesso per la tua API. I token di accesso hanno una durata limitata e possono scadere nel corso del progetto. Puoi utilizzare il token di aggiornamento per l’autenticazione e richiedere token di accesso successivi per il progetto, se necessario. |

Per istruzioni dettagliate su come generare le credenziali OAuth 2.0 per le API [!DNL Google], consulta la seguente [[!DNL Google] guida all’autenticazione OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

## Connetti [!DNL Google BigQuery] alla piattaforma

La documentazione seguente fornisce informazioni su come connettersi a [!DNL Google BigQuery] Platform utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di base Google BigQuery utilizzando l’API del servizio di flusso](../../tutorials/api/create/databases/bigquery.md)
- [Esplorare la struttura dati e il contenuto di un’origine di database utilizzando l’API del servizio di flusso](../../tutorials/api/explore/database-nosql.md)
- [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio di flusso](../../tutorials/api/collect/database-nosql.md)

### Utilizzo dell’interfaccia

- [Creare una connessione sorgente Google BigQuery nell’interfaccia utente](../../tutorials/ui/create/databases/bigquery.md)
- [Creazione di un flusso di dati per una connessione sorgente del database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
