---
title: Panoramica del connettore Source di streaming Snowflake
description: Scopri come creare una connessione di origine e un flusso di dati per acquisire i dati in streaming dall’istanza Snowflake a Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 3%

---

# [!DNL Snowflake] origine streaming

>[!IMPORTANT]
>
>* L&#39;origine di streaming [!DNL Snowflake] è disponibile nell&#39;API per gli utenti che hanno acquistato Real-Time CDP Ultimate.
>
>* È ora possibile utilizzare l&#39;origine di streaming [!DNL Snowflake] durante l&#39;esecuzione di Adobe Experience Platform su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../landing/multi-cloud.md).

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce il supporto per lo streaming dei dati da un database [!DNL Snowflake].

## Informazioni sull&#39;origine di streaming [!DNL Snowflake]

L&#39;origine di flusso [!DNL Snowflake] funziona caricando i dati eseguendo periodicamente una query SQL e creando un record di output per ogni riga nel set risultante.

Utilizzando [!DNL Kafka Connect], l&#39;origine di streaming [!DNL Snowflake] tiene traccia dell&#39;ultimo record ricevuto da ogni tabella, in modo che possa iniziare nella posizione corretta per l&#39;iterazione successiva. L’origine utilizza questa funzionalità per filtrare i dati e ottenere solo le righe aggiornate da una tabella su ogni iterazione.

## Prerequisiti

La sezione seguente descrive i passaggi preliminari da completare prima di poter inviare dati dal database [!DNL Snowflake] ad Experience Platform:

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform](../../ip-address-allow-list.md).

La documentazione seguente fornisce informazioni su come connettere [!DNL Amazon Redshift] ad Experience Platform tramite API o tramite l&#39;interfaccia utente:

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Snowflake], è necessario fornire le seguenti proprietà di connessione:

>[!BEGINTABS]

>[!TAB Autenticazione di base]

| Credenziali | Descrizione |
| --- | --- |
| `account` | L&#39;identificatore account completo (nome account o localizzatore account) dell&#39;account [!DNL Snowflake] aggiunto al suffisso `snowflakecomputing.com`. L’identificatore dell’account può essere in diversi formati: <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (esempio: `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (esempio: `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (esempio: `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Per ulteriori informazioni, leggere [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati ad Experience Platform. |
| `database` | Il database [!DNL Snowflake] contiene i dati che si desidera inserire nell&#39;Experience Platform. |
| `username` | Nome utente per l&#39;account [!DNL Snowflake]. |
| `password` | Password per l&#39;account utente [!DNL Snowflake]. |
| `role` | (Facoltativo) Ruolo personalizzato che può essere fornito a un utente, per una determinata connessione. Se non specificato, il valore predefinito è `public`. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL Snowflake] è `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

>[!TAB Autenticazione coppia di chiavi]

Per utilizzare l&#39;autenticazione con coppia di chiavi, è necessario generare una coppia di chiavi RSA a 2048 bit e quindi fornire i seguenti valori durante la creazione di un account per l&#39;origine [!DNL Snowflake].

| Credenziali | Descrizione |
| --- | --- |
| `account` | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, è necessario identificare in modo univoco un account tra diverse [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Esempio: `orgname-account_name`. Per ulteriori informazioni, consulta la guida in [recupero dell&#39;identificatore dell&#39;account [!DNL Snowflake] &#x200B;](./snowflake.md#retrieve-your-account-identifier). Per ulteriori informazioni, consulta la [[!DNL Snowflake] documentazione](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Il nome utente dell&#39;account [!DNL Snowflake]. |
| `privateKey` | La chiave privata con codifica [!DNL Base64-] del tuo account [!DNL Snowflake]. Puoi generare chiavi private crittografate o non crittografate. Se utilizzi una chiave privata crittografata, devi fornire anche una passphrase di chiave privata durante l’autenticazione in Experience Platform. Per ulteriori informazioni, consulta la guida in [recupero della tua [!DNL Snowflake] chiave privata](./snowflake.md). |
| `passphrase` | La passphrase è un ulteriore livello di sicurezza da utilizzare per l&#39;autenticazione con una chiave privata crittografata. Se si utilizza una chiave privata non crittografata, non è necessario fornire la passphrase. |
| `database` | Il database [!DNL Snowflake] che contiene i dati da acquisire in Experience Platform. |
| `warehouse` | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati ad Experience Platform. |

Per ulteriori informazioni su questi valori, fare riferimento alla [[!DNL Snowflake] guida all&#39;autenticazione con coppia di chiavi](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Recupera l’identificatore dell’account {#retrieve-your-account-identifier}

Per autenticare l&#39;istanza [!DNL Snowflake] con Experience Platform, è necessario ottenere l&#39;identificatore dell&#39;account dal dashboard dell&#39;interfaccia utente [!DNL Snowflake].

Per trovare l’identificatore dell’account, segui la procedura riportata di seguito:

* Accedi al tuo account nel [[!DNL Snowflake] dashboard dell&#39;interfaccia utente dell&#39;applicazione](https://app.snowflake.com/).
* Nel menu di navigazione a sinistra, seleziona **[!DNL Accounts]**, seguito da **[!DNL Active Accounts]** dall&#39;intestazione.
* Quindi, seleziona l’icona delle informazioni, quindi fai clic sul nome di dominio dell’URL corrente e copialo.

### Recupera la chiave privata {#retrieve-your-private-key}

Se si prevede di utilizzare l&#39;autenticazione con coppia di chiavi per la connessione [!DNL Snowflake], è necessario generare una chiave privata prima di connettersi ad Experience Platform.

>[!BEGINTABS]

>[!TAB Crea una chiave privata crittografata]

Per generare la chiave privata [!DNL Snowflake] crittografata, eseguire il comando seguente sul terminale:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

In caso di esito positivo, dovresti ricevere la tua chiave privata in formato PEM.

```shell
|-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
|-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB Crea una chiave privata non crittografata]

