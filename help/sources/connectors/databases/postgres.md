---
title: Panoramica di PostgreSQL Source Connector
description: Scopri l’origine PostgreSQL su Adobe Experience Platform.
exl-id: 27b891c5-5fc5-4539-8f98-e3a53e2eefe3
source-git-commit: 98d1bec3cd453f3a20b8871b891b5464ddd44a09
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL PostgreSQL]

Leggere questo documento per informazioni sui passaggi preliminari da completare prima di connettere il database [!DNL PostgreSQL] a Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Leggere le sezioni seguenti per completare la configurazione dei prerequisiti prima di connettere il database [!DNL PostgreSQL] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform in Azure o Amazon Web Services (AWS), è necessario aggiungere indirizzi IP specifici per l’area geografica al inserisco nell&#39;elenco Consentiti di. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform in Azure e AWS](../../ip-address-allow-list.md).

### Autenticazione in Experience Platform su Azure {#azure}

Per connettere [!DNL PostgreSQL] ad Experience Platform in Azure, è necessario fornire i valori per le credenziali di autenticazione seguenti.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Specificare i valori per le credenziali seguenti per connettere il database [!DNL PostgreSQL] ad Experience Platform in Azure utilizzando l&#39;autenticazione della chiave dell&#39;account.

| Credenziali | Descrizione |
| --- | --- |
| `connectionString` | Stringa di connessione associata all&#39;account [!DNL PostgreSQL]. Schema della stringa di connessione [!DNL PostgreSQL]: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL PostgreSQL] è `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Per ulteriori informazioni, consulta la [[!DNL PostgreSQL] documentazione](https://www.postgresql.org/docs/current/).

>[!TAB Autenticazione di base]

Specificare i valori per le credenziali seguenti per connettere il database [!DNL PostgreSQL] ad Experience Platform su Azure utilizzando l&#39;autenticazione di base.

| Credenziali | Descrizione |
| --- | --- |
| `server` | Il nome o l&#39;indirizzo IP del database [!DNL PostgreSQL]. |
| `port` | Porta TCP del server [!DNL PostgreSQL]. |
| `username` | Il nome utente associato all&#39;autenticazione del database [!DNL PostgreSQL]. |
| `password` | La password associata all&#39;autenticazione del database [!DNL PostgreSQL]. |
| `database` | Nome del database [!DNL PostgreSQL] a cui si desidera connettersi. |
| `sslMode` | Il metodo [!DNL Secure Sockets Layer] (SSL) da applicare alla connessione. I valori disponibili sono: <ul><li>`Disable`: utilizzare questa opzione per disabilitare SSL. Se il server richiede una configurazione SSL, la connessione non riuscirà.</li><li>`Allow`: utilizzare questa opzione per consentire connessioni SSL. Le connessioni non SSL possono comunque essere utilizzate se il server le supporta.</li><li>`Prefer`: utilizzare questa opzione per preferire le connessioni SSL, dato che il server le supporta. Questa opzione consente anche le connessioni non SSL.</li><li>`Require`: utilizzare questa opzione per rendere obbligatorie le connessioni SSL. Se il server non supporta SSL, le connessioni non riusciranno.</li><li>`Verify-Ca`: utilizzare questa opzione per verificare i certificati del server quando le connessioni non riescono se il server non supporta SSL.</li><li>`Verify-Full`: utilizzare questa opzione per verificare i certificati del server con il nome dell&#39;host durante l&#39;interruzione delle connessioni se il server non supporta SSL.</li></ul> |

Per ulteriori informazioni, consulta la [[!DNL PostgreSQL] documentazione](https://www.postgresql.org/docs/current/).

>[!ENDTABS]

### Autenticazione per Experience Platform su Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../landing/multi-cloud.md).

Specificare i valori per le credenziali seguenti per connettere il database [!DNL PostgreSQL] ad Experience Platform su AWS utilizzando l&#39;autenticazione di base.

| Credenziali | Descrizione |
| --- | --- |
| `server` | Il nome o l&#39;indirizzo IP del database [!DNL PostgreSQL]. |
| `port` | Porta TCP del server [!DNL PostgreSQL]. |
| `username` | Il nome utente associato all&#39;autenticazione del database [!DNL PostgreSQL]. |
| `password` | La password associata all&#39;autenticazione del database [!DNL PostgreSQL]. |
| `database` | Nome del database [!DNL PostgreSQL] a cui si desidera connettersi. |
| `sslMode` | Il metodo [!DNL Secure Sockets Layer] (SSL) da applicare alla connessione. I valori disponibili sono: <ul><li>`Disable`: utilizzare questa opzione per disabilitare SSL. Se il server richiede una configurazione SSL, la connessione non riuscirà.</li><li>`Allow`: utilizzare questa opzione per consentire connessioni SSL. Le connessioni non SSL possono comunque essere utilizzate se il server le supporta.</li><li>`Prefer`: utilizzare questa opzione per preferire le connessioni SSL, dato che il server le supporta. Questa opzione consente anche le connessioni non SSL.</li><li>`Require`: utilizzare questa opzione per rendere obbligatorie le connessioni SSL. Se il server non supporta SSL, le connessioni non riusciranno.</li><li>`Verify-Ca`: utilizzare questa opzione per verificare i certificati del server quando le connessioni non riescono se il server non supporta SSL.</li><li>`Verify-Full`: utilizzare questa opzione per verificare i certificati del server con il nome dell&#39;host durante l&#39;interruzione delle connessioni se il server non supporta SSL.</li></ul> |

Per ulteriori informazioni, consulta la [[!DNL PostgreSQL] documentazione](https://www.postgresql.org/docs/current/).

## Connetti [!DNL PostgreSQL] ad Experience Platform tramite API

* [Crea una connessione di base  [!DNL PostgreSQL]  utilizzando l&#39;API del servizio Flusso](../../tutorials/api/create/databases/postgres.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

## Connetti [!DNL PostgreSQL] ad Experience Platform tramite l&#39;interfaccia utente

* [Crea una connessione di origine  [!DNL PostgreSQL]  nell&#39;interfaccia utente](../../tutorials/ui/create/databases/postgres.md)
* [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
