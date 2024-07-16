---
title: Collegare l’account Salesforce Service Cloud utilizzando l’interfaccia utente di Experience Platform
description: Scopri come collegare il tuo account Salesforce Service Cloud e portare a Experience Platform i dati di successo del cliente tramite l’interfaccia utente di.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 3%

---

# Connetti il tuo account [!DNL Salesforce Service Cloud] ad Experience Platform utilizzando l&#39;interfaccia utente

Questo tutorial illustra i passaggi necessari per collegare l&#39;account [!DNL Salesforce Service Cloud] e inviare i dati di successo dei clienti a Adobe Experience Platform utilizzando l&#39;interfaccia utente di Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Salesforce Service Cloud] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati per il successo del cliente](../../dataflow/customer-success.md)

### Raccogli le credenziali richieste

L&#39;origine [!DNL Salesforce Service Cloud] supporta l&#39;autenticazione di base e le credenziali client OAuth2.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per connettere l&#39;account [!DNL Salesforce Service Cloud] tramite l&#39;autenticazione di base, è necessario fornire i valori per le credenziali seguenti.

| Credenziali | Descrizione |
| --- | --- |
| URL ambiente | URL dell&#39;istanza di origine [!DNL Salesforce Service Cloud]. |
| Nome utente | Nome utente per l&#39;account utente [!DNL Salesforce Service Cloud]. |
| Password | Password per l&#39;account utente [!DNL Salesforce Service Cloud]. |
| Token di sicurezza | Token di sicurezza per l&#39;account utente [!DNL Salesforce Service Cloud]. |
| Versione API | (Facoltativo) Versione REST API dell&#39;istanza [!DNL Salesforce Service Cloud] in uso. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, devi immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experience Platform utilizzerà automaticamente l’ultima versione disponibile. |

Per ulteriori informazioni sull&#39;autenticazione, consultare [questa [!DNL Salesforce Service Cloud] guida all&#39;autenticazione](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Credenziali client OAuth2]

È necessario fornire i valori per le credenziali seguenti per connettere l&#39;account [!DNL Salesforce Service Cloud] utilizzando le credenziali client OAuth2.

| Credenziali | Descrizione |
| --- | --- |
| URL ambiente | URL dell&#39;istanza di origine [!DNL Salesforce Service Cloud]. |
| ID client | L’ID client viene utilizzato insieme al segreto client come parte dell’autenticazione OAuth2. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Salesforce Service Cloud]. |
| Segreto client | Il segreto client viene utilizzato insieme all’ID client come parte dell’autenticazione OAuth2. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Salesforce Service Cloud]. |
| Versione API | Versione REST API dell&#39;istanza [!DNL Salesforce Service Cloud] in uso. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, devi immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experience Platform utilizzerà automaticamente l’ultima versione disponibile. |

Per ulteriori informazioni sull&#39;utilizzo di OAuth per [!DNL Salesforce Service Cloud], leggere la [[!DNL Salesforce Service Cloud] guida sui flussi di autorizzazione OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Salesforce Service Cloud] all&#39;Experience Platform.

## Connetti il tuo account [!DNL Salesforce Service Cloud]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Selezionare **[!DNL Salesforce Service Cloud]** nella categoria *[!UICONTROL Customer success]*, quindi selezionare **[!UICONTROL Add data]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini nell&#39;interfaccia utente di Experience Platform con la scheda sorgente di Salesforce Service Cloud selezionata.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Salesforce Service Cloud]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Usa un account esistente

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account desiderato dall&#39;elenco visualizzato. Al termine, selezionare **[!UICONTROL Avanti]** per continuare.

![Elenco di account autenticati di Salesforce Service Cloud già presenti nell&#39;organizzazione.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Crea un nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome e una descrizione per il nuovo account [!DNL Salesforce Service Cloud].

![Interfaccia in cui è possibile creare un nuovo account Salesforce Service Cloud fornendo le credenziali di autenticazione appropriate.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

Quindi, seleziona il tipo di autenticazione che desideri utilizzare per il nuovo account.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per l&#39;autenticazione di base, selezionare **[!UICONTROL Autenticazione di base]**, quindi specificare i valori per le credenziali seguenti:

* URL ambiente
* Nome utente
* Password
* Versione API (opzionale)

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione di base per la creazione dell&#39;account Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB Credenziali client OAuth2]

Per le credenziali client OAuth 2, selezionare **[!UICONTROL Credenziali client OAuth2]**, quindi specificare i valori per le credenziali seguenti:

* URL ambiente
* ID client
* Segreto client
* Versione API

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia OAuth per la creazione dell&#39;account Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Salesforce Service Cloud]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire i dati di successo del cliente in Experience Platform](../../dataflow/customer-success.md).
