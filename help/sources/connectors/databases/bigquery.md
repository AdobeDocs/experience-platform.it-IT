---
title: Panoramica del connettore Source BigQuery Google
description: Scopri come collegare Google BigQuery a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1900a8c6a3f3119c8b9049b12f5660cc9fd181a2
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Origine [!DNL Google BigQuery]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Google BigQuery] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.

Leggere questo documento per i passaggi preliminari da completare per connettere correttamente l&#39;account [!DNL Google BigQuery] a Adobe Experience Platform in Azure o Amazon Web Services (AWS).

## Prerequisiti {#prerequisites}

Leggere le sezioni seguenti relative alla configurazione dei prerequisiti da completare prima di connettere l&#39;account [!DNL Google BigQuery] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform in Azure o Amazon Web Services (AWS), è necessario aggiungere indirizzi IP specifici per l’area geografica al inserisco nell&#39;elenco Consentiti di. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform in Azure e AWS](../../ip-address-allow-list.md).

### Autenticazione in Experience Platform su Azure {#azure}

Per connettere l&#39;account [!DNL Google BigQuery] ad Experience Platform su Azure, è necessario fornire le credenziali seguenti.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per eseguire l’autenticazione utilizzando una combinazione di OAuth 2.0 e autenticazione di base, fornisci i valori appropriati per le seguenti credenziali.

| Credenziali | Descrizione |
| --- | --- |
| `project` | Il progetto è l&#39;entità organizzativa di base per le risorse [!DNL Google Cloud], incluso [!DNL Google BigQuery]. |
| `clientID` | L&#39;ID client corrisponde alla metà delle credenziali OAuth 2.0 di [!DNL Google BigQuery]. |
| `clientSecret` | Il segreto client è l&#39;altra metà delle credenziali OAuth 2.0 di [!DNL Google BigQuery]. |
| `refreshToken` | Il token di aggiornamento consente di ottenere nuovi token di accesso per l’API. I token di accesso hanno una durata limitata e possono scadere nel corso del progetto. Puoi utilizzare il token di aggiornamento per autenticare e richiedere token di accesso successivi per il progetto, quando necessario. |
| `largeResultsDataSetId` | (Facoltativo) L&#39;ID del set di dati [!DNL Google BigQuery] precreato necessario per abilitare il supporto per set di risultati di grandi dimensioni. |

Per istruzioni dettagliate su come generare credenziali OAuth 2.0 per le API [!DNL Google], consulta la [[!DNL Google] Guida all’autenticazione di OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

>[!TAB Autenticazione del servizio]

Per eseguire l&#39;autenticazione tramite l&#39;autenticazione del servizio, specificare i valori appropriati per le credenziali seguenti.

**Nota**: l&#39;account del servizio deve disporre di autorizzazioni sufficienti, ad esempio **[!DNL BigQuery Job User]**, **[!DNL BigQuery Data Viewer]**, **[!DNL BigQuery Read Session User]** e **[!DNL BigQuery Data Owner]** per eseguire l&#39;autenticazione con l&#39;autenticazione del servizio.

| Credenziali | Descrizione |
| --- | --- |
| `projectId` | ID di [!DNL Google BigQuery] su cui si desidera eseguire la query. |
| `keyFileContent` | File di chiave utilizzato per autenticare l&#39;account del servizio. Puoi recuperare questo valore dal [[!DNL Google Cloud service accounts] dashboard](https://console.cloud.google.com). Il contenuto del file chiave è in formato JSON. È necessario codificarlo in [!DNL Base64] durante l&#39;autenticazione in Experience Platform. |
| `largeResultsDataSetId` | (Facoltativo) L&#39;ID del set di dati [!DNL Google BigQuery] precreato necessario per abilitare il supporto per set di risultati di grandi dimensioni. |

Per ulteriori informazioni sull&#39;utilizzo degli account del servizio in [!DNL Google BigQuery], leggere la guida in [utilizzo degli account del servizio in [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts).

>[!ENDTABS]

### Autenticazione per Experience Platform su AWS {#aws}

Per connettere l&#39;account [!DNL Google BigQuery] a Experience Platform su AWS, è necessario fornire le credenziali seguenti.

| Credenziali | Descrizione |
| --- | --- |
| `projectId` | ID di [!DNL Google BigQuery] su cui si desidera eseguire la query. |
| `keyFileContent` | File di chiave utilizzato per autenticare l&#39;account del servizio. Puoi recuperare questo valore dal [[!DNL Google Cloud service accounts] dashboard](https://console.cloud.google.com). Il contenuto del file chiave è in formato JSON. È necessario codificarlo in [!DNL Base64] durante l&#39;autenticazione in Experience Platform. |
| `datasetId` | ID del set di dati [!DNL Google BigQuery]. Questo ID rappresenta dove si trovano le tabelle di dati. |

## Connetti [!DNL Google BigQuery] ad Experience Platform

La documentazione seguente fornisce informazioni su come connettere [!DNL Google BigQuery] ad Experience Platform tramite API o tramite l&#39;interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di base BigQuery Google utilizzando l’API del servizio Flow](../../tutorials/api/create/databases/bigquery.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

### Utilizzo dell’interfaccia utente

- [Creare una connessione sorgente BigQuery Google nell’interfaccia utente](../../tutorials/ui/create/databases/bigquery.md)
- [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
