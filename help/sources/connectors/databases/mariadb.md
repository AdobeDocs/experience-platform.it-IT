---
title: Panoramica del connettore Source MariaDB
description: Scopri come collegare MariaDB a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# [!DNL MariaDB]

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Experience Platform]. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un database di terze parti. [!DNL Experience Platform] può connettersi a diversi tipi di database, ad esempio database relazionali, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL MariaDB].

## Prerequisiti {#prerequisites}

Leggere le sezioni seguenti per completare la configurazione dei prerequisiti prima di connettere l&#39;account [!DNL MariaDB] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform](../../ip-address-allow-list.md).

### Autenticazione per Experience Platform

Per connettere [!DNL MariaDB] ad Experience Platform è necessario fornire i valori per le credenziali seguenti.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Per utilizzare l&#39;autenticazione della chiave dell&#39;account, specificare i valori appropriati per le credenziali seguenti.

| Credenziali | Descrizione |
| --- | --- |
| `connectionString` | Stringa di connessione associata all&#39;autenticazione [!DNL MariaDB]. Schema della stringa di connessione [!DNL MariaDB]: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL MariaDB] è `3000eb99-cd47-43f3-827c-43caf170f015`. **Nota**: queste credenziali sono necessarie solo per la connessione tramite l&#39;API [!DNL Flow Service]. |

Per ulteriori informazioni su come ottenere una stringa di connessione, fare riferimento a questo [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!TAB Autenticazione di base]

Per utilizzare l&#39;autenticazione di base, specificare i valori appropriati per le credenziali seguenti.

| Credenziali | Descrizione |
| --- | --- |
| `server` | Il nome o l&#39;IP del database [!DNL MariaDB]. |
| `username` | Nome del database. |
| `port` | Numero di porta dell&#39;endpoint di comunicazione a cui ci si sta connettendo. |
| `password` | Il nome utente che corrisponde al database. |
| `database` | La password che corrisponde al database. |
| `sslMode` | Il metodo con cui i dati vengono crittografati durante il trasferimento. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL MariaDB] è `3000eb99-cd47-43f3-827c-43caf170f015`. **Nota**: queste credenziali sono necessarie solo per la connessione tramite l&#39;API [!DNL Flow Service]. |

Per ulteriori informazioni su come ottenere una stringa di connessione, fare riferimento a questo [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!ENDTABS]

## Connetti [!DNL MariaDB] ad Experience Platform tramite API

- [Creare una connessione di base MariaDB utilizzando l’API del servizio Flusso](../../tutorials/api/create/databases/mariadb.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

## Connetti [!DNL MariaDB] ad Experience Platform tramite l&#39;interfaccia utente

- [Creare una connessione sorgente MariaDB nell’interfaccia utente](../../tutorials/ui/create/databases/mariadb.md)
- [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
