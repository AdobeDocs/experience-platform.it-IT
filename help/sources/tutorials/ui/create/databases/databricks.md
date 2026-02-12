---
title: Collegare I Database Ad Experience Platform Tramite L’Interfaccia Utente
description: Scopri come collegare i database ad Experience Platform utilizzando l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: 877e22c0-cb77-45bb-88c9-54fdde2d6905
source-git-commit: 6a30e1983a6dcf8e1340281a9385eb8e73b927f6
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 4%

---

# Connettere [!DNL Databricks] ad Experience Platform nell&#39;interfaccia utente

>[!AVAILABILITY]
>
>* L&#39;origine [!DNL Databricks] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time CDP Ultimate.
>
>* L&#39;origine [!DNL Databricks] è in versione beta. Leggi i [termini e condizioni](../../../../home.md#terms-and-conditions) nella panoramica delle origini per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta.

Leggere questa guida per scoprire come collegare l&#39;account [!DNL Databricks] a Adobe Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Specificare i valori per le credenziali seguenti per connettere [!DNL Databricks] ad Experience Platform.

| Credenziali | Descrizione |
| --- | --- |
| Dominio | URL dell&#39;area di lavoro [!DNL Databricks]. Ad esempio, `https://adb-1234567890123456.7.azuredatabricks.net`. |
| ID cluster | ID del cluster in [!DNL Databricks]. Questo cluster deve essere già un cluster esistente e deve essere un cluster interattivo. |
| Token di accesso | Il token di accesso che autentica l&#39;account [!DNL Databricks]. È possibile generare il token di accesso utilizzando l&#39;area di lavoro [!DNL Databricks]. |
| Database | Il nome del database nel delta lake. |

Per ulteriori informazioni, consulta la [[!DNL Databricks] panoramica](../../../../connectors/databases/databricks.md).

## Navigare nel catalogo delle origini

Nell&#39;interfaccia utente di Experience Platform, selezionare **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Sources]*. Scegliere una categoria o utilizzare la barra di ricerca per trovare l&#39;origine.

Per connettersi a [!DNL Databricks], passare alla categoria *[!UICONTROL Databases]*, selezionare la scheda di origine **[!UICONTROL Azure Databricks]**, quindi selezionare **[!UICONTROL Set up]**.

>[!TIP]
>
>Le origini nel catalogo origini visualizzano l&#39;opzione **[!UICONTROL Set up]** quando una determinata origine non dispone ancora di un account autenticato. Una volta creato un account autenticato, questa opzione diventa **[!UICONTROL Add data]**.

![Catalogo delle origini con la scheda di origine di Azure Databricks selezionata.](../../../../images/tutorials/create/databricks/catalog.png)

### Usa un account esistente

Per utilizzare un account esistente, selezionare **[!UICONTROL Existing account]**, quindi selezionare l&#39;account [!DNL Azure Databricks] che si desidera utilizzare.

![Interfaccia account esistente nel flusso di lavoro di origine con &quot;Account esistente&quot; selezionato.](../../../../images/tutorials/create/databricks/existing.png)

### Crea un nuovo account

Per creare un nuovo account, selezionare **[!UICONTROL New account]**, specificare un nome e aggiungere facoltativamente una descrizione per l&#39;account. Quindi, fornisci i valori per le seguenti credenziali di autenticazione:

* Dominio
* ID cluster
* Token di accesso
* Database
* Catalogo

![Nuova interfaccia account nel flusso di lavoro di origine con un nome account e una descrizione facoltativa forniti.](../../../../images/tutorials/create/databricks/new.png)

È inoltre necessario copiare e incollare le credenziali di [!UICONTROL Staging SAS URI] nell&#39;ambiente [!DNL Azure Databricks]. Al termine, selezionare **[!UICONTROL Connect to source]** e attendere alcuni istanti per consentire la connessione.

![Credenziali di gestione temporanea dell&#39;URI SAS.](../../../../images/tutorials/create/databricks/sas-uri.png)

## Crea un flusso di dati per [!DNL Azure Databricks] dati

Dopo aver connesso correttamente l&#39;account [!DNL Azure Databricks], è ora possibile [creare un flusso di dati e acquisire dati dal database in Experience Platform](../../dataflow/databases.md).
