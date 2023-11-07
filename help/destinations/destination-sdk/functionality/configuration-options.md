---
description: Il servizio delle destinazioni in Adobe Experience Platform utilizza endpoint di configurazione per diversi componenti che creano la funzionalità delle destinazioni. Scopri come questi componenti combinati consentono ad Experienci Platform di connettersi ai partner di destinazione, inviare messaggi personalizzati e attivare i dati del profilo nell’ecosistema digitale.
title: Opzioni di configurazione in Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Opzioni di configurazione in Destination SDK

Il servizio delle destinazioni in Adobe Experience Platform utilizza endpoint di configurazione per diversi componenti che creano la funzionalità delle destinazioni.

La combinazione di questi componenti consente ad Experienci Platform di connettersi alle piattaforme di destinazione, inviare messaggi personalizzati, esportare file personalizzati e attivare i dati del profilo nell’ecosistema digitale.

Il diagramma seguente mostra una panoramica ad alto livello dei componenti che è possibile configurare tramite Destination SDK per creare una destinazione personalizzata. Questi componenti sono descritti più avanti.

![Diagramma che mostra i componenti Destination SDK, gli endpoint di configurazione e le operazioni supportate.](../assets/functionality/destination-sdk-components-diagram.png)

## Configurazione del server {#server-configuration}

La configurazione del server di destinazione unisce le informazioni sulle specifiche del server e i modelli utilizzati da Adobe per distribuire i payload alla destinazione.

Ad esempio, qui puoi specificare gli endpoint API lato a cui Experienci Platform deve connettersi, nonché le intestazioni e il formato delle chiamate API che Platform effettuerà.

Per le destinazioni basate su file, questa configurazione include anche i formati di formattazione e compressione file supportati per la destinazione. Puoi configurare le funzionalità descritte di seguito tramite la [endpoint destinazione-server](../authoring-api/destination-server/create-destination-server.md).

* [Specifiche del server](destination-server/server-specs.md): modello di configurazione che contiene informazioni sulla posizione di archiviazione o sull’endpoint HTTP a cui vengono inviati i dati.
* [Specifiche modello](destination-server/templating-specs.md): in questo modello, puoi definire come strutturare la richiesta API HTTP nell’endpoint, incluso come trasformare i campi dell’attributo del profilo tra lo schema XDM e il formato supportato dalla piattaforma. Utilizzare queste informazioni insieme a [formato del messaggio](destination-server/message-format.md) documentazione.
* [Formato del messaggio](destination-server/message-format.md): questa sezione descrive informazioni approfondite sui linguaggi di creazione di modelli supportati, sui formati di messaggio e sulle informazioni richieste da Adobe per configurare l’integrazione con la piattaforma. Utilizzare queste informazioni insieme a [specifiche del modello](destination-server/templating-specs.md) documentazione.
* [Specifiche dei file](destination-server/file-formatting.md): modello di configurazione che include le opzioni di formattazione e compressione del file per la destinazione batch.

## Configurazione della destinazione {#destination-configuration}

Questo endpoint di configurazione contiene informazioni di base e avanzate sulla destinazione. Ad esempio, è qui che puoi specificare i tipi di identità che la tua destinazione può supportare, il formato desiderato dei file esportati (per le destinazioni basate su file) e vari attributi dell’interfaccia utente per la scheda di destinazione nell’interfaccia utente di Adobe Experience Platform.

Per informazioni dettagliate su ciascuno dei componenti di configurazione di destinazione, consulta la documentazione riportata di seguito. Puoi configurare le funzionalità descritte di seguito tramite la [endpoint destinazioni](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configurazione autenticazione cliente](destination-configuration/customer-authentication.md): seleziona il meccanismo di autenticazione che Experienci Platform deve utilizzare per connettersi alla destinazione. Questa configurazione genera il [Configurare una nuova destinazione](../../ui/connect-destination.md) nell’interfaccia utente di Experienci Platform, in cui gli utenti connettono Experienci Platform agli account che hanno con la tua destinazione.
* [Autorizzazione OAuth2](destination-configuration/oauth2-authorization.md): scopri tutte le [!DNL OAuth2] flussi di autenticazione supportati da Destination SDK e istruzioni per la configurazione [!DNL OAuth2] autenticazione per la destinazione.
* [Campi dati cliente](destination-configuration/customer-data-fields.md): scopri come creare campi di input nell’interfaccia utente di Experienci Platform che consentono agli utenti di specificare varie informazioni rilevanti per la connessione e l’esportazione di dati nella destinazione.
* [Attributi dell’interfaccia utente](destination-configuration/ui-attributes.md): scopri come configurare gli attributi dell’interfaccia utente, ad esempio il collegamento alla documentazione, la categoria della scheda di destinazione e il tipo e la frequenza di connessione della destinazione, per le destinazioni create con Destination SDK.
* [Configurazione dello schema](destination-configuration/schema-configuration.md): scopri come definire lo schema di destinazione della destinazione in cui gli utenti possono mappare gli attributi e le identità del profilo.
* [Configurazione dello spazio dei nomi dell’identità](destination-configuration/identity-namespace-configuration.md): scopri come configurare le identità supportate dalla destinazione. Questa configurazione popola le identità di destinazione in [passaggio di mappatura](../../ui/activate-segment-streaming-destinations.md#mapping) dell’interfaccia utente di Experience Platform, in cui gli utenti mappano identità e attributi dai loro schemi XDM allo schema nella destinazione.
* [Consegna della destinazione](destination-configuration/destination-delivery.md): scopri come configurare esattamente dove vanno i dati esportati e quale regola di autenticazione viene utilizzata nella posizione in cui verranno recapitati i dati.
* [Configurazione dei metadati del pubblico](destination-configuration/audience-metadata-configuration.md): scopri come condividere metadati del pubblico come nomi di pubblico o ID tra Experienci Platform e la tua destinazione.
* [Criterio di aggregazione](destination-configuration/aggregation-policy.md): scopri come impostare un criterio di aggregazione per determinare come raggruppare e raggruppare in batch le richieste HTTP per la destinazione.
* [Configurazione batch](destination-configuration/batch-configuration.md): imposta le varie impostazioni di denominazione ed esportazione dei file disponibili per gli utenti quando si connette alla destinazione nell’interfaccia utente di Experienci Platform.
* [Qualifiche del profilo storico](destination-configuration/historical-profile-qualifications.md): scopri le qualifiche storiche dei profili supportate dalle destinazioni create con Destination SDK.

## Configurazione dei metadati del pubblico {#audience-metadata-configuration}

Questo componente consente di configurare il modo in cui i tipi di pubblico vengono creati, aggiornati o eliminati a livello di programmazione nella destinazione. Per le destinazioni basate su file, consente di impostare una notifica ogni volta che i file vengono consegnati correttamente alla destinazione. È possibile configurare questa funzionalità tramite [endpoint &quot;audience-templates&quot;](../metadata-api/create-audience-template.md).

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, avrai una panoramica generale delle funzionalità fornite da Destination SDK e delle pagine da leggere per ulteriori informazioni su configurazioni specifiche. Quindi, puoi leggere le guide che includono tutti i passaggi per [configurare uno streaming](../guides/configure-destination-instructions.md) o un [destinazione basata su file](../guides/configure-file-based-destination-instructions.md) utilizzando Destination SDK.
