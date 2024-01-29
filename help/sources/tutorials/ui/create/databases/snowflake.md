---
title: Creare una connessione sorgente del Snowflake nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente del Snowflake utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 2%

---

# Creare un [!DNL Snowflake] connessione sorgente nell’interfaccia utente

>[!IMPORTANT]
>
>Il [!DNL Snowflake] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial descrive i passaggi necessari per creare [!DNL Snowflake] connettore di origine che utilizza l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Per autenticare le credenziali, è necessario fornire i valori per le seguenti proprietà [!DNL Snowflake] sorgente.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

| Credenziali | Descrizione |
| ---------- | ----------- |
| Account | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, devi identificare in modo univoco un account tra diversi [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Ad esempio: `orgname-account_name`. Per ulteriori informazioni sui nomi degli account, leggere [!DNL Snowflake] documentazione su [identificatori dell’account](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Data warehouse | Il [!DNL Snowflake] warehouse gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni [!DNL Snowflake] il data warehouse è indipendente l’uno dall’altro e deve essere accessibile singolarmente quando si trasferiscono i dati su Platform. |
| Database | Il [!DNL Snowflake] Il database contiene i dati che desideri inserire in Platform. |
| Nome utente | Nome utente per [!DNL Snowflake] account. |
| Password | La password per [!DNL Snowflake] account utente. |
| Ruolo | Ruolo di controllo di accesso predefinito da utilizzare nel [!DNL Snowflake] sessione. Il ruolo deve essere esistente e già assegnato all&#39;utente specificato. Il ruolo predefinito è `PUBLIC`. |
| Stringa di connessione | Stringa di connessione utilizzata per la connessione al [!DNL Snowflake] dell&#39;istanza. Schema della stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autenticazione coppia di chiavi]

Per utilizzare l&#39;autenticazione con coppia di chiavi, è necessario generare una coppia di chiavi RSA a 2048 bit e quindi fornire i seguenti valori durante la creazione di un account per [!DNL Snowflake] sorgente.

| Credenziali | Descrizione |
| --- | --- |
| Account | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, devi identificare in modo univoco un account tra diversi [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Ad esempio: `orgname-account_name`. Per ulteriori informazioni sui nomi degli account, leggere [!DNL Snowflake] documentazione su [identificatori dell’account](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Nome utente | Il nome utente del [!DNL Snowflake] account. |
| Chiave privata | Il [!DNL Base64-]chiave privata codificata del tuo [!DNL Snowflake] account. Puoi generare chiavi private crittografate o non crittografate. Se utilizzi una chiave privata crittografata, devi anche fornire una passphrase di chiave privata durante l’autenticazione in base a Experienci Platform. |
| Passphrase chiave privata | La passphrase per chiave privata è un ulteriore livello di sicurezza da utilizzare per l&#39;autenticazione con una chiave privata crittografata. Se si utilizza una chiave privata non crittografata, non è necessario fornire la passphrase. |
| Database | Il [!DNL Snowflake] database contenente i dati da acquisire in Experienci Platform. |
| Data warehouse | Il [!DNL Snowflake] warehouse gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni [!DNL Snowflake] il data warehouse è indipendente l’uno dall’altro e deve essere accessibile singolarmente quando si trasferiscono i dati su Platform. |

Per ulteriori informazioni su questi valori, consulta [questo documento di Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

Per accedere all’account di Snowflake su Experienci Platform, devi fornire il seguente valore di autenticazione:

>[!NOTE]
>
>È necessario impostare `PREVENT_UNLOAD_TO_INLINE_URL` contrassegna per `FALSE` per consentire lo scaricamento dei dati dal [!DNL Snowflake] database di cui eseguire l&#39;Experience Platform.

## Connetti l’account di Snowflake

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Sotto [!UICONTROL Database] categoria, seleziona **[!UICONTROL Snowflake]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo origini con [!DNL Snowflake] evidenziato.](../../../../images/tutorials/create/snowflake/catalog.png)

Il **[!UICONTROL Connetti al Snowflake]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Snowflake] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![Interfaccia account esistente nel flusso di lavoro origini.](../../../../images/tutorials/create/snowflake/existing.png)

### Nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome e una descrizione facoltativa per il nuovo [!DNL Snowflake] account.

![La nuova interfaccia account nel flusso di lavoro origini.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Per utilizzare l’autenticazione con chiave account, specifica la stringa di connessione nel modulo di input, quindi seleziona **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione della chiave account.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Autenticazione coppia di chiavi]

Per utilizzare l’autenticazione con coppia di chiavi, specifica i valori per l’account, il nome utente, la chiave privata, la passphrase della chiave privata, il database e il warehouse, quindi seleziona **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione della coppia di chiavi account.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account di Snowflake. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
