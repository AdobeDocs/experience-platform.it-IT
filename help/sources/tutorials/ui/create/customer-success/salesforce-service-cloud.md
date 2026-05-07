---
title: Collegare l’account Salesforce Service Cloud tramite l’interfaccia utente di Experience Platform
description: Scopri come collegare il tuo account Salesforce Service Cloud e inserire i dati di successo dei clienti in Experience Platform utilizzando l’interfaccia utente di.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---

# Connetti il tuo account [!DNL Salesforce Service Cloud] ad Experience Platform tramite l&#39;interfaccia utente

Segui questa guida dettagliata per collegare facilmente il tuo account [!DNL Salesforce Service Cloud] e importare i dati di successo dei clienti in Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Salesforce Service Cloud] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati per il successo del cliente](../../dataflow/customer-success.md)

### Raccogli le credenziali richieste

Per ulteriori informazioni sul recupero delle credenziali, leggere la [guida all&#39;autenticazione](../../../../connectors/customer-success/salesforce-service-cloud.md#credentials).

## Connetti il tuo account [!DNL Salesforce Service Cloud]

Nell&#39;interfaccia utente di Experience Platform, selezionare **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Selezionare **[!DNL Salesforce Service Cloud]** nella categoria *[!UICONTROL Customer success]*, quindi selezionare **[!UICONTROL Add data]**.

>[!TIP]
>
>Le origini nel catalogo origini visualizzano l&#39;opzione **[!UICONTROL Set up]** quando una determinata origine non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Add data]**.

![Catalogo delle origini nell&#39;interfaccia utente di Experience Platform con la scheda di origine di Salesforce Service Cloud selezionata.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Salesforce Service Cloud]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Usa un account esistente

Per utilizzare un account esistente, selezionare **[!UICONTROL Existing account]**, quindi selezionare l&#39;account desiderato dall&#39;elenco visualizzato. Al termine, selezionare **[!UICONTROL Next]** per continuare.

![Elenco di account Salesforce Service Cloud autenticati già presenti nell&#39;organizzazione.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Crea un nuovo account

Per creare un nuovo account, selezionare **[!UICONTROL New account]** e fornire un nome e una descrizione per il nuovo account [!DNL Salesforce Service Cloud]. Quindi, selezionare **[!UICONTROL OAuth2 Client Credential]** e specificare i valori per le credenziali seguenti:

* URL ambiente
* ID client
* Segreto client
* Versione API

Al termine, selezionare **[!UICONTROL Connect to source]**.

![Interfaccia OAuth per la creazione dell&#39;account Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Salesforce Service Cloud]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati di successo del cliente in Experience Platform](../../dataflow/customer-success.md).
