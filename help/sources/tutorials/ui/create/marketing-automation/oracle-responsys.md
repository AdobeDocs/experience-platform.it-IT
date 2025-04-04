---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;oracle;
title: (Beta) Creazione di una connessione all’origine Oracle Responsys tramite l’interfaccia utente di Experience Platform
description: Scopri come collegare Adobe Experience Platform ad Oracle Responsys utilizzando l’interfaccia utente di Experience Platform.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# (Beta) Crea una connessione di origine [!DNL Oracle Responsys] tramite l&#39;interfaccia utente di Experience Platform

>[!NOTE]
>
>L&#39;origine [!DNL Oracle Responsys] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../../../home.md#terms-and-conditions).

Questo tutorial illustra i passaggi necessari per creare una connessione di origine [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Se disponi già di un account [!DNL Oracle Responsys] autenticato su Experience Platform, puoi saltare il resto di questo documento e passare all&#39;esercitazione [creazione di un flusso di dati per portare i dati di automazione marketing in Experience Platform](../../dataflow/marketing-automation.md).

### Raccogli le credenziali richieste

Per connettere [!DNL Oracle Responsys] ad Experience Platform, è necessario fornire i valori per le seguenti proprietà di autenticazione:

| Credenziali | Descrizione |
| --- | --- |
| Endpoint | L&#39;URL dell&#39;endpoint di autenticazione REST dell&#39;istanza [!DNL Oracle Responsys]. |
| ID client | ID client dell&#39;istanza [!DNL Oracle Responsys]. |
| Segreto client | Il segreto client dell&#39;istanza [!DNL Oracle Responsys]. |

Per ulteriori informazioni sulle credenziali di autenticazione per [!DNL Oracle Responsys], vedere la [[!DNL Oracle Responsys] guida sull&#39;autenticazione](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Oracle Responsys] ad Experience Platform.

## Connetti il tuo account [!DNL Oracle Responsys]

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL Marketing automation], selezionare **[!UICONTROL Oracle Responsys]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Catalogo origini Adobe Experience Platform con origine Oracle Responsys evidenziata.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account Oracle Responsys]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Oracle Responsys] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![Schermata di autenticazione dell&#39;account esistente per Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nuovo account

Per creare un nuovo account, selezionare **[!UICONTROL Nuovo account]**, quindi specificare un nome, una descrizione facoltativa e i valori appropriati per le credenziali di [!DNL Oracle Responsys]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova schermata di autenticazione dell&#39;account per Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai autenticato e creato una connessione sorgente tra il tuo account [!DNL Oracle Responsys] e Experience Platform. Ora puoi continuare con l&#39;esercitazione successiva e [creare un flusso di dati per portare i dati di automazione marketing in Experience Platform](../../dataflow/marketing-automation.md).
