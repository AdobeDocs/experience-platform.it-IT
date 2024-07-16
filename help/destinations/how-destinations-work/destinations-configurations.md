---
title: Impostazioni di esportazione comuni e configurabili nelle destinazioni
description: Scopri quali impostazioni di esportazione nelle destinazioni sono configurabili a livello di destinazione e quali sono fisse e non possono essere modificate.
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: 47197b745bebb6564d912d9dc045593bc076ae2a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Impostazioni di esportazione comuni e configurabili nelle destinazioni

Quando pensi al comportamento di esportazione nelle destinazioni Experience Platform, devi considerare tre livelli separati su cui agiscono le configurazioni.

* Al primo livello, alcune delle impostazioni relative al comportamento di esportazione del profilo e alle impostazioni di configurazione sono comuni a tutte le destinazioni appartenenti a un tipo di destinazione. Queste impostazioni si riferiscono a ciò che attiva un’esportazione di destinazione e a ciò che è incluso in un’esportazione e non possono essere modificate dagli sviluppatori di destinazione o dagli utenti di Real-Time CDP.
* Al secondo livello, alcune impostazioni possono essere personalizzate a livello di destinazione dallo sviluppatore di destinazione durante l’authoring delle destinazioni utilizzando Destination SDK.
* Al terzo livello, è possibile configurare le impostazioni di configurazione impostate dagli utenti di Real-Time CDP nei flussi di lavoro di attivazione.

![Diagramma che mostra l&#39;interazione tra le impostazioni di esportazione comuni e configurabili per le destinazioni](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Questa pagina descrive o collega tutte le impostazioni di esportazione comuni e configurabili per le destinazioni, sui tre livelli descritti in precedenza.

## Impostazioni di esportazione comuni tra i tipi di destinazione {#common-settings-across-destination-types}

Il comportamento di esportazione della destinazione è coerente tra le destinazioni appartenenti a un tipo di destinazione per quanto riguarda *ciò che attiva un&#39;esportazione di destinazione* e *ciò che è incluso nelle esportazioni di destinazione*. Le esportazioni delle destinazioni vengono attivate dalle notifiche ricevute dal servizio [upstream Real-time Customer Profile](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

Ciò che è incluso nelle esportazioni di destinazione varia leggermente tra i tipi di destinazione. Ulteriori informazioni sui [modelli comuni di comportamento di esportazione per tipo di destinazione](/help/destinations/how-destinations-work/profile-export-behavior.md). Queste impostazioni non possono essere modificate dagli sviluppatori o dagli utenti di Real-Time CDP.

## Impostazioni di esportazione personalizzabili per sviluppatori di destinazione {#customizable-settings-by-destination-developers}

Gli sviluppatori di destinazione possono utilizzare [Destination SDK](/help/destinations/destination-sdk/overview.md) per creare destinazioni personalizzate o prodotte (private o pubbliche). Destination SDK offre agli sviluppatori una grande flessibilità per configurare le destinazioni in base alle funzionalità a valle dei loro endpoint API e dei sistemi di ricezione dei file. In base alle funzionalità a valle, gli sviluppatori di destinazione dispongono delle seguenti opzioni di configurazione quando configurano una destinazione utilizzando Destination SDK:

* Determina quali attributi e identità possono essere esportati da Experience Platform alla destinazione. Determina anche quali identità sono richieste dalle loro destinazioni per una corretta esportazione dei dati.
* Imposta un criterio di aggregazione che determina il tempo di attesa dell’Experience Platform durante l’aggregazione dei messaggi HTTP da inviare alle integrazioni API. Gli sviluppatori di destinazione possono configurare diversi tipi di aggregazione per determinare quanti profili devono essere inclusi nei messaggi HTTP in uscita e per quanto tempo l’Experience Platform deve attendere fino all’invio del messaggio HTTP. Per informazioni dettagliate sulle [opzioni di configurazione dei criteri di aggregazione](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) disponibili per gli sviluppatori di destinazione, consulta la documentazione di Destination SDK.
* Determina se le esportazioni di messaggi HTTP devono includere profili idonei per i segmenti, rimossi dai segmenti o entrambi.
* Determinare il nome e le configurazioni di formattazione dei file da rendere disponibili agli utenti durante l&#39;esportazione dei file.

## Impostazioni a livello di flusso di dati personalizzabili dagli utenti {#settings-on-dataflow-level}

Oltre alle impostazioni non modificabili che dipendono dal tipo di destinazione e dalle impostazioni configurate dallo sviluppatore di destinazione, nel flusso di lavoro di attivazione è possibile configurare alcune impostazioni di esportazione. Queste impostazioni si riferiscono alla pianificazione dell’esportazione di un determinato flusso di dati in una destinazione, agli attributi e ai campi di identità da esportare in un flusso di dati o alle opzioni di formattazione dei file per i file esportati.

Le impostazioni disponibili per gli utenti durante la connessione a una destinazione dipendono dalla configurazione della destinazione da parte dello sviluppatore e dalle impostazioni rese disponibili agli utenti.

Ad esempio, per [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations), uno sviluppatore di destinazione può configurare quali identità accetta la propria destinazione e solo quelle identità verranno visualizzate all&#39;utente in [passaggio di mappatura del flusso di lavoro di attivazione](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), come mostrato di seguito:

![Registrazione schermata della selezione identità per il campo di destinazione nel passaggio di mappatura del flusso di lavoro di attivazione. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

Analogamente, per [destinazioni basate su file](/help/destinations/destination-types.md#file-based), lo sviluppatore di destinazione può determinare quali [opzioni di aggiunta del nome file](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) desidera rendere disponibili per la propria destinazione o quali [opzioni di formattazione file](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) desidera rendere disponibili e l&#39;utente potrà selezionare solo tra queste opzioni, come illustrato di seguito:

![Registrazione dello schermo dell&#39;opzione di formattazione del file durante la connessione a una destinazione basata su file.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Registrazione dello schermo dell&#39;opzione di aggiunta del nome file nel passaggio di pianificazione del flusso di lavoro di attivazione. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Ulteriori informazioni sulle diverse opzioni e passaggi disponibili nel flusso di lavoro di attivazione:

* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Attivare i dati sul pubblico nelle destinazioni Enterprise](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Esporta file on-demand in destinazioni batch](/help/destinations/ui/export-file-now.md)
* [Esportare i set di dati nelle destinazioni dell’archiviazione cloud](/help/destinations/ui/export-datasets.md)

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, sai quali impostazioni di esportazione per le destinazioni sono comuni tra i tipi di destinazione, quali possono essere configurate a livello di singola destinazione dagli sviluppatori e quali impostazioni possono essere modificate dagli utenti nel flusso di lavoro di attivazione.

Quindi, puoi leggere informazioni più dettagliate sui [modelli comuni di comportamento di esportazione per tipo di destinazione](/help/destinations/how-destinations-work/profile-export-behavior.md).

Per gli sviluppatori di destinazione, puoi [iniziare](/help/destinations/destination-sdk/getting-started.md) con Destination SDK. Per gli utenti che cercano di attivare i dati, puoi estrarre tutte le destinazioni disponibili nel [catalogo](/help/destinations/catalog/overview.md).
