---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;oracle;
title: (Beta) Crea un Oracle di connessione sorgente Responsys tramite l’interfaccia utente di Platform
description: Scopri come collegare Adobe Experience Platform a Oracle Responsys utilizzando l’interfaccia utente di Platform.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# (Beta) Crea un [!DNL Oracle Responsys] connessione sorgente tramite l’interfaccia utente di Platform

>[!NOTE]
>
>La [!DNL Oracle Responsys] la sorgente è in versione beta. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo dei connettori con etichetta beta.

Questa esercitazione descrive i passaggi necessari per creare un [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) connessione di origine tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Platform:

* [Origini](../../../../home.md): Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Se disponi già di un&#39;autenticazione [!DNL Oracle Responsys] account su Platform, puoi saltare il resto del documento e procedere all’esercitazione su [creazione di un flusso di dati per trasferire i dati di automazione del marketing a Platform](../../dataflow/marketing-automation.md).

### Raccogli credenziali richieste

Per connettersi [!DNL Oracle Responsys] su Platform, devi fornire valori per le seguenti proprietà di autenticazione:

| Credenziali | Descrizione |
| --- | --- |
| Endpoint | L’URL dell’endpoint di autenticazione REST del tuo [!DNL Oracle Responsys] istanza. |
| ID client | L&#39;ID cliente del tuo [!DNL Oracle Responsys] istanza. |
| Segreto client | Il segreto cliente del tuo [!DNL Oracle Responsys] istanza. |

Per ulteriori informazioni sulle credenziali di autenticazione per [!DNL Oracle Responsys], vedi [[!DNL Oracle Responsys] guida all’autenticazione](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Oracle Responsys] a Platform.

## Collega il tuo [!DNL Oracle Responsys] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la [!UICONTROL Automazione del marketing] categoria, seleziona **[!UICONTROL Oracle Responsys]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo origini Adobe Experience Platform con l&#39;Oracle Origine Responsys evidenziato.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

La **[!UICONTROL Connetti account Oracle Responsys]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Oracle Responsys] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![La schermata di autenticazione dell’account esistente, ad Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e i valori appropriati per il tuo [!DNL Oracle Responsys] credenziali. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![La nuova schermata di autenticazione dell’account, ad Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai autenticato e creato una connessione sorgente tra [!DNL Oracle Responsys] account e piattaforma. Ora puoi passare all’esercitazione successiva e [creare un flusso di dati per trasferire i dati di automazione del marketing a Platform](../../dataflow/marketing-automation.md).
