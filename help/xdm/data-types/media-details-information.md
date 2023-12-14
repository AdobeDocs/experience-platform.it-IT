---
title: Tipo di dati informazioni dettagli contenuti multimediali
description: Scopri il tipo di dati Informazioni su Media Details Experience Data Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# [!UICONTROL Informazioni sui dettagli dei contenuti multimediali] tipo di dati

[!UICONTROL Informazioni sui dettagli dei contenuti multimediali] è un tipo di dati Experience Data Model (XDM) standard che acquisisce dettagli essenziali sugli eventi di riproduzione di contenuti multimediali. Utilizza il [!UICONTROL Informazioni sui dettagli dei contenuti multimediali] tipo di dati per acquisire dettagli quali la posizione della testina di riproduzione all’interno del contenuto, identificatori di sessione univoci e varie proprietà nidificate relative, tra gli altri, alla sessione. Questo tipo di dati fornisce una panoramica completa dell’esperienza di riproduzione, che consente il tracciamento e l’analisi dei modelli di consumo dei contenuti multimediali e degli eventi associati durante le sessioni di riproduzione.

+++Selezionare questa opzione per visualizzare un diagramma del [!UICONTROL Informazioni sui dettagli dei contenuti multimediali] tipo di dati.
![Un diagramma del [!UICONTROL Informazioni sui dettagli dei contenuti multimediali] tipo di dati.](../images/data-types/media-details-information.png)
+++

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Playhead] | `playhead` | numero intero | La testina di riproduzione rappresenta la posizione di riproduzione corrente all’interno del contenuto multimediale. Per il contenuto live, indica il secondo corrente del giorno (0 &lt;= indicatore di riproduzione &lt; 86400). Per il contenuto registrato, riflette il secondo corrente della durata del contenuto (0 &lt;= indicatore di riproduzione &lt; lunghezza contenuto). |
| [!UICONTROL ID sessione multimediale] | `sessionID` | string | L’ID sessione multimediale identifica in modo univoco un’istanza di un flusso di contenuto durante una singola sessione di riproduzione. Funge da identificatore distintivo per il tracciamento e la gestione dell’esperienza di riproduzione specifica associata a un utente o a un visualizzatore. |
| [!UICONTROL Dettagli sessione] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-information.md) | I dettagli della sessione includono informazioni complete associate all’evento esperienza, che offrono informazioni approfondite sulle interazioni degli utenti, sulla durata e sui dati contestuali relativi alla sessione di riproduzione. |
| [!UICONTROL Dettagli pubblicitari] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-information.md) | Dettagli pubblicitari si riferiscono a informazioni specifiche relative alle attività pubblicitarie durante l’evento esperienza. Ciò include metadati di annunci, specifiche di targeting e metriche delle prestazioni. |
| [!UICONTROL Dettagli Advertising Pod] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-information.md) | I dettagli di Advertising Pod contengono informazioni sui pod di annunci all’interno dell’evento esperienza. Fornisce informazioni approfondite sulla sequenza degli annunci, sui contenuti e sulle metriche di coinvolgimento. |
| [!UICONTROL Dettagli capitolo] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-information.md) | Dettagli capitolo acquisisce i dati relativi ai capitoli o alle parti segmentate del contenuto. Fornisce informazioni sui marcatori capitolo, le timeline e i metadati associati. |
| [!UICONTROL Dettagli errore] | `errorDetails` | [[!UICONTROL errorDetails]](./error-details-information.md) | I Dettagli errore contengono informazioni relative agli errori riscontrati durante l’evento esperienza. Ciò include codici di errore, descrizioni, marche temporali e dati contestuali pertinenti. |
| [!UICONTROL Dettagli dati Qoe] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-information.md) | I dettagli dei dati QoE (Quality of Experience) acquisiscono metriche relative alle prestazioni e dati sull&#39;esperienza utente. Fornisce informazioni approfondite sulla qualità, la reattività e le interazioni degli utenti. |
| [!UICONTROL Elenco Degli Stati Inizio] | `statesStart` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | State Start fornisce un array per elencare gli stati all’inizio dell’evento esperienza. Sono disponibili dati relativi alla riproduzione, alle azioni dell’utente o alle specifiche del contenuto. |
| [!UICONTROL Fine Elenco Di Stati] | `statesEnd` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | State End fornisce un array per elencare gli stati alla conclusione dell’evento esperienza. Contiene dettagli sugli stati di riproduzione finali o sullo stato del contenuto. |
| [!UICONTROL Elenco Degli Stati] | `states` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | La proprietà States è un array che acquisisce vari stati durante l’evento esperienza. Questa proprietà fornisce dati sequenziali sulla riproduzione, sulle azioni dell’utente o sulle modifiche al contenuto. |
| [!UICONTROL I metadati personalizzati] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-information.md) | I metadati personalizzati contengono metadati definiti dall&#39;utente o aggiuntivi associati all&#39;evento esperienza. Questi metadati consentono di includere dati personalizzati o specifici nel contesto dell’evento. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json)
