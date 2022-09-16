---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
solution: Experience Platform
title: Creare una connessione sorgente Campagne MailChimp tramite l’interfaccia utente di Platform
topic-legacy: tutorial
description: Scopri come collegare Adobe Experience Platform a Campagne MailChimp tramite l’interfaccia utente di Platform.
exl-id: e8e1ed32-4277-44c9-aafc-6bb9e0a1fe0d
source-git-commit: 430b544835956ec0b212fb44d48beaae46afdd2e
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Crea un [!DNL Mailchimp Campaigns] connessione sorgente tramite l’interfaccia utente di Platform

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Mailchimp] connettore di origine da inserire [!DNL Mailchimp Campaigns] dati a Adobe Experience Platform tramite l’interfaccia utente di .

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Platform consente l’acquisizione di dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Raccogli credenziali richieste

Per portare il vostro [!DNL Mailchimp Campaigns] dati a Platform, devi innanzitutto fornire le credenziali di autenticazione appropriate corrispondenti alla tua [!DNL Mailchimp] conto.

La [!DNL Mailchimp Campaigns] source supporta sia il codice di aggiornamento OAuth 2 che l’autenticazione di base. Per ulteriori informazioni su questi tipi di autenticazione, vedere le tabelle riportate di seguito.

### Codice di aggiornamento OAuth 2

| Credenziali  | Descrizione |
| --- | --- |
| Domain | URL principale utilizzato per connettersi all&#39;API MailChimp. Il formato dell’URL principale è `https://{DC}.api.mailchimp.com`, dove `{DC}` rappresenta il data center che corrisponde al tuo account. |
| URL del test di autorizzazione | L’URL del test di autorizzazione viene utilizzato per convalidare le credenziali quando si connette [!DNL Mailchimp] su Platform. In caso contrario, le credenziali vengono controllate automaticamente durante il passaggio di creazione della connessione di origine. |
| Token di accesso | Il token di accesso corrispondente utilizzato per autenticare l&#39;origine. Questo è necessario per l’autenticazione basata su OAuth. |

Per ulteriori informazioni sull’utilizzo di OAuth 2 per l’autenticazione del [!DNL Mailchimp] account a Platform, consulta questo [[!DNL Mailchimp] documento sull’utilizzo di OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### Autenticazione di base

| Credenziali  | Descrizione |
| --- | --- |
| Dominio | URL principale utilizzato per connettersi all&#39;API MailChimp. Il formato dell’URL principale è `https://{DC}.api.mailchimp.com`, dove `{DC}` rappresenta il data center che corrisponde al tuo account. |
| Nome utente | Il nome utente che corrisponde al tuo account MailChimp. Questo è necessario per l’autenticazione di base. |
| Password | La password che corrisponde al tuo account MailChimp. Questo è necessario per l’autenticazione di base. |

## Collega il tuo [!DNL Mailchimp Campaigns] account a Platform

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la [!UICONTROL Automazione del marketing] categoria, seleziona **[!UICONTROL Campagna Mailchimp]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/mailchimp-campaigns/catalog.png)

La **[!UICONTROL Account Connect Mailchimp Campaigns]** viene visualizzata la pagina . In questa pagina puoi selezionare se stai effettuando l’accesso a un account esistente o scegliere di creare un nuovo account.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Mailchimp Campaigns] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/mailchimp-campaigns/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione per il tuo [!DNL Mailchimp Campaigns] dettagli della connessione sorgente.

![nuovo](../../../../images/tutorials/create/mailchimp-campaigns/new.png)

#### Autenticazione tramite OAuth 2

Per utilizzare OAuth 2, seleziona [!UICONTROL Codice di aggiornamento OAuth 2], fornire valori per il dominio, l&#39;URL del test di autorizzazione e il token di accesso, quindi selezionare **[!UICONTROL Connetti alla sorgente]**. Consentire alcuni istanti per la convalida delle credenziali, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![oauth](../../../../images/tutorials/create/mailchimp-campaigns/oauth.png)

#### Autenticazione tramite autenticazione di base

Per utilizzare l&#39;autenticazione di base, seleziona [!UICONTROL Autenticazione di base], fornire i valori per il dominio, il nome utente e la password, quindi selezionare **[!UICONTROL Connetti alla sorgente]**. Consentire alcuni istanti per la convalida delle credenziali, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![base](../../../../images/tutorials/create/mailchimp-campaigns/basic.png)

### Seleziona [!DNL Mailchimp Campaigns] dati

Una volta autenticata l&#39;origine, devi fornire `campaignId` che corrisponde al tuo [!DNL Mailchimp Campaigns] conto.

Sulla [!UICONTROL Seleziona dati] immetti `campaignId` quindi seleziona **[!UICONTROL Esplora]**.

![esplorare](../../../../images/tutorials/create/mailchimp-campaigns/explore.png)

La pagina viene aggiornata in una struttura dello schema interattiva che consente di esplorare e ispezionare la gerarchia dei dati. Seleziona **[!UICONTROL Successivo]** per procedere.

![select-data](../../../../images/tutorials/create/mailchimp-campaigns/select-data.png)

## Passaggi successivi

Con il tuo [!DNL Mailchimp] account autenticato e [!DNL Mailchimp Campaigns] i dati selezionati, ora puoi iniziare a creare un flusso di dati per trasferire i dati a Platform. Per i passaggi dettagliati su come creare un flusso di dati, consulta la documentazione su [creazione di un flusso di dati per trasferire i dati di automazione del marketing a Platform](../../dataflow/marketing-automation.md).
