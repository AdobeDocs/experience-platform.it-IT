---
keywords: Experience Platform;home;argomenti popolari;Teradata Vantage
title: Creare una connessione sorgente Teradata Vantage nell’interfaccia utente
description: Scopri come creare una connessione sorgente Teradata Vantage utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: 322b9aa5b817276eb4b56daf6e410944591c1d51
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# (Beta) Creare un [!DNL Teradata Vantage] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
> Il [!DNL Teradata Vantage] sorgente in versione beta. Consulta la [Panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questo tutorial descrive i passaggi necessari per creare [!DNL Teradata Vantage] connettore di origine che utilizza l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Platform:

* [Sorgenti](../../../../home.md): Experience Platform consente di acquisire dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Teradata Vantage] su Platform, è necessario fornire il seguente valore di autenticazione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Stringa di connessione | Una stringa di connessione è una stringa che fornisce informazioni su un&#39;origine dati e su come è possibile connettersi a essa. Schema della stringa di connessione per [!DNL Teradata Vantage] è `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Per ulteriori informazioni su come iniziare, consulta questa [[!DNL Teradata Vantage] documento](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Connetti [!DNL Teradata Vantage] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Sotto [!UICONTROL Database] categoria, seleziona **[!UICONTROL Teradata Vantage]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

Il **[!UICONTROL Connetti a Teradata Vantage]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Teradata Vantage] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/teradata/existing.png)

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL Teradata Vantage] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/teradata/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo account Teradata Vantage. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](../../dataflow/databases.md).
