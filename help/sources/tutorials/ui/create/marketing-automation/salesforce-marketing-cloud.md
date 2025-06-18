---
title: Collegare l’account Marketing Cloud di Salesforce ad Experience Platform tramite l’interfaccia utente
description: Scopri come collegare il tuo account Marketing Cloud di Salesforce ad Experience Platform tramite l’interfaccia utente.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 0c6a51d06e57eb6de063a350bd4b17022555a0b4
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Connetti il tuo account [!DNL Salesforce Marketing Cloud] ad Experience Platform tramite l&#39;interfaccia utente

>[!WARNING]
>
>L&#39;origine [!DNL Salesforce Marketing Cloud] diventerà obsoleta a gennaio 2026. Una nuova fonte verrà rilasciata nel corso di quest&#39;anno come alternativa. Una volta rilasciata la nuova origine, è necessario pianificare la migrazione alla nuova origine creando nuove connessioni account e flussi di dati prima della fine di gennaio 2026.

Leggere questa guida per scoprire come collegare l&#39;account [!DNL Salesforce Marketing Cloud] a Adobe Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente di Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL Salesforce Marketing Cloud], puoi saltare il resto di questo documento e passare all&#39;esercitazione su [portare dati di automazione marketing in Experience Platform utilizzando l&#39;interfaccia utente](../../dataflow/marketing-automation.md).

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Salesforce Marketing Cloud] panoramica](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#prerequisites).

## Navigare nel catalogo delle origini

>[!IMPORTANT]
>
>L&#39;acquisizione di oggetti personalizzati non è attualmente supportata dall&#39;integrazione di origine [!DNL Salesforce Marketing Cloud].


Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Origini]*. Scegliere una categoria o utilizzare la barra di ricerca per trovare l&#39;origine.

Per connettersi a [!DNL Salesforce Marketing Cloud], passare alla categoria *[!UICONTROL Marketing Automation]*, selezionare la scheda di origine **[!UICONTROL Salesforce Marketing Cloud]**, quindi selezionare **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Una volta creato un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con la scheda di origine di Salesforce Marketing Cloud selezionata.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

## Usa un account esistente {#existing}

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account [!DNL Salesforce Marketing Cloud] che si desidera utilizzare.

![Interfaccia account esistente nel flusso di lavoro di origine con &quot;Account esistente&quot; selezionato.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Crea un nuovo account {#new}

È possibile utilizzare l&#39;origine [!DNL Salesforce Marketing Cloud] per connettersi ad Experience Platform su [!DNL Azure] o [!DNL Amazon Web Services] (AWS).

### Connetti ad Experience Platform il [!DNL Azure] {#azure}

Per connettersi ad Experience Platform il [!DNL Azure], fornisci un nome account, una descrizione facoltativa e le [credenziali di autenticazione account](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#azure). Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

![La nuova interfaccia account nel flusso di lavoro origini per la connessione ad Experience Platform in Azure.](../../../../images/tutorials/create/salesforce-marketing-cloud/new-azure.png)

### Connettersi ad Experience Platform su Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per connettersi ad Experience Platform il [!DNL AWS], accertati di trovarti in una sandbox VA6 e fornisci un nome account, una descrizione facoltativa e le [credenziali di autenticazione account](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#aws). Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

![La nuova interfaccia account nel flusso di lavoro origini per la connessione ad Experience Platform su AWS](../../../../images/tutorials/create/salesforce-marketing-cloud/new-aws.png)

## Crea un flusso di dati per [!DNL Salesforce Marketing Cloud] dati

Dopo aver connesso correttamente [!DNL Salesforce Marketing Cloud], è ora possibile [creare un flusso di dati e acquisire dati dal provider di automazione marketing in Experience Platform](../../dataflow/marketing-automation.md).
