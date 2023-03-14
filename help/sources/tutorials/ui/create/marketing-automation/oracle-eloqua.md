---
title: Creare una connessione sorgente Eloqua di Oracle utilizzando l’interfaccia utente di Platform
description: Scopri come collegare Adobe Experience Platform ad Oracle Eloqua utilizzando l’interfaccia utente di Platform.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# Creare un [!DNL Oracle Eloqua] connessione sorgente tramite l’interfaccia utente di Platform

Questo tutorial descrive i passaggi necessari per creare [!DNL Oracle Eloqua] connessione sorgente mediante l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Platform:

* [Sorgenti](../../../../home.md): Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Se disponi già di un [!DNL Oracle Eloqua] su Platform, puoi saltare il resto del documento e passare all’esercitazione su [creazione di un flusso di dati per portare i dati di automazione marketing su Platform](../../dataflow/marketing-automation.md).

### Raccogli le credenziali richieste

Per connettersi [!DNL Oracle Eloqua] In Platform, devi fornire i valori per le seguenti proprietà di autenticazione:

| Credenziali | Descrizione |
| --- | --- |
| Endpoint | Endpoint del tuo [!DNL Oracle Eloqua] server. [!DNL Oracle Eloqua] supporta più data center. Per trovare l’endpoint, accedi a [[!DNL Oracle Eloqua] Interfaccia](https://login.eloqua.com) con le tue credenziali, quindi copia la parte dell’URL di base dall’URL di reindirizzamento. Il formato del pattern URL è `xxx.xx.eloqua.com` e devono essere immessi senza `http` o `https`. |
| Nome utente | Il nome utente del [!DNL Oracle Eloqua] server. Il nome utente deve essere formattato come `siteName + \\ + username`, dove `siteName` è il nome della società a cui accedi [!DNL Oracle Eloqua] e `username` è il tuo nome utente. Ad esempio, il nome utente per l’accesso può essere: `Eloqua\Andy`. **Nota**: utilizza una singola barra rovesciata (`\`)quando si utilizza l’interfaccia utente di, perché l’interfaccia utente di Experience Platform aggiunge automaticamente una barra rovesciata aggiuntiva (`\`) quando si immette un nome utente. |
| Password | La password corrispondente al tuo [!DNL Oracle Eloqua] nome utente. |

Per ulteriori informazioni sulle credenziali di autenticazione per [!DNL Oracle Eloqua], vedere [[!DNL Oracle Eloqua] guida all’autenticazione](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Oracle Eloqua] da un account a Platform.

## Connetti [!DNL Oracle Eloqua] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL Automazione del marketing] categoria, seleziona **[!UICONTROL Eloqua Oracle]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

Il **[!UICONTROL Connetti account Oracle Eloqua]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Oracle Eloqua] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome, una descrizione facoltativa e i valori appropriati per il tuo [!DNL Oracle Eloqua] credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai autenticato e creato una connessione sorgente tra [!DNL Oracle Eloqua] e Platform. Ora puoi continuare con l’esercitazione successiva e [creare un flusso di dati per portare i dati di automazione marketing su Platform](../../dataflow/marketing-automation.md).
