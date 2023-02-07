---
title: Creare una connessione sorgente Oracle Eloqua tramite l’interfaccia utente di Platform
description: Scopri come collegare Adobe Experience Platform ad Oracle Eloqua tramite l’interfaccia utente di Platform.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# Crea un [!DNL Oracle Eloqua] connessione sorgente tramite l’interfaccia utente di Platform

Questa esercitazione descrive i passaggi necessari per creare un [!DNL Oracle Eloqua] connessione di origine tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Platform:

* [Origini](../../../../home.md): Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Se disponi già di un&#39;autenticazione [!DNL Oracle Eloqua] account su Platform, puoi saltare il resto del documento e procedere all’esercitazione su [creazione di un flusso di dati per trasferire i dati di automazione del marketing a Platform](../../dataflow/marketing-automation.md).

### Raccogli credenziali richieste

Per connettersi [!DNL Oracle Eloqua] su Platform, devi fornire valori per le seguenti proprietà di autenticazione:

| Credenziali | Descrizione |
| --- | --- |
| Endpoint | L&#39;endpoint della [!DNL Oracle Eloqua] server. [!DNL Oracle Eloqua] supporta più data center. Per trovare l&#39;endpoint, accedi al [[!DNL Oracle Eloqua] interfaccia](https://login.eloqua.com) con le tue credenziali, quindi copia la porzione dell’URL di base dall’URL di reindirizzamento. Il formato del pattern URL è `xxx.xx.eloqua.com` e deve essere inserito senza `http` o `https`. |
| Nome utente | Il nome utente del tuo [!DNL Oracle Eloqua] server. Il nome utente deve essere formattato come `siteName + \\ + username`, dove `siteName` è il nome della società a cui hai effettuato l’accesso [!DNL Oracle Eloqua] e `username` è il tuo nome utente. Ad esempio, il nome utente per l’accesso può essere: `Eloqua\Andy`. **Nota**: È necessario utilizzare una singola barra rovesciata (`\`)quando utilizzi l’interfaccia utente perché l’interfaccia utente di Experience Platform aggiunge automaticamente una barra rovesciata aggiuntiva (`\`) quando si immette un nome utente. |
| Password | La password corrispondente alla [!DNL Oracle Eloqua] nome utente. |

Per ulteriori informazioni sulle credenziali di autenticazione per [!DNL Oracle Eloqua], vedi [[!DNL Oracle Eloqua] guida all’autenticazione](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Oracle Eloqua] a Platform.

## Collega il tuo [!DNL Oracle Eloqua] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la [!UICONTROL Automazione del marketing] categoria, seleziona **[!UICONTROL Oracle Eloqua]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

La **[!UICONTROL Connetti account Eloqua Oracle]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Oracle Eloqua] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e i valori appropriati per il tuo [!DNL Oracle Eloqua] credenziali. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai autenticato e creato una connessione sorgente tra [!DNL Oracle Eloqua] account e piattaforma. Ora puoi passare all’esercitazione successiva e [creare un flusso di dati per trasferire i dati di automazione del marketing a Platform](../../dataflow/marketing-automation.md).
