---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
solution: Experience Platform
title: Creare una connessione sorgente dei membri MailChimp tramite l’interfaccia utente di Platform
topic-legacy: tutorial
description: Scopri come collegare Adobe Experience Platform ai membri MailChimp tramite l’interfaccia utente di Platform.
exl-id: dc620ef9-624d-4fc9-8475-bb475ea86eb7
source-git-commit: ed185d0957c3cd84c33a6ff60c5ded2b17fbfe74
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Crea un [!DNL Mailchimp Members] connessione sorgente tramite l’interfaccia utente di Platform

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Mailchimp] connettore di origine da inserire [!DNL Mailchimp Members] dati a Adobe Experience Platform tramite l’interfaccia utente di .

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Platform consente l’acquisizione di dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Raccogli credenziali richieste

Per portare il vostro [!DNL Mailchimp Members] dati a Platform, devi innanzitutto fornire le credenziali di autenticazione appropriate corrispondenti alla tua [!DNL Mailchimp] conto.

La [!DNL Mailchimp Members] source supporta sia il codice di aggiornamento OAuth 2 che l’autenticazione di base. Per ulteriori informazioni su questi tipi di autenticazione, consulta le tabelle riportate di seguito.

### Codice di aggiornamento OAuth 2

| Credenziali | Descrizione |
| --- | --- |
| Host | URL principale utilizzato per connettersi all&#39;API MailChimp. Il formato dell’URL principale è `https://{DC}.api.mailchimp.com`, dove `{DC}` rappresenta il data center che corrisponde al tuo account. |
| URL del test di autorizzazione | L’URL del test di autorizzazione viene utilizzato per convalidare le credenziali quando si connette [!DNL Mailchimp] su Platform. In caso contrario, le credenziali vengono controllate automaticamente durante il passaggio di creazione della connessione di origine. |
| Token di accesso | Il token di accesso corrispondente utilizzato per autenticare l&#39;origine. Questo è necessario per l’autenticazione basata su OAuth. |

Per ulteriori informazioni sull’utilizzo di OAuth 2 per l’autenticazione del [!DNL Mailchimp] account a Platform, consulta questo [[!DNL Mailchimp] documento sull’utilizzo di OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### Autenticazione di base

| Credenziali | Descrizione |
| --- | --- |
| Host | URL principale utilizzato per connettersi all&#39;API MailChimp. Il formato dell’URL principale è `https://{DC}.api.mailchimp.com`, dove `{DC}` rappresenta il data center che corrisponde al tuo account. |
| Nome utente | Il nome utente che corrisponde al tuo account MailChimp. Questo è necessario per l’autenticazione di base. |
| Password | La password che corrisponde al tuo account MailChimp. Questo è necessario per l’autenticazione di base. |

## Collega il tuo [!DNL Mailchimp Members] account a Platform

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la [!UICONTROL Automazione del marketing] categoria, seleziona **[!UICONTROL Campagna Mailchimp]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/mailchimp-members/catalog.png)

La **[!UICONTROL Account Connect Mailchimp Campaigns]** viene visualizzata la pagina . In questa pagina puoi selezionare se stai effettuando l’accesso a un account esistente o scegliere di creare un nuovo account.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Mailchimp Members] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/mailchimp-members/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione per il tuo [!DNL Mailchimp Members] dettagli della connessione sorgente.

![nuovo](../../../../images/tutorials/create/mailchimp-members/new.png)


#### Autenticazione tramite OAuth 2

Per utilizzare OAuth 2, seleziona [!UICONTROL Codice di aggiornamento OAuth 2], fornisci valori per l’host, l’URL del test di autorizzazione e il token di accesso, quindi seleziona **[!UICONTROL Connetti alla sorgente]**. Consentire alcuni istanti per la convalida delle credenziali, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![oauth](../../../../images/tutorials/create/mailchimp-members/oauth.png)

#### Autenticazione tramite autenticazione di base

Per utilizzare l&#39;autenticazione di base, seleziona [!UICONTROL Autenticazione di base], fornire i valori per l&#39;host, il nome utente e la password, quindi selezionare **[!UICONTROL Connetti alla sorgente]**. Consentire alcuni istanti per la convalida delle credenziali, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![base](../../../../images/tutorials/create/mailchimp-members/basic.png)

### Seleziona [!DNL Mailchimp Members] dati

Una volta autenticata l&#39;origine, devi fornire `listId` che corrisponde al tuo [!DNL Mailchimp Members] conto.

Sulla [!UICONTROL Seleziona dati] immetti `listId` quindi seleziona **[!UICONTROL Esplora]**.

![esplorare](../../../../images/tutorials/create/mailchimp-members/explore.png)

La pagina viene aggiornata in una struttura dello schema interattiva che consente di esplorare e ispezionare la gerarchia dei dati. Seleziona **[!UICONTROL Successivo]** per procedere.

![select-data](../../../../images/tutorials/create/mailchimp-members/select-data.png)

## Passaggi successivi

Con il tuo [!DNL Mailchimp] account autenticato e [!DNL Mailchimp Members] i dati selezionati, ora puoi iniziare a creare un flusso di dati per trasferire i dati a Platform. Per i passaggi dettagliati su come creare un flusso di dati, consulta la documentazione su [creazione di un flusso di dati per trasferire i dati di automazione del marketing a Platform](../../dataflow/marketing-automation.md).
