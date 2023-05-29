---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;oracle;
title: (Beta) Creazione di una connessione di origine Responsys Oracle tramite l’interfaccia utente di Platform
description: Scopri come collegare Adobe Experience Platform ad Oracle Responsys utilizzando l’interfaccia utente di Platform.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# (Beta) Creare un [!DNL Oracle Responsys] connessione sorgente tramite l’interfaccia utente di Platform

>[!NOTE]
>
>Il [!DNL Oracle Responsys] sorgente in versione beta. Consulta la [Panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di connettori con etichetta beta.

Questo tutorial illustra i passaggi necessari per creare [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) connessione sorgente mediante l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Platform:

* [Sorgenti](../../../../home.md): Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Se disponi già di un [!DNL Oracle Responsys] su Platform, puoi saltare il resto del documento e passare all’esercitazione su [creazione di un flusso di dati per portare i dati di automazione marketing su Platform](../../dataflow/marketing-automation.md).

### Raccogli le credenziali richieste

Per connettersi [!DNL Oracle Responsys] In Platform, devi fornire i valori per le seguenti proprietà di autenticazione:

| Credenziali | Descrizione |
| --- | --- |
| Endpoint | L’URL dell’endpoint di autenticazione REST del [!DNL Oracle Responsys] dell&#39;istanza. |
| ID client | L’ID client del tuo [!DNL Oracle Responsys] dell&#39;istanza. |
| Segreto client | Il segreto client del tuo [!DNL Oracle Responsys] dell&#39;istanza. |

Per ulteriori informazioni sulle credenziali di autenticazione per [!DNL Oracle Responsys], vedere [[!DNL Oracle Responsys] guida all’autenticazione](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Oracle Responsys] da un account a Platform.

## Connetti [!DNL Oracle Responsys] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL Automazione del marketing] categoria, seleziona **[!UICONTROL Responsys Oracle]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini di Adobe Experience Platform con l&#39;Oracle Origine Responsys evidenziato.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

Il **[!UICONTROL Connetti account Oracle Responsys]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Oracle Responsys] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![La schermata di autenticazione dell’account esistente, ad Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome, una descrizione facoltativa e i valori appropriati per il tuo [!DNL Oracle Responsys] credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova schermata di autenticazione dell’account, ad Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai autenticato e creato una connessione sorgente tra [!DNL Oracle Responsys] e Platform. Ora puoi continuare con l’esercitazione successiva e [creare un flusso di dati per portare i dati di automazione marketing su Platform](../../dataflow/marketing-automation.md).
