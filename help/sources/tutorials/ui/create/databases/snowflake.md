---
title: Creare una connessione Source di Snowflake nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente del Snowflake utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: d89e0c81bd250e41a863b8b28d358cc6ddea1c37
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 4%

---

# Crea una connessione sorgente [!DNL Snowflake] nell&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL Snowflake] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial illustra i passaggi per la creazione di un connettore di origine [!DNL Snowflake] tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Per autenticare l&#39;origine [!DNL Snowflake], è necessario fornire i valori per le seguenti proprietà delle credenziali.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

| Credenziali | Descrizione |
| ---------- | ----------- |
| Account | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, è necessario identificare in modo univoco un account tra diverse [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Esempio: `orgname-account_name`. Per ulteriori informazioni, consulta la guida in [recupero dell&#39;identificatore dell&#39;account [!DNL Snowflake] ](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier). Per ulteriori informazioni, consulta la [[!DNL Snowflake] documentazione](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Data warehouse | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati a Platform. |
| Database | Il database [!DNL Snowflake] contiene i dati che si desidera inserire nella piattaforma. |
| Nome utente | Nome utente per l&#39;account [!DNL Snowflake]. |
| Password | Password per l&#39;account utente [!DNL Snowflake]. |
| Ruolo | Ruolo di controllo di accesso predefinito da utilizzare nella sessione [!DNL Snowflake]. Il ruolo deve essere esistente e già assegnato all&#39;utente specificato. Il ruolo predefinito è `PUBLIC`. |
| Stringa di connessione | Stringa di connessione utilizzata per connettersi all&#39;istanza [!DNL Snowflake]. Il modello di stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticazione coppia di chiavi]

Per utilizzare l&#39;autenticazione con coppia di chiavi, è necessario generare una coppia di chiavi RSA a 2048 bit e quindi fornire i seguenti valori durante la creazione di un account per l&#39;origine [!DNL Snowflake].

| Credenziali | Descrizione |
| --- | --- |
| Account | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, è necessario identificare in modo univoco un account tra diverse [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Esempio: `orgname-account_name`. Per ulteriori informazioni, consulta la guida in [recupero dell&#39;identificatore dell&#39;account [!DNL Snowflake] ](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier). Per ulteriori informazioni, consulta la [[!DNL Snowflake] documentazione](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Nome utente | Il nome utente dell&#39;account [!DNL Snowflake]. |
| Chiave privata | La chiave privata con codifica [!DNL Base64-] del tuo account [!DNL Snowflake]. Puoi generare chiavi private crittografate o non crittografate. Se utilizzi una chiave privata crittografata, devi anche fornire una passphrase di chiave privata durante l’autenticazione in base a Experience Platform. Per ulteriori informazioni, consulta la guida in [recupero della tua [!DNL Snowflake] chiave privata](../../../../connectors/databases/snowflake.md). |
| Passphrase chiave privata | La passphrase per chiave privata è un ulteriore livello di sicurezza da utilizzare per l&#39;autenticazione con una chiave privata crittografata. Se si utilizza una chiave privata non crittografata, non è necessario fornire la passphrase. |
| Database | Il database [!DNL Snowflake] che contiene i dati da acquisire per l&#39;Experience Platform. |
| Data warehouse | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati a Platform. |

Per ulteriori informazioni su questi valori, fare riferimento a [questo documento di Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>È necessario impostare il flag `PREVENT_UNLOAD_TO_INLINE_URL` su `FALSE` per consentire lo scaricamento dei dati dal database [!DNL Snowflake] su Experience Platform.

## Connetti l’account di Snowflake

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini].

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Nella categoria [!UICONTROL Database], selezionare **[!UICONTROL Snowflake]**, quindi **[!UICONTROL Aggiungi dati]**.

![Catalogo origini con [!DNL Snowflake] evidenziato.](../../../../images/tutorials/create/snowflake/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti al Snowflake]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, selezionare l&#39;account [!DNL Snowflake] con cui connettersi, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![Interfaccia account esistente nel flusso di lavoro di origine.](../../../../images/tutorials/create/snowflake/existing.png)

### Nuovo account

Per creare un nuovo account, selezionare **[!UICONTROL Nuovo account]**, quindi specificare un nome e una descrizione facoltativa per il nuovo account [!DNL Snowflake].

![Nuova interfaccia account nel flusso di lavoro di origine.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Per utilizzare l&#39;autenticazione della chiave account, specificare la stringa di connessione nel modulo di input, quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione della chiave dell&#39;account.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Autenticazione coppia di chiavi]

Per utilizzare l&#39;autenticazione con coppia di chiavi, specificare i valori per l&#39;account, il nome utente, la chiave privata, la passphrase della chiave privata, il database e il warehouse, quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione della coppia di chiavi dell&#39;account.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account di Snowflake. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
