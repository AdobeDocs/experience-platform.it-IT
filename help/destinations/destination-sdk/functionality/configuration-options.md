---
description: Il servizio Destinazioni in Adobe Experience Platform utilizza gli endpoint di configurazione per diversi componenti che generano la funzionalità Destinazioni. Scopri come questi componenti combinati consentono ad Experience Platform di connettersi ai partner di destinazione, inviare messaggi personalizzati e attivare i dati di profilo nell’ecosistema digitale.
title: Opzioni di configurazione in Destination SDK
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# Opzioni di configurazione in Destination SDK

Il servizio Destinazioni in Adobe Experience Platform utilizza gli endpoint di configurazione per diversi componenti che generano la funzionalità Destinazioni.

Combinati, questi componenti consentono ad Experience Platform di connettersi alle piattaforme di destinazione, inviare messaggi personalizzati, esportare file personalizzati e attivare i dati di profilo nell’ecosistema digitale.

Il diagramma seguente mostra una panoramica di alto livello dei componenti che puoi configurare tramite Destination SDK per creare una tua destinazione. Questi componenti sono descritti più avanti.

![Diagramma che mostra i componenti Destination SDK, gli endpoint di configurazione e le operazioni da essi supportate.](../assets/functionality/destination-sdk-components-diagram.png)

## Configurazione del server {#server-configuration}

La configurazione del server di destinazione unisce le informazioni sulle specifiche del server e sul modello utilizzato da Adobe per distribuire i payload alla destinazione.

Ad esempio, in questo punto puoi specificare gli endpoint API sul tuo lato a cui Experience Platform deve connettersi, nonché le intestazioni e il formato delle chiamate API che Platform effettuerà.

Per le destinazioni basate su file, questa configurazione include anche i formati di formattazione e compressione supportati per la destinazione. Puoi configurare le funzionalità descritte di seguito tramite la [endpoint server di destinazione](../authoring-api/destination-server/create-destination-server.md).

* [Specifiche del server](destination-server/server-specs.md): Modello di configurazione che contiene informazioni sulla posizione di archiviazione o sull&#39;endpoint HTTP a cui vengono inviati i dati.
* [Specifiche dei modelli](destination-server/templating-specs.md): In questo modello, puoi definire la struttura della richiesta API HTTP all’endpoint, incluso come trasformare i campi dell’attributo del profilo tra lo schema XDM e il formato supportato dalla piattaforma. Utilizza queste informazioni insieme al [formato messaggio](destination-server/message-format.md) documentazione.
* [Formato del messaggio](destination-server/message-format.md): Questa sezione contiene informazioni approfondite sulle lingue di template supportate, sui formati dei messaggi e sulle informazioni richieste da Adobe per configurare l&#39;integrazione con la piattaforma. Utilizza queste informazioni insieme al [specifiche del modello](destination-server/templating-specs.md) documentazione.
* [Specifiche dei file](destination-server/file-formatting.md): Un modello di configurazione che include le opzioni di formattazione e compressione del file per la destinazione batch.

## Configurazione della destinazione {#destination-configuration}

Questo endpoint di configurazione contiene informazioni di base e avanzate sulla destinazione. Ad esempio, in questo punto è possibile specificare i tipi di identità supportati dalla destinazione, il formato desiderato dei file esportati (per le destinazioni basate su file) e vari attributi di interfaccia utente per la scheda di destinazione nell’interfaccia utente di Adobe Experience Platform.

Per informazioni dettagliate su ciascuno dei componenti di configurazione di destinazione, consulta la documentazione riportata di seguito. Puoi configurare le funzionalità descritte di seguito tramite la [endpoint destinazioni](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configurazione dell’autenticazione cliente](destination-configuration/customer-authentication.md): Seleziona il meccanismo di autenticazione da utilizzare in Experience Platform per connettersi alla destinazione. Questa configurazione genera [Configurare una nuova destinazione](../../ui/connect-destination.md) nell’interfaccia utente di Experience Platform, in cui gli utenti collegano Experience Platform agli account che hanno con la tua destinazione.
* [Autenticazione OAuth2](destination-configuration/oauth2-authentication.md): Scopri tutte le [!DNL OAuth2] flussi di autenticazione supportati da Destination SDK e ottenere istruzioni per la configurazione [!DNL OAuth2] autenticazione per la destinazione..
* [Campi dati cliente](destination-configuration/customer-data-fields.md): Scopri come creare campi di input nell’interfaccia utente di Experience Platform per consentire agli utenti di specificare varie informazioni relative alla modalità di connessione ed esportazione dei dati verso la destinazione.
* [Attributi dell&#39;interfaccia utente](destination-configuration/ui-attributes.md): Scopri come configurare gli attributi dell’interfaccia utente, ad esempio il collegamento alla documentazione, la categoria della scheda di destinazione e il tipo di connessione e la frequenza di destinazione, per le destinazioni create con Destination SDK.
* [Configurazione dello schema](destination-configuration/schema-configuration.md): Scopri come definire lo schema di destinazione della destinazione in cui gli utenti possono mappare attributi e identità di profilo.
* [Configurazione dello spazio dei nomi identità](destination-configuration/identity-namespace-configuration.md): Scopri come configurare le identità supportate dalla destinazione. Questa configurazione popola le identità di destinazione nel [fase di mappatura](../../ui/activate-segment-streaming-destinations.md#mapping) dell’interfaccia utente di Experience Platform, in cui gli utenti mappano identità e attributi dai loro schemi XDM allo schema di destinazione.
* [Consegna delle destinazioni](destination-configuration/destination-delivery.md): Scopri come configurare esattamente dove vanno i dati esportati e quale regola di autenticazione viene utilizzata nel percorso in cui i dati verranno inviati.
* [Configurazione dei metadati del pubblico](destination-configuration/audience-metadata-configuration.md): Scopri come i metadati dei segmenti, come i nomi dei segmenti o gli ID, devono essere condivisi tra l’Experience Platform e la destinazione.
* [Criteri di aggregazione](destination-configuration/aggregation-policy.md): Scopri come impostare un criterio di aggregazione per determinare in che modo raggruppare e gestire le richieste HTTP nella destinazione.
* [Configurazione batch](destination-configuration/batch-configuration.md): Configura le varie impostazioni di denominazione dei file ed esportazione disponibili per gli utenti quando ti connetti alla tua destinazione nell’interfaccia utente di Experience Platform.
* [Qualifiche di profilo storiche](destination-configuration/historical-profile-qualifications.md): Scopri le qualifiche di profilo storiche supportate dalle destinazioni create con Destination SDK.

## Configurazione dei metadati del pubblico {#audience-metadata-configuration}

Questo componente consente di configurare il modo in cui i tipi di pubblico/segmenti vengono creati, aggiornati o eliminati a livello di programmazione nella destinazione. Per le destinazioni basate su file, ti consente di impostare una notifica ogni volta che i file vengono consegnati correttamente alla tua destinazione. Puoi configurare questa funzionalità tramite [endpoint modelli di pubblico](../metadata-api/create-audience-template.md).

## Passaggi successivi {#next-steps}

Leggendo questo articolo, disponi ora di una panoramica generale delle funzionalità fornite da Destination SDK e delle pagine da leggere per ulteriori informazioni sulle configurazioni specifiche. Successivamente, puoi leggere le guide che includono tutti i passaggi per [configurare uno streaming](../guides/configure-destination-instructions.md) o [destinazione basata su file](../guides/configure-file-based-destination-instructions.md) utilizzando la Destination SDK.
