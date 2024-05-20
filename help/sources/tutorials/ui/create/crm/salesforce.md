---
title: Collegare l'account Salesforce tramite l'interfaccia utente Experienci Platform
description: Scopri come collegare il tuo account Salesforce e portare i tuoi dati di gestione delle relazioni con i clienti a Experience Platform utilizzando l’interfaccia utente di.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: c543590ef1806e5259da2ffb6833cd030d573ca7
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 1%

---

# Connetti [!DNL Salesforce] Experience Platform dell’account tramite l’interfaccia utente

Questo tutorial descrive come collegare [!DNL Salesforce] e trasferire i dati CRM a Adobe Experience Platform utilizzando l’interfaccia utente di Experienci Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Salesforce] account, puoi saltare il resto di questo documento e passare all’esercitazione su [configurazione di un flusso di dati per i dati CRM](../../dataflow/crm.md).

### Raccogli le credenziali richieste {#gather-required-credentials}

Il [!DNL Salesforce] L&#39;origine supporta l&#39;autenticazione di base e le credenziali client OAuth2.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

È necessario fornire i valori per le seguenti credenziali per connettere il [!DNL Salesforce] tramite autenticazione di base.

| Credenziali | Descrizione |
| --- | --- |
| URL ambiente | L’URL del [!DNL Salesforce] istanza di origine. |
| Nome utente | Nome utente per [!DNL Salesforce] account utente. |
| Password | La password per [!DNL Salesforce] account utente. |
| Token di sicurezza | Token di sicurezza per [!DNL Salesforce] account utente. |
| Versione API | (Facoltativo) La versione REST API di [!DNL Salesforce] che si sta utilizzando. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, è necessario immettere il valore come `52.0` Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. |

Per ulteriori informazioni sull’autenticazione, consulta [questo [!DNL Salesforce] guida all’autenticazione](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Credenziali client OAuth2]

È necessario fornire i valori per le seguenti credenziali per connettere il [!DNL Salesforce] utilizzando le credenziali client OAuth2.

| Credenziali | Descrizione |
| --- | --- |
| URL ambiente | L’URL del [!DNL Salesforce] istanza di origine. |
| ID client | L’ID client viene utilizzato insieme al segreto client come parte dell’autenticazione OAuth2. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto dell’account identificando l’applicazione in [!DNL Salesforce]. |
| Segreto client | Il segreto client viene utilizzato insieme all’ID client come parte dell’autenticazione OAuth2. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto dell’account identificando l’applicazione in [!DNL Salesforce]. |
| Versione API | (Facoltativo) La versione REST API di [!DNL Salesforce] che si sta utilizzando. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, è necessario immettere il valore come `52.0` Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. |

Per ulteriori informazioni sull’utilizzo di OAuth per [!DNL Salesforce], leggi [[!DNL Salesforce] guida ai flussi di autorizzazione OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Salesforce] da Experience Platform.

## Connetti [!DNL Salesforce] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere all’area di lavoro sorgenti. Il *[!UICONTROL Catalogo]* nella schermata vengono visualizzate diverse sorgenti disponibili nel catalogo sorgenti di Experience Platform.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare un’origine specifica utilizzando l’opzione di ricerca.

Seleziona **[!UICONTROL CRM]** dall’elenco delle categorie di origini, quindi seleziona **[!UICONTROL Aggiungi dati]** dal [!DNL Salesforce] Card.

![Catalogo delle sorgenti nell’interfaccia utente di Experienci Platform con la scheda sorgente Salesforce selezionata.](../../../../images/tutorials/create/salesforce/catalog.png)

Il **[!UICONTROL Connetti a Salesforce]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

>[!BEGINTABS]

>[!TAB Usa un account Salesforce esistente]

Per utilizzare un account esistente, seleziona **[!UICONTROL Account esistente]** quindi selezionare l&#39;account che si desidera utilizzare dall&#39;elenco visualizzato. Al termine, seleziona **[!UICONTROL Successivo]** per procedere.

![Elenco di account Salesforce autenticati già presenti nell’organizzazione.](../../../../images/tutorials/create/salesforce/existing.png)

>[!TAB Crea un nuovo account Salesforce]

Per utilizzare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome, una descrizione e [!DNL Salesforce] credenziali di autenticazione. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e lascia qualche secondo per consentire alla nuova connessione di stabilirsi.

![L’interfaccia in cui puoi creare un nuovo account Salesforce fornendo le credenziali di autenticazione appropriate.](../../../../images/tutorials/create/salesforce/new.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Salesforce] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/crm.md).
