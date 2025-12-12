---
title: Panoramica dell’estensione Microsoft Azure
description: Scopri l’estensione Microsoft Azure per l’inoltro degli eventi in Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# Panoramica dell&#39;estensione [!DNL Microsoft Azure]

In [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) è un servizio di immissione dati altamente scalabile e in tempo reale che consente di elaborare e analizzare le grandi quantità di dati prodotti dai dispositivi e dalle applicazioni connessi. Una volta raccolti i dati in un hub eventi, questi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/archiviazione.

L&#39;estensione [!DNL Microsoft Azure] [event forwarding](../../../ui/event-forwarding/overview.md) sfrutta [!DNL Event Hubs] per inviare eventi da Adobe Experience Platform Edge Network a [!DNL Azure] per ulteriore elaborazione. Questa guida illustra come installare l’estensione e utilizzarne le funzionalità in una regola di inoltro degli eventi.

## Prerequisiti

Per utilizzare questa estensione, è necessario disporre di un account [!DNL Azure] valido con accesso a [!DNL Event Hubs]. Devi anche [creare un hub eventi utilizzando il [!DNL Azure] portale](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) prima di seguire i passaggi seguenti.

## Installare l’estensione

Per installare l&#39;estensione Microsoft [!DNL Azure], passa all&#39;interfaccia utente di Data Collection o all&#39;interfaccia utente di Experience Platform e seleziona **[!UICONTROL Event Forwarding]** dal menu di navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione o creane una nuova.

Dopo aver selezionato o creato la proprietà desiderata, selezionare **[!UICONTROL Extensions]** nel menu di navigazione a sinistra, quindi selezionare la scheda **[!UICONTROL Catalog]**. Cerca la scheda [!UICONTROL Microsoft Azure], quindi seleziona **[!UICONTROL Install]**.

![Pulsante [!UICONTROL Install] selezionato per l&#39;estensione [!UICONTROL Microsoft Azure] nell&#39;interfaccia utente di Data Collection.](../../../images/extensions/server/azure/install.png)

Poiché l&#39;estensione non dispone di proprietà di configurazione, viene aggiunta immediatamente all&#39;elenco delle estensioni installate. È ora possibile iniziare a utilizzare i tipi di azione [!DNL Event Hub] durante la configurazione delle regole di inoltro degli eventi.

## Configurare una regola di inoltro degli eventi {#rule}

Inizia a creare una nuova regola di inoltro degli eventi e configurane le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona **[!UICONTROL Microsoft Azure]** per l&#39;estensione, quindi seleziona **[!UICONTROL Send Data to Event Hubs]** per il tipo di azione.

![Tipo di azione [!UICONTROL Send Data to Event Hubs] selezionato per una regola nell&#39;interfaccia utente di Data Collection.](../../../images/extensions/server/azure/select-action-type.png)

Il pannello a destra si aggiorna per mostrare le opzioni di configurazione per la modalità di invio dei dati. In particolare, devi assegnare [elementi dati](../../../ui/managing-resources/data-elements.md) alle varie proprietà che rappresentano la tua configurazione di [!DNL Event Hub].

![Opzioni di configurazione per il tipo di azione [!UICONTROL Send Data to Event Hubs] visualizzato nell&#39;interfaccia utente.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Event Hub Details]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Namespace] | Nome dello spazio dei nomi [!DNL Event Hubs] creato durante la [configurazione dell&#39;hub eventi](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Name] | Nome dell’hub eventi. |
| [!UICONTROL SAS Authorization Rule Name] | Nome della regola di autorizzazione di accesso condiviso per l&#39;intero spazio dei nomi [!DNL Event Hubs] o per l&#39;istanza hub eventi specifica a cui si desidera inviare i dati. Per ulteriori informazioni, vedere la sezione dell&#39;appendice su [ottenimento dei valori di autorizzazione SAS](#sas). |
| [!UICONTROL SAS Access Key] | Chiave primaria della regola di autorizzazione di accesso condiviso per l&#39;intero spazio dei nomi [!DNL Event Hubs] o per l&#39;istanza hub eventi specifica a cui si desidera inviare i dati. Per ulteriori informazioni, vedere la sezione dell&#39;appendice su [ottenimento dei valori di autorizzazione SAS](#sas). |
| [!UICONTROL Partition ID] | [!DNL Event Hubs] consente di [inviare eventi direttamente a partizioni specifiche](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Per sfruttare questa funzione, fornisci l’ID della partizione a cui desideri inviare gli eventi. |

{style="table-layout:auto"}

**Dati**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Payload] | Questo campo contiene i dati che verranno inoltrati a [!DNL Event Hubs]. I dati possono essere un oggetto JSON, una stringa o un elemento dati. |

{style="table-layout:auto"}

Al termine, selezionare **[!UICONTROL Keep Changes]** per aggiungere l&#39;azione alla configurazione della regola. Quando si è soddisfatti della regola, selezionare **[!UICONTROL Save to Library]**.

Infine, pubblica un nuovo evento con inoltro di [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Event Hubs] utilizzando l&#39;estensione di inoltro eventi [!DNL Microsoft Azure]. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro degli eventi](../../../ui/event-forwarding/overview.md).

## Appendice: ottenere i valori di autorizzazione SAS {#sas}

Alle applicazioni esterne viene concesso l&#39;accesso a [!DNL Event Hubs] tramite [firme di accesso condiviso (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Ogni istanza hub eventi e spazio dei nomi [!DNL Event Hubs] dispone di una regola di autorizzazione SAS predefinita assegnata automaticamente al momento della creazione, ma è anche possibile creare criteri aggiuntivi per ogni risorsa.

Quando [configuri una regola di inoltro eventi](#rule) utilizzando l&#39;estensione [!DNL Azure], devi fornire il nome e la chiave primaria per la regola di autorizzazione che disciplina lo spazio dei nomi o l&#39;hub eventi specifico a cui desideri inviare i dati. Per informazioni dettagliate su come ottenere questi valori dal portale [!DNL Azure], fare riferimento alle sezioni seguenti nella documentazione di [!DNL Azure]:

* [Ottieni valori SAS per uno [!DNL Event Hubs] spazio dei nomi](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Ottenere valori SAS per un hub eventi specifico in uno spazio dei nomi](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Una volta ottenuti i valori richiesti, il nome della regola di autorizzazione può essere fornito direttamente come stringa nell’input di configurazione oppure puoi creare un elemento dati di tipo stringa a cui fare riferimento. La chiave primaria, tuttavia, deve prima essere contenuta all’interno di un segreto di inoltro degli eventi prima di poter essere fornita nella configurazione della regola per proteggere la sicurezza dei dati.

Nell&#39;interfaccia utente per l&#39;inoltro degli eventi, [crea un nuovo segreto](../../../ui/event-forwarding/secrets.md) e seleziona **[!UICONTROL Token]** come tipo segreto. Per il valore del token stesso, specifica la chiave primaria copiata in precedenza. Dopo aver creato il segreto, creare un elemento dati con il tipo **[!UICONTROL Secret]** e selezionare il segreto [!DNL Event Hubs] dall&#39;elenco. Una volta configurato l&#39;elemento dati segreto, è possibile fare riferimento a tale elemento dati nel campo **[!UICONTROL SAS Access Key]**.
