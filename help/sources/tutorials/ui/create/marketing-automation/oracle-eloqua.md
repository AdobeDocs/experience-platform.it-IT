---
title: Creare una connessione sorgente Eloqua di Oracle utilizzando l’interfaccia utente di Platform
description: Scopri come collegare Adobe Experience Platform ad Oracle Eloqua utilizzando l’interfaccia utente di Platform.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# Crea una connessione di origine [!DNL Oracle Eloqua] tramite l&#39;interfaccia utente di Platform

>[!WARNING]
>
>L&#39;origine [!DNL Oracle Eloqua] diventerà obsoleta alla fine di maggio 2025.

Questo tutorial illustra i passaggi per la creazione di una connessione di origine [!DNL Oracle Eloqua] tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Platform:

* [Origini](../../../../home.md): Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Se disponi già di un account [!DNL Oracle Eloqua] autenticato su Platform, puoi saltare il resto di questo documento e passare all&#39;esercitazione [creazione di un flusso di dati per portare i dati di automazione marketing su Platform](../../dataflow/marketing-automation.md).

### Raccogli le credenziali richieste

Per connettere [!DNL Oracle Eloqua] a Platform, è necessario fornire i valori per le seguenti proprietà di autenticazione:

| Credenziali | Descrizione |
| --- | --- |
| Endpoint | Endpoint del server [!DNL Oracle Eloqua]. [!DNL Oracle Eloqua] supporta più data center. Per trovare l&#39;endpoint, accedere all&#39;[[!DNL Oracle Eloqua] interfaccia](https://login.eloqua.com) con le credenziali, quindi copiare la parte dell&#39;URL di base dall&#39;URL di reindirizzamento. Il formato del pattern URL è `xxx.xx.eloqua.com` e deve essere immesso senza `http` o `https`. |
| Nome utente | Il nome utente del server [!DNL Oracle Eloqua]. Il nome utente deve essere formattato come `siteName + \\ + username`, dove `siteName` è il nome società utilizzato per accedere a [!DNL Oracle Eloqua] e `username` è il nome utente. Ad esempio, il nome utente di accesso può essere: `Eloqua\Andy`. **Nota**: è necessario utilizzare una singola barra rovesciata (`\`) quando si utilizza l&#39;interfaccia utente di Experience Platform, poiché questa aggiunge automaticamente una barra rovesciata aggiuntiva (`\`) quando si immette un nome utente. |
| Password | La password corrispondente al nome utente [!DNL Oracle Eloqua]. |

Per ulteriori informazioni sulle credenziali di autenticazione per [!DNL Oracle Eloqua], vedere la [[!DNL Oracle Eloqua] guida sull&#39;autenticazione](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Oracle Eloqua] a Platform.

## Connetti il tuo account [!DNL Oracle Eloqua]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL Marketing automation], selezionare **[!UICONTROL Oracle Eloqua]**, quindi **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect Oracle Eloqua account]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Oracle Eloqua] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![esistente](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e i valori appropriati per le credenziali di [!DNL Oracle Eloqua]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai autenticato e creato una connessione di origine tra l&#39;account [!DNL Oracle Eloqua] e Platform. Ora puoi continuare con l&#39;esercitazione successiva e [creare un flusso di dati per portare i dati di automazione marketing in Platform](../../dataflow/marketing-automation.md).
