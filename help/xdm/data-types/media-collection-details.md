---
title: Tipo di dati Dettagli raccolta multimediale
description: Scopri il tipo di dati Dettagli raccolta multimediale Experience Data Model (XDM).
exl-id: 1faf60f7-6afb-4ce2-b50d-967776a57715
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# [!UICONTROL Dettagli raccolta multimediale] tipo di dati

[!UICONTROL Dettagli raccolta file multimediali] è un tipo di dati Experience Data Model (XDM) standard che acquisisce dettagli essenziali sugli eventi di riproduzione di file multimediali. Utilizza il tipo di dati [!UICONTROL Dettagli raccolta file multimediali] per acquisire dettagli quali, tra gli altri, la posizione della testina di riproduzione all&#39;interno del contenuto, identificatori di sessione univoci e varie proprietà nidificate correlate alla sessione. Questo tipo di dati fornisce una panoramica completa dell’esperienza di riproduzione che consente il tracciamento e l’analisi dei modelli di consumo dei contenuti multimediali e degli eventi associati durante le sessioni di riproduzione.

>[!NOTE]
>
>I campi di Media Collection acquisiscono i dati e li inviano ad altri servizi Adobe per un’ulteriore elaborazione. I servizi Adobe utilizzano i campi di Media Reporting per analizzare i campi di Media Collection inviati dagli utenti. Questi dati, insieme ad altre metriche utente specifiche, vengono calcolati e segnalati.

+++Selezionare questa opzione per visualizzare un diagramma del tipo di dati [!UICONTROL Dettagli raccolta multimediale].
![Diagramma del tipo di dati [!UICONTROL Informazioni sui dettagli di Media Collection].](../images/data-types/media-collection-details.png)
+++

| Nome visualizzato | Proprietà | Eventi necessari per | Tipo di dati | Descrizione |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL Dettagli Advertising] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] - Raccolta](./advertising-details-collection.md) | I dettagli di Advertising si riferiscono a informazioni specifiche relative alle attività pubblicitarie durante l’evento esperienza. Ciò include metadati di annunci, specifiche di targeting e metriche delle prestazioni. |
| [!UICONTROL Dettagli pod Advertising] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] - Raccolta](./advertising-pod-details-collection.md) | I Dettagli del pod di Advertising contengono informazioni sui pod di annunci all’interno dell’evento esperienza. Fornisce informazioni approfondite sulla sequenza degli annunci, sui contenuti e sulle metriche di coinvolgimento. |
| [!UICONTROL Dettagli capitolo] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] - Raccolta](./chapter-details-collection.md) | Dettagli capitolo acquisisce i dati relativi ai capitoli o alle parti segmentate del contenuto. Fornisce informazioni sui marcatori capitolo, le timeline e i metadati associati. |
| [!UICONTROL Dettagli errore] | `errorDetails` | `error` | [[!UICONTROL errorDetails] - Raccolta](./error-details-collection.md) | I Dettagli errore contengono informazioni relative agli errori riscontrati durante l’evento esperienza. Ciò include codici di errore, descrizioni, marche temporali e dati contestuali pertinenti. |
| [!UICONTROL Fine Elenco Stati] | `statesEnd` | Utilizzato in `statesUpdate` | [[!UICONTROL statesEnd] - Raccolta](./list-of-states-end-collection.md) | State End fornisce un array per elencare gli stati alla conclusione dell’evento esperienza. Contiene dettagli sugli stati di riproduzione finali o sullo stato del contenuto. |
| [!UICONTROL Inizio Elenco Stati] | `statesStart` | Utilizzato in `statesUpdate` | [[!UICONTROL statesStart] - Raccolta](./list-of-states-start-collection.md) | State Start fornisce un array per elencare gli stati all’inizio dell’evento esperienza. Sono disponibili dati relativi alla riproduzione, alle azioni dell’utente o alle specifiche del contenuto. |
| [!UICONTROL Dettagli dati Qoe] | `qoeDataDetails` | Facoltativo per tutti | [[!UICONTROL qoeDataDetails] - Raccolta](./qoe-data-details-collection.md) | I dettagli dei dati QoE (Quality of Experience) acquisiscono metriche relative alle prestazioni e dati sull&#39;esperienza utente. Fornisce informazioni approfondite sulla qualità, la reattività e le interazioni degli utenti. |
| [!UICONTROL Dettagli sessione] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] - Raccolta](./session-details-collection.md) | I dettagli della sessione includono informazioni complete associate all’evento esperienza, che offrono informazioni approfondite sulle interazioni degli utenti, sulla durata e sui dati contestuali relativi alla sessione di riproduzione. |
| [!UICONTROL Metadati Personalizzati] | `customMetadata` | Facoltativo per `sessionStart`, `adStart`, `sessionStart` | [[!UICONTROL customMetadataDetails] - Raccolta](./custom-metadata-details-collection.md) | I metadati personalizzati contengono metadati definiti dall&#39;utente o aggiuntivi associati all&#39;evento esperienza. Questi metadati consentono di includere dati personalizzati o specifici nel contesto dell’evento. |
| [!UICONTROL ID sessione multimediale] | `sessionID` | Tutti gli eventi **eccetto** `sessionStart` e il contenuto scaricato. | stringa | L’ID sessione multimediale identifica in modo univoco un’istanza di un flusso di contenuto durante una singola sessione di riproduzione. Funge da identificatore distintivo per il tracciamento e la gestione dell’esperienza di riproduzione specifica associata a un utente o a un visualizzatore.<br><em>Nota:<em>`sessionId` viene inviato per tutti gli eventi, ad eccezione di `sessionStart` e per tutti gli eventi scaricati. |
| [!UICONTROL Testina di riproduzione] | `playhead` | Tutti gli eventi | intero | La testina di riproduzione rappresenta la posizione di riproduzione corrente all’interno del contenuto multimediale. Per il contenuto live, indica il secondo corrente del giorno (0 &lt;= indicatore di riproduzione &lt; 86400). Per il contenuto registrato, riflette il secondo corrente della durata del contenuto (0 &lt;= indicatore di riproduzione &lt; lunghezza contenuto). |

{style="table-layout:auto"}