Per generare la chiave privata [!DNL Snowflake] non crittografata, eseguire il comando seguente sul terminale:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

In caso di esito positivo, dovresti ricevere la tua chiave privata in formato PEM.

```shell
|-----BEGIN PRIVATE KEY-----
MIIE6T...
|-----END PRIVATE KEY-----
```

>[!ENDTABS]

Dopo aver generato la chiave privata, codificarla direttamente in [!DNL Base64] senza apportare alcuna modifica al formato o al contenuto. Prima di eseguire la codifica, accertati che non vi siano spazi o righe vuote (comprese le nuove righe finali) alla fine della chiave privata.

### Verifica configurazioni

Prima di poter creare una connessione di origine per i dati di [!DNL Snowflake], è necessario verificare che siano soddisfatte le seguenti configurazioni:

* Il magazzino predefinito assegnato a un determinato utente deve essere uguale al magazzino immesso durante l&#39;autenticazione in Experience Platform.
* Il ruolo predefinito assegnato a un determinato utente deve avere accesso allo stesso database inserito durante l’autenticazione in Experience Platform.

Per verificare il ruolo e il magazzino:

* Selezionare **[!DNL Admin]** nel menu di navigazione a sinistra, quindi selezionare **[!DNL Users & Roles]**.
* Selezionare l&#39;utente appropriato, quindi selezionare i puntini di sospensione (`...`) nell&#39;angolo superiore destro.
* Nella finestra [!DNL Edit user] visualizzata, passa a [!DNL Default Role] per visualizzare il ruolo associato all&#39;utente specificato.
* Nella stessa finestra passare a [!DNL Default Warehouse] per visualizzare il magazzino associato all&#39;utente specificato.

Una volta codificata correttamente, è possibile utilizzare la chiave privata con codifica [!DNL Base64] in Experience Platform per autenticare l&#39;account [!DNL Snowflake].

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

## Convertire i campi ora Unix in data

[!DNL Snowflake Streaming] analizza e scrive i campi `DATE` come il numero di giorni dall&#39;epoca Unix (1970-01-01). Ad esempio, un valore `DATE` di 0 significa 1 gennaio 1970, mentre un valore di 1 significa 2 gennaio 1970. Pertanto, durante la preparazione del file per la creazione di mapping nell&#39;origine [!DNL Snowflake Streaming], assicurarsi che la colonna `DATE` sia rappresentata come numero intero.

È possibile utilizzare le [funzioni data e ora della preparazione dati](../../../data-prep/functions.md#date-and-time-functions) per convertire l&#39;ora Unix in campi data che possono essere acquisiti in Experience Platform. Ad esempio:

```shell
dformat({DATE_COLUMN} * 86400000, "yyyy-MM-dd")
```

In questa funzione:

* `{DATE_COLUMN}` è la colonna della data contenente il numero intero del giorno dell&#39;epoca.
* Moltiplicando per 86400000 i giorni epoca vengono convertiti in millisecondi.
* &#39;gg-MM-aaaa&#39; specifica il formato della data desiderato.

Questa conversione garantisce che la data sia rappresentata correttamente nel set di dati.


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

>[!NOTE]
>
>Dopo aver creato o aggiornato un flusso di dati in streaming, è necessaria una breve pausa di 5 minuti nell’acquisizione dei dati per evitare potenziali istanze di perdita o perdita di dati.

Il seguente tutorial illustra i passaggi necessari per collegare l&#39;origine di streaming [!DNL Snowflake] ad Experience Platform utilizzando l&#39;API:

* [Trasmetti dati da un database  [!DNL Snowflake]  ad Experience Platform utilizzando l&#39;API del servizio Flusso](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Trasmetti dati da un database  [!DNL Snowflake]  ad Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente di Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
