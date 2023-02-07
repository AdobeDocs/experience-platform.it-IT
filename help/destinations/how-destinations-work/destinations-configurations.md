---
title: Impostazioni di esportazione comuni e configurabili nelle destinazioni
description: Scopri quali impostazioni di esportazione nelle destinazioni sono configurabili a livello di destinazione e quali sono fisse e non possono essere modificate.
source-git-commit: 372231ab4fc1148c1c2c0c5fdbfd3cd5328b17cc
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---


# Impostazioni di esportazione comuni e configurabili nelle destinazioni

Quando pensi al comportamento di esportazione nelle destinazioni di Experience Platform, devi considerare tre livelli separati su cui agiscono le configurazioni.

* A un primo livello, alcune delle impostazioni relative al comportamento di esportazione del profilo e alle impostazioni di configurazione sono comuni tra tutte le destinazioni appartenenti a un tipo di destinazione. Queste impostazioni fanno riferimento a ciò che attiva un’esportazione di destinazione e a ciò che è incluso in un’esportazione e non può essere modificato dagli sviluppatori di destinazione o dagli utenti Real-time CDP.
* Su un secondo livello, alcune impostazioni possono essere personalizzate a livello di destinazione dallo sviluppatore di destinazione quando si creano destinazioni utilizzando Destination SDK.
* Su un terzo livello, ci sono impostazioni di configurazione che gli utenti Real-time CDP possono impostare nei flussi di lavoro di attivazione.

![Diagramma che mostra l’interazione tra le impostazioni di esportazione comuni e configurabili per le destinazioni](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Questa pagina descrive o effettua un collegamento a tutte le impostazioni di esportazione comuni e configurabili per le destinazioni, ai tre livelli sopra descritti.

## Impostazioni di esportazione comuni tra i tipi di destinazione {#common-settings-across-destination-types}

Il comportamento di esportazione della destinazione è coerente tra le destinazioni appartenenti a un tipo di destinazione per quanto riguarda *che attiva un’esportazione di destinazione* e *che cosa è incluso nelle esportazioni di destinazione*. Le esportazioni di destinazione vengono attivate dalle notifiche ricevute dal servizio di destinazione dal [servizio Profilo cliente in tempo reale a monte](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

Ciò che è incluso nelle esportazioni di destinazione varia leggermente tra i tipi di destinazione. Ulteriori informazioni sulle [modelli comuni di comportamento per le esportazioni per tipo di destinazione](/help/destinations/how-destinations-work/profile-export-behavior.md). Queste impostazioni non possono essere modificate dagli sviluppatori di destinazione o dagli utenti Real-time CDP.

## Impostazioni di esportazione personalizzabili per sviluppatori di destinazione {#customizable-settings-by-destination-developers}

Gli sviluppatori di destinazione possono utilizzare [Destination SDK](/help/destinations/destination-sdk/overview.md) per creare destinazioni personalizzate o prodotte (private o pubbliche). Destination SDK offre agli sviluppatori una grande flessibilità per configurare le destinazioni in base alle funzionalità a valle degli endpoint API e dei sistemi di ricezione dei file. In base alle funzionalità downstream, gli sviluppatori di destinazione hanno le seguenti opzioni di configurazione disponibili quando configurano una destinazione utilizzando Destination SDK:

* Determina quali attributi e identità possono essere esportati fuori dall’Experience Platform nella destinazione. Stabilire inoltre quali identità sono richieste dalle rispettive destinazioni per un’esportazione di dati corretta.
* Imposta un criterio di aggregazione, che determina per quanto tempo Experience Platform deve aspettare quando si aggregano i messaggi HTTP da inviare alle integrazioni API. Gli sviluppatori di destinazione possono configurare diversi tipi di aggregazione per determinare quanti profili devono essere inclusi nei messaggi HTTP in uscita e per quanto tempo Experience Platform deve attendere l’invio del messaggio HTTP. Trova informazioni complete sui [opzioni di configurazione dei criteri di aggregazione](/help/destinations/destination-sdk/destination-configuration.md#aggregation) disponibile per gli sviluppatori di destinazione nella documentazione Destination SDK.
* Determina se le esportazioni di messaggi HTTP devono includere profili qualificati per i segmenti, che vengono rimossi dai segmenti o da entrambi.
* Determinare quali configurazioni di file e formattazione devono essere disponibili per gli utenti durante l&#39;esportazione dei file.

## Impostazioni su un livello di flusso di dati personalizzabile dagli utenti {#settings-on-dataflow-level}

Oltre alle impostazioni non modificabili che dipendono dal tipo di destinazione e dalle impostazioni configurate dallo sviluppatore di destinazione, nel flusso di lavoro di attivazione gli utenti possono configurare alcune impostazioni di esportazione. Queste impostazioni si riferiscono alla pianificazione per l’esportazione di un determinato flusso di dati in una destinazione, agli attributi e ai campi di identità da esportare in un flusso di dati o alle opzioni di formattazione per i file esportati.

Le impostazioni disponibili per gli utenti che si connettono a una destinazione dipendono da come lo sviluppatore della destinazione ha configurato la destinazione e quali impostazioni hanno reso disponibili agli utenti.

Ad esempio, [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations), uno sviluppatore di destinazione può configurare quali identità accetta dalla propria destinazione e solo tali identità verranno visualizzate all&#39;utente in [fase di mappatura del flusso di lavoro di attivazione](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), come illustrato di seguito:

![Registrazione su schermo della selezione di identità per il campo di destinazione nella fase di mappatura del flusso di lavoro di attivazione. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

Analogamente, per [destinazioni basate su file](/help/destinations/destination-types.md#file-based), lo sviluppatore di destinazione può determinare quali [opzioni di aggiunta nome file](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) che desiderano mettere a disposizione per la loro destinazione o quali [opzioni di formattazione dei file](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) desiderano rendere disponibili e l’utente potrà selezionare solo tra queste opzioni, come illustrato di seguito:

![Registrazione su schermo dell&#39;opzione di formattazione del file quando ci si connette a una destinazione basata su file.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Registrazione su schermo dell’opzione di aggiunta del nome file nella fase di pianificazione del flusso di lavoro di attivazione. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Ulteriori informazioni sulle diverse opzioni e passaggi disponibili nel flusso di lavoro di attivazione:

* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni aziendali](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Esportare file on-demand in destinazioni batch](/help/destinations/ui/export-file-now.md)
* [(Beta) Esportare i set di dati nelle destinazioni di archiviazione cloud](/help/destinations/ui/export-datasets.md)

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai quali impostazioni di esportazione per le destinazioni sono comuni tra i tipi di destinazione, che possono essere configurate a livello di destinazione individuale dagli sviluppatori e quali impostazioni possono essere modificate dagli utenti nel flusso di lavoro di attivazione.

Successivamente, puoi leggere informazioni più dettagliate su [modelli comuni di comportamento per le esportazioni per tipo di destinazione](/help/destinations/how-destinations-work/profile-export-behavior.md).

Per gli sviluppatori di destinazioni, puoi [introduzione](/help/destinations/destination-sdk/getting-started.md) con Destination SDK. Per gli utenti che desiderano attivare i dati, puoi estrarre tutte le destinazioni disponibili nella [catalogo](/help/destinations/catalog/overview.md).