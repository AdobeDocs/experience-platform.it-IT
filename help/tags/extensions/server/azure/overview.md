---
title: Panoramica dell’estensione Microsoft Azure
description: Scopri l’estensione Microsoft Azure per l’inoltro di eventi in Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 3%

---

# [!DNL Microsoft Azure] panoramica dell&#39;estensione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

In [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) è un servizio altamente scalabile in tempo reale che consente di elaborare e analizzare le enormi quantità di dati prodotti dai dispositivi e dalle applicazioni collegati. Una volta raccolti i dati in un hub eventi, questi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/storage.

La [!DNL Microsoft Azure] [inoltro eventi](../../../ui/event-forwarding/overview.md) utilizzo di estensioni [!DNL Event Hubs] per inviare eventi da Adobe Experience Platform Edge Network a [!DNL Azure] per ulteriori elaborazioni. Questa guida illustra come installare l&#39;estensione e utilizzarne le funzionalità in una regola di inoltro degli eventi.

## Prerequisiti

Per utilizzare questa estensione, è necessario disporre di un [!DNL Azure] account con accesso a [!DNL Event Hubs]. Devi anche [creare un hub evento utilizzando [!DNL Azure] portale](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) prima di seguire i passaggi seguenti.

## Installare l’estensione

Per installare Microsoft [!DNL Azure] , passa all’interfaccia utente di raccolta dati o di Experience Platform e seleziona **[!UICONTROL Inoltro eventi]** dalla navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione oppure crea una nuova proprietà.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seleziona il **[!UICONTROL Catalogo]** scheda . Cerca il [!UICONTROL Microsoft Azure] scheda , quindi seleziona **[!UICONTROL Installa]**.

![La [!UICONTROL Installa] pulsante selezionato per [!UICONTROL Microsoft Azure] estensione nell’interfaccia utente di raccolta dati.](../../../images/extensions/server/azure/install.png)

Poiché l&#39;estensione non dispone di proprietà di configurazione, viene aggiunta immediatamente all&#39;elenco delle estensioni installate. Ora puoi iniziare a utilizzare [!DNL Event Hub] tipi di azioni durante la configurazione delle regole di inoltro eventi.

## Configurare una regola di inoltro eventi {#rule}

Inizia a creare una nuova regola di inoltro eventi e configurane le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona **[!UICONTROL Microsoft Azure]** per l&#39;estensione , quindi seleziona **[!UICONTROL Inviare dati agli hub eventi]** per il tipo di azione.

![La [!UICONTROL Inviare dati agli hub eventi] tipo di azione selezionato per una regola nell&#39;interfaccia utente Raccolta dati.](../../../images/extensions/server/azure/select-action-type.png)

Il pannello a destra si aggiorna e mostra le opzioni di configurazione per l’invio dei dati. In particolare, è necessario assegnare [elementi dati](../../../ui/managing-resources/data-elements.md) alle varie proprietà che rappresentano la [!DNL Event Hub] configurazione.

![Le opzioni di configurazione per [!UICONTROL Inviare dati agli hub eventi] tipo di azione mostrato nell’interfaccia utente.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Dettagli hub eventi]**

| Ingresso | Descrizione |
| --- | --- |
| [!UICONTROL Spazio dei nomi] | Nome della [!DNL Event Hubs] spazio dei nomi creato quando [configurazione dell’hub dell’evento](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Nome] | Nome dell&#39;hub eventi. |
| [!UICONTROL Nome della regola di autorizzazione SAS] | Nome della regola di autorizzazione di accesso condiviso per l&#39;intero [!DNL Event Hubs] spazio dei nomi o l&#39;istanza specifica dell&#39;hub eventi a cui si desidera inviare i dati. Vedi la sezione dell&#39;appendice su [ottenimento dei valori di autorizzazione SAS](#sas) per ulteriori informazioni. |
| [!UICONTROL Chiave di accesso SAS] | Chiave primaria della regola di autorizzazione di accesso condiviso per l&#39;intero [!DNL Event Hubs] spazio dei nomi o l&#39;istanza specifica dell&#39;hub eventi a cui si desidera inviare i dati. Vedi la sezione dell&#39;appendice su [ottenimento dei valori di autorizzazione SAS](#sas) per ulteriori informazioni. |
| [!UICONTROL ID partizione] | [!DNL Event Hubs] consente di [inviare eventi direttamente a partizioni specifiche](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Per sfruttare questa funzione, fornisci l’ID della partizione che desideri ricevere gli eventi. |

{style="table-layout:auto"}

**Dati**

| Ingresso | Descrizione |
| --- | --- |
| [!UICONTROL Payload] | Questo campo contiene i dati che verranno inoltrati al [!DNL Event Hubs]. I dati possono essere un oggetto JSON, una stringa o un elemento dati. |

{style="table-layout:auto"}

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola. Quando la regola è soddisfatta, seleziona **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo inoltro evento [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Event Hubs] utilizzando [!DNL Microsoft Azure] estensione inoltro eventi. Per ulteriori informazioni sulle funzionalità di inoltro eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).

## Appendice: Ottenere i valori di autorizzazione SAS {#sas}

Alle applicazioni esterne è concesso l&#39;accesso [!DNL Event Hubs] attraverso [firme di accesso condiviso (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Ogni [!DNL Event Hubs] Lo spazio dei nomi e l&#39;istanza dell&#39;hub eventi dispongono di una regola di autorizzazione SAS predefinita assegnata automaticamente al momento della creazione, ma è anche possibile creare criteri aggiuntivi per ogni risorsa, se lo si desidera.

Quando [configurazione di una regola di inoltro eventi](#rule) utilizzando [!DNL Azure] devi fornire il nome e la chiave primaria della regola di autorizzazione che regola lo spazio dei nomi o l’hub eventi specifico a cui desideri inviare i dati. Per informazioni dettagliate su come ottenere questi valori dal [!DNL Azure] , fare riferimento alle sezioni seguenti nel [!DNL Azure] documentazione:

* [Ottenere valori SAS per un [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Ottenere i valori SAS per un hub eventi specifico in uno spazio dei nomi](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Una volta ottenuti i valori richiesti, il nome della regola di autorizzazione può essere fornito direttamente come stringa nell&#39;input della configurazione oppure è possibile creare un elemento dati di tipo stringa per farvi riferimento. La chiave primaria, tuttavia, deve prima essere contenuta all&#39;interno di un segreto di inoltro dell&#39;evento prima che possa essere fornita nella configurazione della regola per proteggere la sicurezza dei dati.

Nell’interfaccia utente dell’inoltro eventi, [crea un nuovo segreto](../../../ui/event-forwarding/secrets.md) e seleziona **[!UICONTROL Token]** come tipo segreto. Per il valore del token stesso, fornisci la chiave primaria copiata in precedenza. Dopo aver creato il segreto, crea un elemento dati con il tipo **[!UICONTROL Segreto]** e seleziona la [!DNL Event Hubs] segreto dalla lista. Una volta configurato l’elemento dati segreto, puoi fare riferimento a tale elemento dati nel **[!UICONTROL Chiave di accesso SAS]** campo .
