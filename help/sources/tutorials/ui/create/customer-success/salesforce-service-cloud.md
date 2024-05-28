---
title: Collegare l’account Salesforce Service Cloud utilizzando l’interfaccia utente di Experienci Platform
description: Scopri come collegare il tuo account Salesforce Service Cloud e portare a Experience Platform i dati di successo del cliente tramite l’interfaccia utente di.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 3%

---

# Connetti [!DNL Salesforce Service Cloud] Experience Platform dell’account tramite l’interfaccia utente

Questo tutorial descrive come collegare [!DNL Salesforce Service Cloud] e trasferire i dati di successo dei clienti a Adobe Experience Platform utilizzando l’interfaccia utente di Experienci Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Salesforce Service Cloud] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati per il successo del cliente](../../dataflow/customer-success.md)

### Raccogli le credenziali richieste

Il [!DNL Salesforce Service Cloud] L&#39;origine supporta l&#39;autenticazione di base e le credenziali client OAuth2.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

È necessario fornire i valori per le seguenti credenziali per connettere il [!DNL Salesforce Service Cloud] tramite autenticazione di base.

| Credenziali | Descrizione |
| --- | --- |
| URL ambiente | L’URL del [!DNL Salesforce Service Cloud] istanza di origine. |
| Nome utente | Nome utente per [!DNL Salesforce Service Cloud] account utente. |
| Password | La password per [!DNL Salesforce Service Cloud] account utente. |
| Token di sicurezza | Token di sicurezza per [!DNL Salesforce Service Cloud] account utente. |
| Versione API | (Facoltativo) La versione REST API di [!DNL Salesforce Service Cloud] che si sta utilizzando. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, è necessario immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. |

Per ulteriori informazioni sull’autenticazione, consulta [questo [!DNL Salesforce Service Cloud] guida all’autenticazione](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Credenziali client OAuth2]

È necessario fornire i valori per le seguenti credenziali per connettere il [!DNL Salesforce Service Cloud] utilizzando le credenziali client OAuth2.

| Credenziali | Descrizione |
| --- | --- |
| URL ambiente | L’URL del [!DNL Salesforce Service Cloud] istanza di origine. |
| ID client | L’ID client viene utilizzato insieme al segreto client come parte dell’autenticazione OAuth2. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto del tuo account identificando l’applicazione in [!DNL Salesforce Service Cloud]. |
| Segreto client | Il segreto client viene utilizzato insieme all’ID client come parte dell’autenticazione OAuth2. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto del tuo account identificando l’applicazione in [!DNL Salesforce Service Cloud]. |
| Versione API | Versione REST API di [!DNL Salesforce Service Cloud] che si sta utilizzando. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, è necessario immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. |

Per ulteriori informazioni sull’utilizzo di OAuth per [!DNL Salesforce Service Cloud], leggi [[!DNL Salesforce Service Cloud] guida ai flussi di autorizzazione OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Salesforce Service Cloud] da Experience Platform.

## Connetti [!DNL Salesforce Service Cloud] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Seleziona **[!DNL Salesforce Service Cloud]** sotto *[!UICONTROL Customer success]* categoria, quindi selezionare **[!UICONTROL Aggiungi dati]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano **[!UICONTROL Configurazione]** quando una determinata origine non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Il catalogo delle sorgenti nell’interfaccia utente di Experienci Platform con la scheda sorgente Salesforce Service Cloud selezionata.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

Il **[!UICONTROL Connetti a Salesforce Service Cloud]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Usa un account esistente

Per utilizzare un account esistente, seleziona **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account desiderato dall&#39;elenco visualizzato. Al termine, seleziona **[!UICONTROL Successivo]** per procedere.

![Elenco di account Salesforce Service Cloud autenticati già presenti nell’organizzazione.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Crea un nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome e una descrizione per il nuovo [!DNL Salesforce Service Cloud] account.

![L’interfaccia in cui puoi creare un nuovo account Salesforce Service Cloud fornendo le credenziali di autenticazione appropriate.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

Quindi, seleziona il tipo di autenticazione che desideri utilizzare per il nuovo account.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per l’autenticazione di base, seleziona **[!UICONTROL Autenticazione di base]** e quindi fornisci i valori per le seguenti credenziali:

* URL ambiente
* Nome utente
* Password
* Versione API (opzionale)

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione di base per la creazione dell’account Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB Credenziali client OAuth2]

Per le credenziali client OAuth 2, selezionare **[!UICONTROL Credenziali client OAuth2]** e quindi fornisci i valori per le seguenti credenziali:

* URL ambiente
* ID client
* Segreto client
* Versione API

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]**.

![L’interfaccia OAuth per la creazione dell’account Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Salesforce Service Cloud] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare in Experience Platform i dati di successo del cliente](../../dataflow/customer-success.md).
