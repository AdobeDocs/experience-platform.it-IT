---
title: Panoramica dell’estensione Microsoft Azure
description: Scopri l’estensione Microsoft Azure per l’inoltro degli eventi in Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 3%

---

# [!DNL Microsoft Azure] panoramica dell’estensione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

In entrata [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) è un servizio di inserimento dati altamente scalabile e in tempo reale che consente di elaborare e analizzare l&#39;enorme quantità di dati prodotti dai dispositivi e dalle applicazioni collegati. Una volta raccolti i dati in un hub eventi, questi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/archiviazione.

Il [!DNL Microsoft Azure] [inoltro eventi](../../../ui/event-forwarding/overview.md) l&#39;estensione sfrutta [!DNL Event Hubs] per inviare eventi da Adobe Experience Platform Edge Network a [!DNL Azure] per ulteriore elaborazione. Questa guida illustra come installare l’estensione e utilizzarne le funzionalità in una regola di inoltro degli eventi.

## Prerequisiti

Per utilizzare questa estensione, è necessario disporre di un [!DNL Azure] account con accesso a [!DNL Event Hubs]. È inoltre necessario [creare un hub eventi utilizzando [!DNL Azure] portale](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) prima di seguire i passaggi seguenti.

## Installare l’estensione

Per installare Microsoft [!DNL Azure] , passa all’interfaccia utente di Data Collection o all’interfaccia utente di Experience Platform e seleziona **[!UICONTROL Inoltro eventi]** dal menu di navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione o creane una nuova.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seleziona quindi **[!UICONTROL Catalogo]** scheda. Cerca [!UICONTROL Microsoft Azure] , quindi seleziona **[!UICONTROL Installa]**.

![Il [!UICONTROL Installa] pulsante selezionato per il [!UICONTROL Microsoft Azure] nell’interfaccia utente di Data Collection.](../../../images/extensions/server/azure/install.png)

Poiché l&#39;estensione non dispone di proprietà di configurazione, viene aggiunta immediatamente all&#39;elenco delle estensioni installate. Ora puoi iniziare a utilizzare [!DNL Event Hub] tipi di azioni durante la configurazione delle regole di inoltro degli eventi.

## Configurare una regola di inoltro degli eventi {#rule}

Inizia a creare una nuova regola di inoltro degli eventi e configurane le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona **[!UICONTROL Microsoft Azure]** per l’estensione, seleziona **[!UICONTROL Invia dati a hub eventi]** per il tipo di azione.

![Il [!UICONTROL Invia dati a hub eventi] tipo di azione selezionato per una regola nell’interfaccia utente di Data Collection.](../../../images/extensions/server/azure/select-action-type.png)

Il pannello a destra si aggiorna per mostrare le opzioni di configurazione per la modalità di invio dei dati. In particolare, devi assegnare [elementi dati](../../../ui/managing-resources/data-elements.md) alle varie proprietà che rappresentano [!DNL Event Hub] configurazione.

![Le opzioni di configurazione per [!UICONTROL Invia dati a hub eventi] tipo di azione visualizzato nell’interfaccia utente.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Dettagli hub eventi]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Spazio dei nomi] | Il nome del [!DNL Event Hubs] spazio dei nomi creato quando [configurazione dell’hub eventi](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Nome] | Nome dell’hub eventi. |
| [!UICONTROL Nome regola di autorizzazione SAS] | Nome della regola di autorizzazione di accesso condiviso per l&#39;intero [!DNL Event Hubs] spazio dei nomi o istanza hub eventi specifica a cui si desidera inviare i dati. Vedere la sezione dell&#39;appendice relativa a [recupero dei valori di autorizzazione SAS](#sas) per ulteriori informazioni. |
| [!UICONTROL Chiave di accesso SAS] | Chiave primaria della regola di autorizzazione di accesso condiviso per l&#39;intero [!DNL Event Hubs] spazio dei nomi o istanza hub eventi specifica a cui si desidera inviare i dati. Vedere la sezione dell&#39;appendice relativa a [recupero dei valori di autorizzazione SAS](#sas) per ulteriori informazioni. |
| [!UICONTROL ID partizione] | [!DNL Event Hubs] consente di: [inviare eventi direttamente a partizioni specifiche](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Per sfruttare questa funzione, fornisci l’ID della partizione a cui desideri inviare gli eventi. |

{style="table-layout:auto"}

**Dati**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Payload] | Questo campo contiene i dati che verranno inoltrati al [!DNL Event Hubs]. I dati possono essere un oggetto JSON, una stringa o un elemento dati. |

{style="table-layout:auto"}

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l’azione alla configurazione della regola. Quando sei soddisfatto della regola, seleziona **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo inoltro di eventi [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Event Hubs] utilizzando [!DNL Microsoft Azure] estensione di inoltro degli eventi. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experience Platform, consulta [panoramica sull’inoltro degli eventi](../../../ui/event-forwarding/overview.md).

## Appendice: ottenere i valori di autorizzazione SAS {#sas}

Le applicazioni esterne possono accedere a [!DNL Event Hubs] da a [firme di accesso condiviso (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Ogni [!DNL Event Hubs] All&#39;istanza di namespace e hub eventi viene assegnata automaticamente una regola di autorizzazione SAS predefinita al momento della creazione, ma è anche possibile creare criteri aggiuntivi per ogni risorsa.

Quando [configurazione di una regola di inoltro degli eventi](#rule) utilizzando [!DNL Azure] devi fornire il nome e la chiave primaria per la regola di autorizzazione che disciplina lo spazio dei nomi o l’hub eventi specifico a cui desideri inviare i dati. Per informazioni dettagliate su come ottenere questi valori da [!DNL Azure] portale, fare riferimento alle sezioni seguenti nella [!DNL Azure] documentazione:

* [Ottenere valori SAS per un [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Ottenere valori SAS per un hub evento specifico in uno spazio dei nomi](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Una volta ottenuti i valori richiesti, il nome della regola di autorizzazione può essere fornito direttamente come stringa nell’input di configurazione oppure puoi creare un elemento dati di tipo stringa a cui fare riferimento. La chiave primaria, tuttavia, deve prima essere contenuta all’interno di un segreto di inoltro degli eventi prima di poter essere fornita nella configurazione della regola per proteggere la sicurezza dei dati.

Nell’interfaccia utente per l’inoltro degli eventi, [crea un nuovo segreto](../../../ui/event-forwarding/secrets.md) e seleziona **[!UICONTROL Token]** come tipo segreto. Per il valore del token stesso, specifica la chiave primaria copiata in precedenza. Dopo aver creato il segreto, crea un elemento dati con il tipo **[!UICONTROL Segreto]** e seleziona la [!DNL Event Hubs] segreto dall&#39;elenco. Una volta configurato l’elemento dati segreto, puoi farvi riferimento in **[!UICONTROL Chiave di accesso SAS]** campo.
