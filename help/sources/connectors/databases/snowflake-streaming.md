---
title: Panoramica del connettore di origine per lo streaming di Snowflake
description: Scopri come creare una connessione di origine e un flusso di dati per acquisire i dati in streaming dall’istanza di Snowflake a Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 1%

---

# [!DNL Snowflake] origine streaming

>[!IMPORTANT]
>
>* Il [!DNL Snowflake] l&#39;origine di streaming è in versione beta. Leggi le [Panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.
>* Il [!DNL Snowflake] l’origine di streaming è disponibile nell’API per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per lo streaming di dati da una [!DNL Snowflake] database.

## Comprensione di [!DNL Snowflake] origine streaming

Il [!DNL Snowflake] l&#39;origine di streaming funziona caricando i dati eseguendo periodicamente una query SQL e creando un record di output per ogni riga del set risultante.

Utilizzando [!DNL Kafka Connect], il [!DNL Snowflake] l&#39;origine di streaming tiene traccia del record più recente ricevuto da ogni tabella, in modo che possa iniziare nella posizione corretta per l&#39;iterazione successiva. L’origine utilizza questa funzionalità per filtrare i dati e ottenere solo le righe aggiornate da una tabella su ogni iterazione.

## Prerequisiti

La sezione seguente illustra i passaggi prerequisiti da completare prima di poter inviare i dati dal [!DNL Snowflake] database di Experience Platform:

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Snowflake], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| `account` | Il nome completo dell&#39;account associato al [!DNL Snowflake] account. Un sistema completo [!DNL Snowflake] il nome account include il nome account, l’area geografica e la piattaforma cloud. Ad esempio, `cj12345.east-us-2.azure`. Per ulteriori informazioni sui nomi degli account, consulta questa [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Il [!DNL Snowflake] warehouse gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni [!DNL Snowflake] il data warehouse è indipendente l’uno dall’altro e deve essere accessibile singolarmente quando si trasferiscono i dati su Platform. |
| `database` | Il [!DNL Snowflake] Il database contiene i dati che desideri inserire in Platform. |
| `username` | Nome utente per [!DNL Snowflake] account. |
| `password` | La password per [!DNL Snowflake] account utente. |
| `role` | (Facoltativo) Ruolo personalizzato che può essere fornito a un utente, per una determinata connessione. Se non specificato, il valore predefinito è `public`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Snowflake] è `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

Per ulteriori informazioni sull’autenticazione, consulta [[!DNL Snowflake] documento](<https://docs.snowflake.com/en/user-guide/key-pair-auth.html>).

### Configurare le impostazioni del ruolo {#configure-role-settings}

È necessario configurare i privilegi per un ruolo, anche se il ruolo pubblico predefinito è assegnato, per consentire alla connessione di origine di accedere al relativo [!DNL Snowflake] database, schema e tabella. I vari privilegi per diversi [!DNL Snowflake] entità è il seguente:

| [!DNL Snowflake] entità | Richiedi privilegio ruolo |
| --- | --- |
| Data warehouse | FUNZIONAMENTO, UTILIZZO |
| Database | UTILIZZO |
| Schema | UTILIZZO |
| Tabella | SELEZIONA |

>[!NOTE]
>
>Nella configurazione delle impostazioni avanzate del magazzino devono essere abilitate le funzioni Ripresa automatica e Sospensione automatica.

Per ulteriori informazioni sulla gestione di ruoli e privilegi, fare riferimento a [[!DNL Snowflake] Riferimento API](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Limitazioni e domande frequenti {#limitations-and-frequently-asked-questions}

* Velocità effettiva dei dati per [!DNL Snowflake] l&#39;origine è di 2000 record al secondo.
* I prezzi possono variare in base al periodo di tempo in cui è attiva una warehouse e alle dimensioni della warehouse. Per [!DNL Snowflake] integrazione di origine, il magazzino di dimensioni più piccole, x-small è sufficiente. Si consiglia di abilitare la sospensione automatica in modo che il magazzino possa sospendere da solo quando non è in uso.
* Il [!DNL Snowflake] l&#39;origine esegue il polling del database per i nuovi dati ogni 10 secondi.
* Opzioni di configurazione:
   * È possibile abilitare una `backfill` flag booleano per [!DNL Snowflake] origine durante la creazione di una connessione di origine.
      * Se backfill è impostato su true, il valore di timestamp.initial è impostato su 0. Ciò significa che vengono recuperati dati con una colonna di marca temporale maggiore di 0 epoca.
      * Se backfill è impostato su false, il valore di timestamp.initial è impostato su -1. Ciò significa che vengono recuperati i dati con una colonna di marca temporale maggiore dell’ora corrente (l’ora in cui inizia l’acquisizione della sorgente).
   * La colonna timestamp deve essere formattata come tipo: `TIMESTAMP_LTZ` o `TIMESTAMP_NTZ`. Se la colonna timestamp è impostata su `TIMESTAMP_NTZ`, il fuso orario corrispondente in cui sono memorizzati i valori deve essere trasmesso tramite `timezoneValue` parametro. Se non specificato, il valore predefinito è UTC.
      * `TIMESTAMP_TZ` non può essere utilizzata in una colonna timestamp o in una mappatura.

## Passaggi successivi

Il seguente tutorial descrive i passaggi necessari per collegare [!DNL Snowflake] origine di streaming per l’Experience Platform tramite API:

* [Trasmetti dati da un [!DNL Snowflake] database di cui eseguire l’Experience Platform utilizzando l’API del servizio Flusso](../../tutorials/api/create/databases/snowflake-streaming.md)
