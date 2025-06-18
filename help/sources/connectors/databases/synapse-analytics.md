---
title: Panoramica del connettore Source di Azure Synapse Analytics
description: Scopri come collegare Azure Synapse Analytics a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 3%

---

# [!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Azure Synapse Analytics] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.

[!DNL Azure Synapse Analytics] è un servizio di analisi basato su cloud che unifica big data e data warehousing. È possibile acquisire, esplorare, preparare e analizzare i dati utilizzando gli strumenti SQL, [!DNL Spark] o in tempo reale, il tutto senza spostare i dati.

È possibile utilizzare l&#39;origine [!DNL Azure Synapse Analytics] per connettere l&#39;account e trasferire i dati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Leggere le sezioni seguenti per completare la configurazione dei prerequisiti prima di connettere l&#39;account [!DNL Azure Synapse Analytics] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform](../../ip-address-allow-list.md).

### Configurare le autorizzazioni

Per connettere l’account di origine a Experience Platform, è necessario che entrambe le autorizzazioni seguenti siano abilitate:

* **Visualizza origini**
* **Gestisci origini**

Se non disponi di queste autorizzazioni, contatta l’amministratore del prodotto per richiedere l’accesso. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/ui/overview.md).

### Autenticazione per Experience Platform

È possibile utilizzare l&#39;autenticazione della chiave account o l&#39;autenticazione della chiave service-principal per connettere [!DNL Azure Synapse Analytics] ad Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Specificare i valori per le credenziali seguenti per connettere il database [!DNL Azure Synapse Analytics] ad Experience Platform utilizzando l&#39;autenticazione della chiave account.

| Credenziali | Descrizione |
| --- | --- |
| Stringa di connessione | **stringa di connessione** utilizzata per l&#39;autenticazione con [!DNL Azure Synapse Analytics]. Formato standard: `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. Sostituire i segnaposto con i dettagli di connessione effettivi. |
| ID specifica di connessione | La **specifica di connessione** fornisce le proprietà del connettore di un&#39;origine dati. Ciò include dettagli quali le specifiche di autenticazione e i requisiti per la creazione di connessioni **base** e **source**. Per [!DNL Azure Synapse Analytics], l&#39;ID della specifica di connessione è: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Nota:** questa credenziale è necessaria solo per la connessione tramite API. |

>[!TAB Autenticazione chiave entità servizio]

Per recuperare le credenziali per l&#39;autenticazione della chiave dell&#39;entità servizio, passare a [[!DNL Microsfot Entra admin center]](https://entra.microsoft.com/#home) e recuperare i valori per:

* ID app
* Nome visualizzato
* Segreto
* ID tenant

Passare quindi all&#39;[[!DNL Azure Synapse Analytics] istanza](https://azure.microsoft.com/en-ca/products/synapse-analytics) e selezionare l&#39;opzione per creare un utente da un provider esterno. Da qui, fornisci le autorizzazioni appropriate per l’entità servizio nello schema. **NOTA:**: è necessario includere &quot;SELECT&quot; in quanto è necessario per l&#39;anteprima dello schema, in modo analogo a &quot;COPY&quot;. Un esempio di comando può essere:

```SQL
GRANT SELECT ON SCHEMA::dbo TO {APP_ID};
```

Specificare i valori per le credenziali seguenti per connettere il database [!DNL Azure Synapse Analytics] ad Experience Platform utilizzando l&#39;autenticazione della chiave dell&#39;entità servizio.

| Credenziali | Descrizione |
| --- | --- |
| Server | Il nome di dominio completo dell&#39;endpoint SQL [!DNL Azure Synapse Analytics]. |
| Database | Il nome del database specifico nell&#39;area di lavoro [!DNL Azure Synapse Analytics]. |
| Tenant | L&#39;ID tenant [!DNL Azure Active Directory] associato alla sottoscrizione [!DNL Azure]. |
| ID entità principale servizio | ID client di un&#39;applicazione [!DNL Azure Active Directory]. |
| Chiave servizio entità principale | Il segreto client o la password associati all&#39;entità servizio. |
| ID specifica di connessione | La **specifica di connessione** fornisce le proprietà del connettore di un&#39;origine dati. Ciò include dettagli quali le specifiche di autenticazione e i requisiti per la creazione di connessioni **base** e **source**. Per [!DNL Azure Synapse Analytics], l&#39;ID della specifica di connessione è: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Nota:** questa credenziale è necessaria solo per la connessione tramite API. |

Per ulteriori informazioni, leggere la [[!DNL Azure] documentazione sulla gestione delle identità per  [!DNL Azure Synapse Analytics]](https://learn.microsoft.com/en-us/azure/synapse-analytics/synapse-service-identity).

>[!ENDTABS]

## Connetti [!DNL Azure Synapse Analytics] ad Experience Platform tramite API

* [Connetti [!DNL Azure Synapse Analytics] ad Experience Platform utilizzando l&#39;API del servizio Flusso](../../tutorials/api/create/databases/synapse-analytics.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

## Connetti [!DNL Azure Synapse Analytics] ad Experience Platform tramite l&#39;interfaccia utente

* [Connetti [!DNL Azure Synapse Analytics] ad Experience Platform nell&#39;interfaccia utente](../../tutorials/ui/create/databases/synapse-analytics.md)
* [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)

