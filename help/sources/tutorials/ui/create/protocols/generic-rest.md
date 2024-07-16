---
keywords: Experience Platform;home;argomenti popolari;API REST generica
title: Creare una connessione Source API REST generica nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente REST API generica utilizzando l’interfaccia utente di Adobe Experience Platform.
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 3%

---

# Crea una connessione sorgente [!DNL Generic REST API] nell&#39;interfaccia utente

>[!NOTE]
>
> L&#39;origine [!DNL Generic REST API] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../../../home.md#terms-and-conditions).

Questo tutorial illustra i passaggi per la creazione di un connettore di origine [!DNL Generic REST API] tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Per accedere al tuo account [!DNL Generic REST API] su Platform, devi fornire credenziali valide per il tipo di autenticazione desiderato. L’API REST generica supporta sia il codice di aggiornamento OAuth 2 che l’autenticazione di base. Per informazioni sulle credenziali per i due tipi di autenticazione supportati, vedere le tabelle seguenti.

#### Codice di aggiornamento OAuth 2

| Credenziali | Descrizione |
| --- | --- |
| Host | L’URL host dell’origine a cui stai effettuando la richiesta. Questo valore è obbligatorio e non può essere ignorato utilizzando la sostituzione del parametro della richiesta. |
| URL test di autorizzazione | (Facoltativo) L’URL del test di autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non vengono fornite, le credenziali vengono controllate automaticamente durante il passaggio di creazione della connessione di origine. |
| ID client | (Facoltativo) L’ID client associato al tuo account utente. |
| Segreto client | (Facoltativo) Il segreto client associato al tuo account utente. |
| Token di accesso | Credenziali di autenticazione primarie utilizzate per accedere all&#39;applicazione. Il token di accesso rappresenta l’autorizzazione dell’applicazione ad accedere ad aspetti particolari dei dati di un utente. Questo valore è obbligatorio e non può essere ignorato utilizzando la sostituzione del parametro della richiesta. |
| Aggiorna token | (Facoltativo) Token utilizzato per generare un nuovo token di accesso, se il token di accesso è scaduto. |
| URL token di accesso | (Facoltativo) L’endpoint URL utilizzato per recuperare il token di accesso. |
| Sostituzione parametro richiesta | (Facoltativo) Proprietà che consente di specificare i parametri delle credenziali da ignorare. |


#### Autenticazione di base

| Credenziali | Descrizione |
| --- | --- |
| Host | L’URL host dell’origine a cui stai effettuando la richiesta. |
| Nome utente | Il nome utente che corrisponde al tuo account utente. |
| Password | La password che corrisponde al tuo account utente. |

## Connettere l’account API REST generico

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Nella categoria [!UICONTROL Protocolli], selezionare **[!UICONTROL API REST generica]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/generic-rest/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a API REST generica]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per connettere un account esistente, seleziona l&#39;account API REST generico con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![esistente](../../../../images/tutorials/create/generic-rest/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione dell&#39;opzione per il nuovo account [!DNL Generic REST API].

![nuovo](../../../../images/tutorials/create/generic-rest/new.png)

#### Autenticazione tramite codice di aggiornamento OAuth 2

[!DNL Generic REST API] supporta sia il codice di aggiornamento OAuth 2 che l&#39;autenticazione di base. Per eseguire l&#39;autenticazione tramite un&#39;autenticazione OAuth2, selezionare **[!UICONTROL OAuth2RefreshCode]**, fornire le credenziali OAuth 2, quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Autenticazione tramite autenticazione di base

Per utilizzare l&#39;autenticazione di base, selezionare **[!UICONTROL Autenticazione di base]**, specificare l&#39;host, il nome utente e la password, quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione all’account API REST generico. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](../../dataflow/protocols.md).
