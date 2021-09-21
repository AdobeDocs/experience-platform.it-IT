---
keywords: Experience Platform;home;argomenti popolari;Snowflake
title: Creare una connessione sorgente di Snowflake nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente del Snowflake utilizzando l’interfaccia utente di Adobe Experience Platform.
source-git-commit: 2e717f33b487430220bd3bb7812558cde81d8852
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Snowflake] nell&#39;interfaccia utente

>[!NOTE]
>
> Il connettore [!DNL Snowflake] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL Snowflake] utilizzando l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Raccogli credenziali richieste

Per accedere al tuo account di Snowflake su [!DNL Platform], devi fornire il seguente valore di autenticazione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Account | L’account [!DNL Snowflake] a cui desideri connetterti a Platform. |
| Magazzino | Il warehouse [!DNL Snowflake] gestisce il processo di esecuzione della query per l&#39;applicazione. Ogni warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente al momento del trasferimento dei dati su Platform. |
| Database | Il [!DNL Snowflake] contiene i dati che desideri inserire nella piattaforma. |
| Nome utente | Nome utente dell&#39;account [!DNL Snowflake]. |
| Password | Password dell&#39;account utente [!DNL Snowflake]. |
| Stringa di connessione | Stringa di connessione utilizzata per connettersi all&#39;istanza [!DNL Snowflake]. Il pattern della stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

Per ulteriori informazioni su questi valori, consulta [questo documento di Snowflake](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Collegare l&#39;account di Snowflake

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Origini]. La schermata [!UICONTROL Catalogo] visualizza una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la categoria [!UICONTROL Database], selezionare **[!UICONTROL Snowflake]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Snowflake]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per collegare un account esistente, selezionare l&#39;account di Snowflake con cui si desidera connettersi, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali del Snowflake. Al termine, selezionare **[!UICONTROL Connetti]**, quindi lasciare che sia necessario un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/snowflake/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione all&#39;account di Snowflake. Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in [!DNL Platform]](../../dataflow/databases.md).
