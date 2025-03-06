---
title: Connettere Snowflake Ad Experience Platform Tramite L’Interfaccia Utente
type: Tutorial
description: Scopri come creare una connessione sorgente Snowflake utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: cde31b692e9a11b15cf91a505133f75f69604cba
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 3%

---

# Connetti [!DNL Snowflake] ad Experience Platform tramite l&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL Snowflake] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.

Leggere questa guida per scoprire come collegare l&#39;account [!DNL Snowflake] a Adobe Experience Platform utilizzando l&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

>[!NOTE]
>
>Impostare il flag `PREVENT_UNLOAD_TO_INLINE_URL` su `FALSE` per consentire lo scaricamento dei dati dal database [!DNL Snowflake] in Experience Platform.

## Navigare nel catalogo delle origini {#navigate}

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Selezionare **[!DNL Snowflake]** nella categoria *[!UICONTROL Database]*, quindi selezionare **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con la scheda Snowflake selezionata..](../../../../images/tutorials/create/snowflake/catalog.png)

## Usa un account esistente {#existing}

Successivamente, viene visualizzato il passaggio di autenticazione del flusso di lavoro sorgenti. In questo caso, puoi utilizzare un account esistente o crearne uno nuovo.

Per utilizzare un account esistente, selezionare l&#39;account [!DNL Snowflake] con cui connettersi, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![Interfaccia account esistente nel flusso di lavoro di origine.](../../../../images/tutorials/create/snowflake/existing.png)

## Crea un nuovo account {#create}

Se non disponi di un account esistente, devi crearne uno nuovo fornendo le credenziali di autenticazione necessarie che corrispondono all’origine.

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi specifica un nome e, facoltativamente, aggiungi una descrizione per l&#39;account.

### Connettersi ad Experience Platform in Azure {#azure}

È possibile connettere l&#39;account [!DNL Snowflake] ad Experience Platform su Azure utilizzando l&#39;autenticazione con chiave dell&#39;account o l&#39;autenticazione con coppia di chiavi.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Per utilizzare l&#39;autenticazione della chiave dell&#39;account, selezionare **[!UICONTROL Autenticazione della chiave dell&#39;account]**, specificare la stringa di connessione nel modulo di input, quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione della chiave dell&#39;account.](../../../../images/tutorials/create/snowflake/account-key-auth.png)

| Credenziali | Descrizione |
| --- | --- |
| Account | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, è necessario identificare in modo univoco un account tra diverse [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Esempio: `orgname-account_name`. Per ulteriori informazioni, consulta la guida in [recupero dell&#39;identificatore dell&#39;account [!DNL Snowflake] ](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier). Per ulteriori informazioni, consulta la [[!DNL Snowflake] documentazione](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Data warehouse | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati a Platform. |
| Database | Il database [!DNL Snowflake] contiene i dati che si desidera inserire nella piattaforma. |
| Nome utente | Nome utente per l&#39;account [!DNL Snowflake]. |
| Password | Password per l&#39;account utente [!DNL Snowflake]. |
| Ruolo | Ruolo di controllo di accesso predefinito da utilizzare nella sessione [!DNL Snowflake]. Il ruolo deve essere esistente e già assegnato all&#39;utente specificato. Il ruolo predefinito è `PUBLIC`. |
| Stringa di connessione | Stringa di connessione utilizzata per connettersi all&#39;istanza [!DNL Snowflake]. Il modello di stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticazione coppia di chiavi]

Per utilizzare l&#39;autenticazione con coppia di chiavi, selezionare **[!UICONTROL Autenticazione coppia di chiavi]**, specificare i valori per l&#39;account, il nome utente, la chiave privata, la passphrase della chiave privata, il database e il warehouse, quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione della coppia di chiavi dell&#39;account.](../../../../images/tutorials/create/snowflake/key-pair-auth.png)

Con l&#39;autenticazione con coppia di chiavi, è necessario generare una coppia di chiavi RSA a 2048 bit e quindi fornire i seguenti valori durante la creazione di un account per l&#39;origine [!DNL Snowflake].

| Credenziali | Descrizione |
| --- | --- |
| Account | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, è necessario identificare in modo univoco un account tra diverse [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Esempio: `orgname-account_name`. Per ulteriori informazioni, consulta la guida in [recupero dell&#39;identificatore dell&#39;account [!DNL Snowflake] ](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier). Per ulteriori informazioni, consulta la [[!DNL Snowflake] documentazione](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Nome utente | Il nome utente dell&#39;account [!DNL Snowflake]. |
| Chiave privata | La chiave privata con codifica [!DNL Base64-] del tuo account [!DNL Snowflake]. Puoi generare chiavi private crittografate o non crittografate. Se utilizzi una chiave privata crittografata, devi fornire anche una passphrase di chiave privata durante l’autenticazione in Experience Platform. Per ulteriori informazioni, consulta la guida in [recupero della tua [!DNL Snowflake] chiave privata](../../../../connectors/databases/snowflake.md). |
| Passphrase chiave privata | La passphrase per chiave privata è un ulteriore livello di sicurezza da utilizzare per l&#39;autenticazione con una chiave privata crittografata. Se si utilizza una chiave privata non crittografata, non è necessario fornire la passphrase. |
| Database | Il database [!DNL Snowflake] che contiene i dati da acquisire in Experience Platform. |
| Data warehouse | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati a Platform. |

Per ulteriori informazioni su questi valori, fare riferimento a [questo documento di Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Connettersi ad Experience Platform su AWS {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per creare un nuovo account [!DNL Snowflake] e connettersi ad Experience Platform su AWS, verificare di essere in una sandbox VA6 e quindi fornire le credenziali necessarie per l&#39;autenticazione.

![Il nuovo passaggio dell&#39;account nel flusso di lavoro delle origini da cui è possibile connettere Snowflake ad Experience Platform su AWS.](../../../../images/tutorials/create/snowflake/aws-auth.png)

| Credenziali | Descrizione |
| --- | --- |
| Host | L&#39;URL host al quale il tuo account [!DNL Snowflake] si connette. |
| Porta | Numero di porta utilizzato da [!DNL Snowflake] per la connessione a un server tramite Internet. |
| Nome utente | Il nome utente associato al tuo account [!DNL Snowflake]. |
| Password | La password associata al tuo account [!DNL Snowflake]. |
| Database | Il database [!DNL Snowflake] da cui verranno estratti i dati. |
| Schema | Il nome dello schema associato al database [!DNL Snowflake]. È necessario assicurarsi che anche l&#39;utente a cui si desidera concedere l&#39;accesso al database abbia accesso a questo schema. |
| Data warehouse | Il data warehouse [!DNL Snowflake] in uso. |

### Ignora anteprima dei dati di esempio {#skip-preview-of-sample-data}

Durante il passaggio di selezione dei dati, potrebbe verificarsi un timeout durante l’acquisizione di tabelle o file di dati di grandi dimensioni. Puoi saltare l’anteprima dei dati per evitare il timeout e visualizzare comunque lo schema, anche senza dati di esempio. Per ignorare l&#39;anteprima dei dati, abilitare l&#39;interruttore **[!UICONTROL Ignora anteprima dati di esempio]**.

Il resto del flusso di lavoro rimarrà invariato. L’unica avvertenza è che ignorare l’anteprima dei dati potrebbe impedire la convalida automatica dei campi calcolati e obbligatori durante il passaggio di mappatura, per cui dovrai convalidarli manualmente durante la mappatura.

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account Snowflake. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
