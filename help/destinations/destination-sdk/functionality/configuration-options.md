---
description: Il servizio delle destinazioni in Adobe Experience Platform utilizza endpoint di configurazione per diversi componenti che creano la funzionalità delle destinazioni. Scopri come questi componenti combinati consentono ad Experience Platform di connettersi ai partner di destinazione, inviare messaggi personalizzati e attivare i dati del profilo nell’ecosistema digitale.
title: Opzioni di configurazione in Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: f652faac7d771b590b30f591616b53d0cd2ff1eb
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Opzioni di configurazione in Destination SDK

Il servizio delle destinazioni in Adobe Experience Platform utilizza endpoint di configurazione per diversi componenti che creano la funzionalità delle destinazioni.

La combinazione di questi componenti consente ad Experience Platform di connettersi alle piattaforme di destinazione, inviare messaggi personalizzati, esportare file personalizzati e attivare i dati del profilo nell’ecosistema digitale.

Il diagramma seguente mostra una panoramica ad alto livello dei componenti che è possibile configurare tramite Destination SDK per creare una destinazione personalizzata. Questi componenti sono descritti più avanti.

>[!BEGINSHADEBOX]

![Diagramma che mostra i componenti Destination SDK, gli endpoint di configurazione e le operazioni da essi supportate.](../assets/functionality/destination-sdk-components-diagram.png){zoomable="yes"}

>[!ENDSHADEBOX]

## Configurazione del server {#server-configuration}

La configurazione del server di destinazione unisce le informazioni sulle specifiche del server e i modelli utilizzati da Adobe per distribuire i payload alla destinazione.

Ad esempio, qui puoi specificare gli endpoint API lato a cui Experience Platform deve connettersi, nonché le intestazioni e il formato delle chiamate API che Platform effettuerà.

Per le destinazioni basate su file, questa configurazione include anche i formati di formattazione e compressione file supportati per la destinazione. Puoi configurare le funzionalità descritte di seguito tramite l&#39;endpoint [server di destinazione](../authoring-api/destination-server/create-destination-server.md).

* [Specifiche server](destination-server/server-specs.md): modello di configurazione che contiene informazioni sul percorso di archiviazione o sull&#39;endpoint HTTP a cui vengono inviati i dati.
* [Specifiche modello](destination-server/templating-specs.md): in questo modello, puoi definire come strutturare la richiesta API HTTP nell&#39;endpoint, incluso come trasformare i campi degli attributi del profilo tra lo schema XDM e il formato supportato dalla piattaforma. Utilizza queste informazioni insieme alla documentazione del [formato del messaggio](destination-server/message-format.md).
* [Formato del messaggio](destination-server/message-format.md): in questa sezione vengono trattate informazioni approfondite sui linguaggi di modelli supportati, i formati dei messaggi e le informazioni richieste dall&#39;Adobe per configurare l&#39;integrazione con la piattaforma. Utilizza queste informazioni insieme alla documentazione delle [specifiche modello](destination-server/templating-specs.md).
* [Specifiche file](destination-server/file-formatting.md): modello di configurazione che include le opzioni di formattazione e compressione del file per la destinazione batch.

## Configurazione della destinazione {#destination-configuration}

Questo endpoint di configurazione contiene informazioni di base e avanzate sulla destinazione. Ad esempio, è qui che puoi specificare i tipi di identità che la tua destinazione può supportare, il formato desiderato dei file esportati (per le destinazioni basate su file) e vari attributi dell’interfaccia utente per la scheda di destinazione nell’interfaccia utente di Adobe Experience Platform.

Per informazioni dettagliate su ciascuno dei componenti di configurazione di destinazione, consulta la documentazione riportata di seguito. Puoi configurare le funzionalità descritte di seguito tramite l&#39;endpoint [destinations](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configurazione autenticazione cliente](destination-configuration/customer-authentication.md): selezionare il meccanismo di autenticazione che Experience Platform deve utilizzare per connettersi alla destinazione. Questa configurazione genera la pagina [Configura nuova destinazione](../../ui/connect-destination.md) nell&#39;interfaccia utente di Experience Platform, in cui gli utenti connettono Experience Platform agli account di cui dispongono con la destinazione.
* [Autorizzazione OAuth2](destination-configuration/oauth2-authorization.md): scopri tutti i flussi di autenticazione [!DNL OAuth2] supportati da Destination SDK e ottieni istruzioni per configurare l&#39;autenticazione [!DNL OAuth2] per la tua destinazione.
* [Campi dati cliente](destination-configuration/customer-data-fields.md): scopri come creare campi di input nell&#39;interfaccia utente di Experience Platform che consentono agli utenti di specificare varie informazioni rilevanti per la connessione e l&#39;esportazione di dati nella destinazione.
* [Attributi dell&#39;interfaccia utente](destination-configuration/ui-attributes.md): scopri come configurare gli attributi dell&#39;interfaccia utente, ad esempio il collegamento alla documentazione, la categoria della scheda di destinazione e il tipo e la frequenza di connessione di destinazione, per le destinazioni create con Destination SDK.
* [Configurazione dello schema](destination-configuration/schema-configuration.md): scopri come definire lo schema di destinazione della tua destinazione in cui gli utenti possono mappare gli attributi e le identità del profilo.
* [Configurazione dello spazio dei nomi delle identità](destination-configuration/identity-namespace-configuration.md): scopri come configurare le identità supportate dalla destinazione. Questa configurazione popola le identità di destinazione nel [passaggio di mappatura](../../ui/activate-segment-streaming-destinations.md#mapping) dell&#39;interfaccia utente di Experience Platform, dove gli utenti mappano le identità e gli attributi dai loro schemi XDM allo schema nella destinazione.
* [Consegna di destinazione](destination-configuration/destination-delivery.md): scopri come configurare dove vanno esattamente i dati esportati e quale regola di autenticazione viene utilizzata nel percorso in cui verranno recapitati i dati.
* [Configurazione metadati pubblico](destination-configuration/audience-metadata-configuration.md): scopri come i metadati del pubblico, come nomi o ID di pubblico, devono essere condivisi tra Experience Platform e la destinazione.
* [Criteri di aggregazione](destination-configuration/aggregation-policy.md): scopri come impostare un criterio di aggregazione per determinare come raggruppare e raggruppare in batch le richieste HTTP nella destinazione.
* [Configurazione batch](destination-configuration/batch-configuration.md): configura varie impostazioni di denominazione ed esportazione dei file disponibili per gli utenti quando si connette alla destinazione nell&#39;interfaccia utente di Experience Platform.
* [Qualifiche di profilo cronologiche](destination-configuration/historical-profile-qualifications.md): scopri le qualifiche di profilo cronologiche supportate dalle destinazioni create con Destination SDK.

## Configurazione dei metadati del pubblico {#audience-metadata-configuration}

Questo componente consente di configurare il modo in cui i tipi di pubblico vengono creati, aggiornati o eliminati a livello di programmazione nella destinazione. Per le destinazioni basate su file, consente di impostare una notifica ogni volta che i file vengono consegnati correttamente alla destinazione. Puoi configurare questa funzionalità tramite l&#39;endpoint [modelli di pubblico](../metadata-api/create-audience-template.md).

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, avrai una panoramica generale delle funzionalità fornite da Destination SDK e delle pagine da leggere per ulteriori informazioni su configurazioni specifiche. È quindi possibile leggere le guide che includono tutti i passaggi per [configurare uno streaming](../guides/configure-destination-instructions.md) o una [destinazione basata su file](../guides/configure-file-based-destination-instructions.md) utilizzando Destination SDK.
