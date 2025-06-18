---
title: Creare una connessione Source di Azure Synapse Analytics nell’interfaccia utente
description: Scopri come creare una connessione sorgente Azure Synapse Analytics (di seguito "Synapse") utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Crea una connessione di origine [!DNL Azure Synapse Analytics] nell&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL Azure Synapse Analytics] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.

Leggere questa guida per scoprire come collegare l&#39;account [!DNL Azure Synapse Analytics] a Adobe Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Azure Synapse Analytics] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Azure Synapse Analytics] panoramica](../../../../connectors/databases/synapse-analytics.md#prerequisites).

## Navigare nel catalogo delle origini

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Origini]*. Scegliere una categoria o utilizzare la barra di ricerca per trovare l&#39;origine.

Per connettersi a [!DNL Azure Synapse Analytics], passare alla categoria *[!UICONTROL Database]*, selezionare la scheda di origine **[!UICONTROL Azure Synapse Analytics]**, quindi selezionare **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Una volta creato un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo origini con &quot;Azure Synapse Analytics&quot; selezionato.](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

## Usa un account esistente {#existing}

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account [!DNL Azure Synapse Analytics] che si desidera utilizzare.

![Interfaccia account esistente del flusso di lavoro origini.](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Crea un nuovo account {#new}

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi specifica un nome e, facoltativamente, aggiungi una descrizione per l&#39;account.

![Nuova interfaccia account del flusso di lavoro di origine.](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Connettersi ad Experience Platform

È possibile connettere l&#39;account [!DNL Azure Synapse Analytics] ad Experience Platform utilizzando l&#39;autenticazione della chiave dell&#39;account o l&#39;autenticazione dell&#39;entità servizio e della chiave.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Per utilizzare l&#39;autenticazione della chiave dell&#39;account, selezionare **[!UICONTROL Autenticazione della chiave dell&#39;account]**, specificare la [stringa di connessione](../../../../connectors/databases/synapse-analytics.md#prerequisites), quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Passaggio &quot;Crea nuovo account&quot; nel flusso di lavoro di origine con &quot;autenticazione chiave account selezionata.](../../../../images/tutorials/create/azure-synapse-analytics/account-key-auth.png)

>[!TAB Autenticazione entità servizio e chiave]

In alternativa, selezionare **[!UICONTROL Autenticazione principale servizio e chiave]**, fornire i valori per le [credenziali di autenticazione](../../../../connectors/databases/synapse-analytics.md#prerequisites), quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Passaggio &quot;Crea nuovo account&quot; nel flusso di lavoro delle origini con l&#39;opzione &quot;Autenticazione entità servizio e chiave&quot; selezionata.](../../../../images/tutorials/create/azure-synapse-analytics/service-principal.png)

>[!ENDTABS]

## Crea un flusso di dati per [!DNL Azure Synapse Analytics] dati

Dopo aver connesso correttamente il database [!DNL Azure Synapse Analytics], è ora possibile [creare un flusso di dati e acquisire dati dal database in Experience Platform](../../dataflow/databases.md).
