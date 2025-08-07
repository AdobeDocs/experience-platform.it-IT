---
title: Panoramica del connettore Source di Oracle DB
description: Scopri come collegare Oracle a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2025-08-06T00:00:00Z
exl-id: be422cf8-fb24-48c7-8369-34f0f2ec95fc
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# [!DNL Oracle DB]

[!DNL Oracle DB] è un potente sistema di gestione del database relazionale sviluppato da [!DNL Oracle Corporation]. È possibile utilizzare [!DNL Oracle DB] per archiviare, gestire e recuperare grandi volumi di dati strutturati in modo efficiente e sicuro.

Utilizza l&#39;origine [!DNL Oracle DB] nel catalogo origini di Adobe Experience Platform per collegare il database e acquisire i dati in Experience Platform.

## Prerequisiti {#prerequisites}

Leggere le sezioni seguenti per completare la configurazione dei prerequisiti prima di connettere l&#39;account [!DNL Oracle DB] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform in Azure o Amazon Web Services (AWS), è necessario aggiungere indirizzi IP specifici per l’area geografica al inserisco nell&#39;elenco Consentiti di. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform in Azure e AWS](../../ip-address-allow-list.md).

### Autenticazione in Experience Platform su Azure {#azure}

Specificare una stringa di connessione per autenticare e connettere l&#39;account [!DNL Oracle DB] ad Experience Platform in Azure.

| Credenziali | Descrizione |
| --- | --- |
| Stringa di connessione | Una stringa di connessione è una stringa di testo utilizzata dalle applicazioni per connettersi a un database. Schema della stringa di connessione [!DNL Oracle DB]: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| ID specifica di connessione | L&#39;ID della specifica di connessione restituisce le proprietà del connettore di origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Oracle]: `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Nota**: queste credenziali sono necessarie solo per la connessione tramite l&#39;API [!DNL Flow Service]. |

### Autenticazione per Experience Platform su Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../landing/multi-cloud.md).

Immetti i valori per le seguenti credenziali per autenticare e connettere l&#39;account [!DNL Oracle DB] ad Experience Platform su AWS.

| Credenziali | Descrizione |
| --- | --- |
| Server | Indirizzo IP o nome host del server [!DNL Oracle DB]. |
| Porta | Numero di porta del server di database. Il numero di porta predefinito è `1521`. |
| Nome utente | Account utente [!DNL Oracle DB] utilizzato per l&#39;autenticazione e l&#39;accesso al database. |
| Password | Chiave segreta associata al nome utente, utilizzata per l’autenticazione. |
| Database | L&#39;istanza di database [!DNL Oracle] specifica a cui si desidera connettersi. |
| Schema | Contenitore per gli oggetti di database, ad esempio tabelle, viste o routine. |
| Modalità SSL | Valore booleano che controlla se SSL è applicato o meno. Questa configurazione dipende dal supporto del server e viene impostata come predefinita `false`. |
| ID specifica di connessione | L&#39;ID della specifica di connessione restituisce le proprietà del connettore di origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Oracle]: `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Nota**: queste credenziali sono necessarie solo per la connessione tramite l&#39;API [!DNL Flow Service]. |


## Connetti [!DNL Oracle] a [!DNL Experience Platform] tramite API

- [Connettere Oracle DB utilizzando l’API del servizio Flusso](../../tutorials/api/create/databases/oracle.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

## Connetti [!DNL Oracle] a [!DNL Experience Platform] tramite l&#39;interfaccia utente

- [Connetti Oracle DB utilizzando l’area di lavoro dell’interfaccia utente di Experience Platform.](../../tutorials/ui/create/databases/oracle.md)
- [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
