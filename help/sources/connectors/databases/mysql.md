---
title: Panoramica di MySQL Source Connector
description: Scopri come connettere MySQL a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2025-05-20T00:00:00Z
exl-id: a18e8e69-880f-4bee-b339-726091d6f858
source-git-commit: 16fe5340582dcea0ff40000fb516c1b72d5f150e
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# [!DNL MySQL]

[!DNL MySQL] è un sistema di gestione di database relazionali open source utilizzato per archiviare e gestire dati strutturati. Organizza i dati in tabelle e utilizza SQL (Structured Query Language) per eseguire query e aggiornare le informazioni. [!DNL MySQL] è ampiamente utilizzato nelle applicazioni Web, supporta più piattaforme ed è noto per la velocità, l&#39;affidabilità e la facilità d&#39;uso.

È possibile utilizzare l&#39;origine [!DNL MySQL] per connettere l&#39;account e acquisire i dati dal database [!DNL MySQL] a Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Leggere le sezioni seguenti per completare la configurazione dei prerequisiti prima di connettere l&#39;account [!DNL MySQl] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform in Azure o Amazon Web Services (AWS), è necessario aggiungere indirizzi IP specifici per l’area geografica al inserisco nell&#39;elenco Consentiti di. Per ulteriori informazioni, leggere la guida su [inserire nell&#39;elenco Consentiti gli indirizzi IP per connettersi ad Experience Platform in Azure e AWS](../../ip-address-allow-list.md).

### Autenticazione in Experience Platform su Azure {#azure}

È possibile utilizzare l&#39;autenticazione con chiave account o l&#39;autenticazione di base per connettere il database [!DNL MySQL] ad Experience Platform in Azure.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Specificare i valori per le credenziali seguenti per connettere il database [!DNL MySQL] ad Experience Platform utilizzando l&#39;autenticazione della chiave account.

| Credenziali | Descrizione |
| --- | --- |
| `connectionString` | La stringa di connessione [!DNL MySQL] associata al tuo account. Schema della stringa di connessione [!DNL MySQL]: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL MySQL]: `26d738e0-8963-47ea-aadf-c60de735468a`. |

Per ulteriori informazioni, leggere la [[!DNL MySQL] documentazione sulle stringhe di connessione](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

>[!TAB Autenticazione di base]

Specificare i valori per le credenziali seguenti per connettere il database [!DNL MySQL] ad Experience Platform utilizzando l&#39;autenticazione di base.

| Credenziali | Descrizione |
| --- | --- |
| `server` | Il nome o l&#39;indirizzo IP del database [!DNL MySQL]. |
| `username` | Il nome utente associato all&#39;autenticazione del database [!DNL MySQL]. |
| `password` | La password associata all&#39;autenticazione del database [!DNL MySQL]. |
| `database` | Nome del database [!DNL MySQL] a cui si desidera connettersi. |
| `sslMode` | Il metodo [!DNL Secure Sockets Layer] (SSL) da applicare alla connessione. I valori disponibili sono: <ul><li>`DISABLED`: utilizzare questa opzione per disabilitare SSL. Se il server richiede una configurazione SSL, la connessione non riuscirà</li><li>`PREFERRED`: utilizzare questa opzione per preferire le connessioni SSL, dato che il server le supporta. Questa opzione consente anche le connessioni non SSL.</li><li>`REQUIRED`: utilizzare questa opzione per rendere obbligatorie le connessioni SSL. Se il server non supporta SSL, le connessioni non riusciranno.</li><li>`Verify-Ca`: utilizzare questa opzione per verificare i certificati del server quando le connessioni non riescono se il server non supporta SSL.</li><li>`Verify Identity`: utilizzare questa opzione per verificare i certificati del server con il nome dell&#39;host durante l&#39;interruzione delle connessioni se il server non supporta SSL.</li></ul> |

>[!ENDTABS]

### Autenticazione per Experience Platform su Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../landing/multi-cloud.md).

Per connettere [!DNL MySQL] ad Experience Platform su AWS è necessario fornire i valori per le credenziali seguenti.

| Credenziali | Descrizione |
| --- | --- |
| `server` | Il nome o l&#39;IP del database [!DNL MySQL]. |
| `username` | Nome del database. |
| `password` | Il nome utente che corrisponde al database. |
| `database` | La password che corrisponde al database. |
| `sslMode` | Valore booleano che controlla se SSL è applicato o meno, a seconda del supporto del server. Il valore predefinito di questa configurazione è `false`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL MySQL] è `26d738e0-8963-47ea-aadf-c60de735468a`. **Nota**: queste credenziali sono necessarie solo per la connessione tramite l&#39;API [!DNL Flow Service]. |

## Connetti [!DNL MySQL] ad Experience Platform tramite API

- [Connetti il database  [!DNL MySQL]  tramite l&#39;API del servizio Flusso](../../tutorials/api/create/databases/mysql.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

## Connettere MySQL ad Experience Platform tramite l’interfaccia utente

- [Connetti il database  [!DNL MySQL]  ad Experience Platform tramite l&#39;interfaccia utente](../../tutorials/ui/create/databases/mysql.md)
- [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
