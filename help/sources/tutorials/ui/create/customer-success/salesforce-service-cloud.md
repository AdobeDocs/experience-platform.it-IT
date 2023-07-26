---
title: Collegare l’account Salesforce Service Cloud utilizzando l’interfaccia utente di Experienci Platform
description: Scopri come collegare il tuo account Salesforce Service Cloud e portare a Experience Platform i dati di successo del cliente tramite l’interfaccia utente di.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 57cdcbd5018e7f57261f09c6bddf5e2a8dcfd0d5
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

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

Per accedere al tuo [!DNL Salesforce Service Cloud] account di Experience Platform, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| --- | --- |
| `environmentUrl` | L’URL del [!DNL Salesforce Service Cloud] istanza di origine. |
| `username` | Nome utente per [!DNL Salesforce Service Cloud] account utente. |
| `password` | La password per [!DNL Salesforce Service Cloud] account utente. |
| `securityToken` | Token di sicurezza per [!DNL Salesforce Service Cloud] account utente. |
| `apiVersion` | (Facoltativo) La versione REST API di [!DNL Salesforce Service Cloud] che si sta utilizzando. Se questo campo viene lasciato vuoto, Experienci Platform utilizzerà automaticamente l’ultima versione disponibile. |

Per ulteriori informazioni sull’autenticazione, consulta [questo [!DNL Salesforce] guida all’autenticazione](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

## Connetti [!DNL Salesforce Service Cloud] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Salesforce] da Experience Platform.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere all’area di lavoro sorgenti. Il *[!UICONTROL Catalogo]* nella schermata vengono visualizzate diverse origini disponibili nel catalogo sorgenti di Experience Platform.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare un’origine specifica utilizzando l’opzione di ricerca.

Seleziona **[!UICONTROL Customer success]** dall’elenco delle categorie di origini, quindi seleziona **[!UICONTROL Aggiungi dati]** dal [!DNL Salesforce Service Cloud] Card.

![Il catalogo delle sorgenti nell’interfaccia utente di Experienci Platform con la scheda sorgente Salesforce Service Cloud selezionata.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

Il **[!UICONTROL Connetti a Salesforce Service Cloud]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

>[!BEGINTABS]

>[!TAB Usa un account Salesforce Service Cloud esistente]

Per utilizzare un account esistente, seleziona **[!UICONTROL Account esistente]** quindi selezionare l&#39;account che si desidera utilizzare dall&#39;elenco visualizzato. Al termine, seleziona **[!UICONTROL Successivo]** per procedere.

![Elenco di account Salesforce autenticati già presenti nell’organizzazione.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

>[!TAB Crea un nuovo account Salesforce Service Cloud]

Per utilizzare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome, una descrizione e [!DNL Salesforce Service Cloud] credenziali di autenticazione. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e lascia qualche secondo per consentire alla nuova connessione di stabilirsi.

![L’interfaccia in cui puoi creare un nuovo account Salesforce fornendo le credenziali di autenticazione appropriate.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Salesforce Service Cloud] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare in Experience Platform i dati di successo del cliente](../../dataflow/customer-success.md).
