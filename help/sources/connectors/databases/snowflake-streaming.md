---
title: Panoramica del connettore Source per streaming di Snowflake
description: Scopri come creare una connessione di origine e un flusso di dati per acquisire i dati in streaming dall’istanza di Snowflake a Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-09-24T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: 34b1676ebb5405d73cf37cd786d1e6c26cb8fdaa
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---

# [!DNL Snowflake] origine streaming

>[!IMPORTANT]
>
> L&#39;origine di streaming [!DNL Snowflake] è disponibile nell&#39;API per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce il supporto per lo streaming dei dati da un database [!DNL Snowflake].

## Informazioni sull&#39;origine di streaming [!DNL Snowflake]

L&#39;origine di flusso [!DNL Snowflake] funziona caricando i dati eseguendo periodicamente una query SQL e creando un record di output per ogni riga nel set risultante.

Utilizzando [!DNL Kafka Connect], l&#39;origine di streaming [!DNL Snowflake] tiene traccia dell&#39;ultimo record ricevuto da ogni tabella, in modo che possa iniziare nella posizione corretta per l&#39;iterazione successiva. L’origine utilizza questa funzionalità per filtrare i dati e ottenere solo le righe aggiornate da una tabella su ogni iterazione.

## Prerequisiti

La sezione seguente illustra i passaggi preliminari da completare prima di poter inviare dati dal database [!DNL Snowflake] all&#39;Experience Platform:

### Aggiorna l’elenco consentiti del tuo indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md#ip-address-allow-list-for-streaming-sources).

La documentazione seguente fornisce informazioni su come connettere [!DNL Amazon Redshift] a Platform tramite API o tramite l&#39;interfaccia utente:

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Snowflake], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| `account` | L&#39;identificatore account completo (nome account o localizzatore account) dell&#39;account [!DNL Snowflake] aggiunto al suffisso `snowflakecomputing.com`. L’identificatore dell’account può essere in diversi formati: <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (esempio: `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (esempio: `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (esempio: `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Per ulteriori informazioni, leggere [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati a Platform. |
| `database` | Il database [!DNL Snowflake] contiene i dati che si desidera inserire nella piattaforma. |
| `username` | Nome utente per l&#39;account [!DNL Snowflake]. |
| `password` | Password per l&#39;account utente [!DNL Snowflake]. |
| `role` | (Facoltativo) Ruolo personalizzato che può essere fornito a un utente, per una determinata connessione. Se non specificato, il valore predefinito è `public`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL Snowflake] è `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

{style="table-layout:auto"}

### Configurare le impostazioni del ruolo {#configure-role-settings}

È necessario configurare i privilegi per un ruolo, anche se il ruolo pubblico predefinito è assegnato, per consentire alla connessione di origine di accedere al database, allo schema e alla tabella [!DNL Snowflake] rilevanti. I vari privilegi per le diverse entità [!DNL Snowflake] sono i seguenti:

| Entità [!DNL Snowflake] | Richiedi privilegio ruolo |
| --- | --- |
| Data warehouse | FUNZIONAMENTO, UTILIZZO |
| Database | UTILIZZO |
| Schema | UTILIZZO |
| Tabella | SELEZIONA |

>[!NOTE]
>
>Nella configurazione delle impostazioni avanzate del magazzino devono essere abilitate le funzioni Ripresa automatica e Sospensione automatica.

Per ulteriori informazioni sulla gestione di ruoli e privilegi, fare riferimento al [[!DNL Snowflake] riferimento API](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Limitazioni e domande frequenti {#limitations-and-frequently-asked-questions}

* La velocità effettiva dei dati per l&#39;origine [!DNL Snowflake] è di 2.000 record al secondo.
* I prezzi possono variare in base al periodo di tempo in cui è attiva una warehouse e alle dimensioni della warehouse. Per l&#39;integrazione di origine [!DNL Snowflake], è sufficiente la data warehouse di piccole dimensioni, x-small. Si consiglia di abilitare la sospensione automatica in modo che il magazzino possa sospendere da solo quando non è in uso.
* L&#39;origine [!DNL Snowflake] esegue il polling del database per i nuovi dati ogni 10 secondi.
* Opzioni di configurazione:
   * È possibile abilitare un flag booleano `backfill` per l&#39;origine [!DNL Snowflake] durante la creazione di una connessione di origine.
      * Se backfill è impostato su true, il valore di timestamp.initial è impostato su 0. Ciò significa che vengono recuperati dati con una colonna di marca temporale maggiore di 0 epoca.
      * Se backfill è impostato su false, il valore di timestamp.initial è impostato su -1. Ciò significa che vengono recuperati i dati con una colonna di marca temporale maggiore dell’ora corrente (l’ora in cui inizia l’acquisizione della sorgente).
   * La colonna timestamp deve essere formattata come tipo: `TIMESTAMP_LTZ` o `TIMESTAMP_NTZ`. Se la colonna timestamp è impostata su `TIMESTAMP_NTZ`, il fuso orario corrispondente in cui sono archiviati i valori deve essere passato tramite il parametro `timezoneValue`. Se non specificato, il valore predefinito è UTC.
      * Impossibile utilizzare `TIMESTAMP_TZ` in una colonna timestamp o in una mappatura.

## Passaggi successivi

Il seguente tutorial illustra i passaggi necessari per collegare l&#39;origine di streaming [!DNL Snowflake] ad Experience Platform utilizzando l&#39;API:

* [Trasmetti i dati da un database  [!DNL Snowflake]  all&#39;Experience Platform utilizzando l&#39;API del servizio Flusso](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Trasmetti dati da un database  [!DNL Snowflake]  a Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente di Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
