---
title: Creare una connessione sorgente Eloqua di Oracle utilizzando l’interfaccia utente di Experience Platform
description: Scopri come collegare Adobe Experience Platform ad Oracle Eloqua utilizzando l’interfaccia utente di Experience Platform.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---

# Crea una connessione di origine [!DNL Oracle Eloqua] tramite l&#39;interfaccia utente di Experience Platform

>[!WARNING]
>
>L&#39;origine [!DNL Oracle Eloqua] diventerà obsoleta alla fine di giugno 2025.

Questo tutorial illustra i passaggi per la creazione di una connessione di origine [!DNL Oracle Eloqua] tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Se disponi già di un account [!DNL Oracle Eloqua] autenticato su Experience Platform, puoi saltare il resto di questo documento e passare all&#39;esercitazione [creazione di un flusso di dati per portare i dati di automazione marketing in Experience Platform](../../dataflow/marketing-automation.md).

### Raccogli le credenziali richieste

Per connettere [!DNL Oracle Eloqua] ad Experience Platform, è necessario fornire i valori per le seguenti proprietà di autenticazione:

| Credenziali | Descrizione |
| --- | --- |
| Endpoint | Endpoint del server [!DNL Oracle Eloqua]. [!DNL Oracle Eloqua] supporta più data center. Per trovare l&#39;endpoint, accedere all&#39;[[!DNL Oracle Eloqua] interfaccia](https://login.eloqua.com) con le credenziali, quindi copiare la parte dell&#39;URL di base dall&#39;URL di reindirizzamento. Il formato del pattern URL è `xxx.xx.eloqua.com` e deve essere immesso senza `http` o `https`. |
| Nome utente | Il nome utente del server [!DNL Oracle Eloqua]. Il nome utente deve essere formattato come `siteName + \\ + username`, dove `siteName` è il nome società utilizzato per accedere a [!DNL Oracle Eloqua] e `username` è il nome utente. Ad esempio, il nome utente di accesso può essere: `Eloqua\Andy`. **Nota**: è necessario utilizzare una singola barra rovesciata (`\`) quando si utilizza l&#39;interfaccia utente di Experience Platform, perché questa aggiunge automaticamente una barra rovesciata aggiuntiva (`\`) quando si immette un nome utente. |
| Password | La password corrispondente al nome utente [!DNL Oracle Eloqua]. |

Per ulteriori informazioni sulle credenziali di autenticazione per [!DNL Oracle Eloqua], vedere la [[!DNL Oracle Eloqua] guida sull&#39;autenticazione](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Oracle Eloqua] ad Experience Platform.

## Connetti il tuo account [!DNL Oracle Eloqua]

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL Automazione marketing], seleziona **[!UICONTROL Oracle Eloqua]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account Oracle Eloqua]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Oracle Eloqua] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![esistente](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e i valori appropriati per le credenziali di [!DNL Oracle Eloqua]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai autenticato e creato una connessione sorgente tra il tuo account [!DNL Oracle Eloqua] e Experience Platform. Ora puoi continuare con l&#39;esercitazione successiva e [creare un flusso di dati per portare i dati di automazione marketing in Experience Platform](../../dataflow/marketing-automation.md).
