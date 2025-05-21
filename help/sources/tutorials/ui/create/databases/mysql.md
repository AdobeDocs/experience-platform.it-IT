---
title: Connettere MySQL Ad Experience Platform Utilizzando L’Interfaccia Utente
description: Scopri come collegare il database MySQL ad Experience Platform utilizzando l’interfaccia utente.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Connetti [!DNL MySQL] ad Experience Platform tramite l&#39;interfaccia utente

Leggere questa guida per scoprire come collegare il database [!DNL MySQL] a Adobe Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente di Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL MySQL], puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL MySQL] panoramica](../../../../connectors/databases/mysql.md#prerequisites).

## Navigare nel catalogo delle origini

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Origini]*. Scegliere una categoria o utilizzare la barra di ricerca per trovare l&#39;origine.

Per connettersi a [!DNL MySQL], passare alla categoria *[!UICONTROL Database]*, selezionare la scheda di origine **[!UICONTROL MySQL]**, quindi selezionare **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Una volta creato un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo origini con la scheda di origine MySQL selezionata.](../../../../images/tutorials/create/my-sql/catalog.png)

## Usa un account esistente {#existing}

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account [!DNL MySQL] che si desidera utilizzare.

![Interfaccia account esistente nel flusso di lavoro di origine con &quot;Account esistente&quot; selezionato.](../../../../images/tutorials/create/my-sql/existing.png)

## Crea un nuovo account {#new}

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi specifica un nome e, facoltativamente, aggiungi una descrizione per l&#39;account.

![Nuova interfaccia account nel flusso di lavoro di origine con un nome account e una descrizione facoltativa forniti.](../../../../images/tutorials/create/my-sql/new.png)

### Connettersi ad Experience Platform in Azure {#azure}

È possibile connettere il database [!DNL MySQL] ad Experience Platform su Azure utilizzando la chiave account o l&#39;autenticazione di base.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Per utilizzare l&#39;autenticazione della chiave dell&#39;account, selezionare **[!UICONTROL Autenticazione della chiave dell&#39;account]**, specificare la [stringa di connessione](../../../../connectors/databases/mysql.md#azure), quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![La nuova interfaccia account nel flusso di lavoro origini con &quot;Autenticazione chiave account&quot; selezionata.](../../../../images/tutorials/create/my-sql/account-key.png)

>[!TAB Autenticazione di base]

Per utilizzare l&#39;autenticazione di base, selezionare **[!UICONTROL Autenticazione di base]**, fornire i valori per le [credenziali di autenticazione](../../../../connectors/databases/mysql.md#azure), quindi selezionare **[!UICONTROL Connetti all&#39;origine]**.

![La nuova interfaccia account nel flusso di lavoro origini con &quot;Autenticazione di base&quot; selezionata.](../../../../images/tutorials/create/my-sql/basic-auth.png)

>[!ENDTABS]

### Connettersi ad Experience Platform su Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../../landing/multi-cloud.md).

Per creare un nuovo account [!DNL MySQL] e connettersi ad Experience Platform su AWS, verificare di essere in una sandbox VA6 e quindi fornire le [credenziali necessarie per l&#39;autenticazione](../../../../connectors/databases/mysql.md#aws).

![La nuova interfaccia account nel flusso di lavoro origini per la connessione ad AWS.](../../../../images/tutorials/create/my-sql/aws.png)

## Crea un flusso di dati per [!DNL MySQL] dati

Dopo aver connesso correttamente il database [!DNL MySQL], è ora possibile [creare un flusso di dati e acquisire dati dal database in Experience Platform](../../dataflow/databases.md).
