---
keywords: Experience Platform;home;argomenti popolari;Snowflake
title: Creare una connessione sorgente di Snowflake nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente del Snowflake utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: ac7910c971fbedf3afebd87633f814d597260cae
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# Crea un [!DNL Snowflake] connessione sorgente nell’interfaccia utente

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Snowflake] connettore di origine tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Raccogli credenziali richieste

Per accedere al tuo account di Snowflake su [!DNL Platform], devi fornire il seguente valore di autenticazione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Account | Nome account completo associato al [!DNL Snowflake] conto. Un completo [!DNL Snowflake] il nome account include il nome account, la regione e la piattaforma cloud. Ad esempio, `cj12345.east-us-2.azure`. Per ulteriori informazioni sui nomi account, consulta questo [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Magazzino | La [!DNL Snowflake] warehouse gestisce il processo di esecuzione della query per l&#39;applicazione. Ogni [!DNL Snowflake] warehouse è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati in Platform. |
| Database | La [!DNL Snowflake] Il database contiene i dati che si desidera inserire in Platform. |
| Nome utente | Il nome utente per il [!DNL Snowflake] conto. |
| Password | La password per [!DNL Snowflake] account utente. |
| Stringa di connessione | Stringa di connessione utilizzata per la connessione al [!DNL Snowflake] istanza. Pattern di stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

Per ulteriori informazioni su questi valori, consulta [presente documento del Snowflake](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

## Collegare l&#39;account di Snowflake

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in questa schermata vengono visualizzate diverse sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la [!UICONTROL Database] categoria, seleziona **[!UICONTROL Snowflake]** quindi seleziona **[!UICONTROL Aggiungi dati]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

La **[!UICONTROL Connetti al Snowflake]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per collegare un account esistente, selezionare l&#39;account di Snowflake con cui si desidera connettersi, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali del Snowflake. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/snowflake/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione all&#39;account di Snowflake. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’immissione di dati in [!DNL Platform]](../../dataflow/databases.md).
