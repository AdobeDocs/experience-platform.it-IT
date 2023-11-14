---
title: Creare una connessione sorgente del Snowflake nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente del Snowflake utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 669b47753a9c9400f22aa81d08a4d25bb5e414c5
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 2%

---

# Creare un [!DNL Snowflake] connessione sorgente nell’interfaccia utente

>[!IMPORTANT]
>
>Il [!DNL Snowflake] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial descrive i passaggi necessari per creare [!DNL Snowflake] connettore di origine che utilizza l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Per accedere al tuo account di Snowflake su [!DNL Platform], è necessario fornire il seguente valore di autenticazione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Account | Il nome completo dell&#39;account associato al [!DNL Snowflake] account. Un sistema completo [!DNL Snowflake] il nome account include il nome account, l’area geografica e la piattaforma cloud. Ad esempio, `cj12345.east-us-2.azure`. Per ulteriori informazioni sui nomi degli account, consulta questa [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Data warehouse | Il [!DNL Snowflake] warehouse gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni [!DNL Snowflake] il data warehouse è indipendente l’uno dall’altro e deve essere accessibile singolarmente quando si trasferiscono i dati su Platform. |
| Database | Il [!DNL Snowflake] Il database contiene i dati che desideri inserire in Platform. |
| Nome utente | Nome utente per [!DNL Snowflake] account. |
| Password | La password per [!DNL Snowflake] account utente. |
| Ruolo | Ruolo di controllo di accesso predefinito da utilizzare nel [!DNL Snowflake] sessione. Il ruolo deve essere esistente e già assegnato all&#39;utente specificato. Il ruolo predefinito è `PUBLIC`. |
| Stringa di connessione | Stringa di connessione utilizzata per la connessione al [!DNL Snowflake] dell&#39;istanza. Schema della stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

Per ulteriori informazioni su questi valori, consulta [questo documento di Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!NOTE]
>
>È necessario impostare `PREVENT_UNLOAD_TO_INLINE_URL` contrassegna per `FALSE` per consentire lo scaricamento dei dati dal [!DNL Snowflake] database di cui eseguire l&#39;Experience Platform.

## Connetti l’account di Snowflake

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Sotto [!UICONTROL Database] categoria, seleziona **[!UICONTROL Snowflake]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

Il **[!UICONTROL Connetti al Snowflake]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per connettere un account esistente, seleziona l’account di Snowflake con cui desideri connetterti, quindi fai clic su **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali di Snowflake. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/snowflake/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account di Snowflake. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
