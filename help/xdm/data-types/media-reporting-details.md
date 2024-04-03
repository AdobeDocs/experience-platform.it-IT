---
title: Tipo di dati Dettagli di Media Reporting
description: Scopri il tipo di dati Dettagli di Media Reporting Experience Data Model (XDM).
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# [!UICONTROL Dettagli di Media Reporting] tipo di dati

>[!NOTE]
>
>I campi di Media Collection acquisiscono i dati e li inviano ad altri servizi Adobe per un’ulteriore elaborazione. I servizi Adobe utilizzano i campi di Media Reporting per analizzare i campi di Media Collection inviati dagli utenti. Questi dati, insieme ad altre metriche utente specifiche, vengono calcolati e segnalati.

[!UICONTROL Dettagli di Media Reporting] è un tipo di dati Experience Data Model (XDM) standard che acquisisce dettagli essenziali sugli eventi di riproduzione di contenuti multimediali. Utilizza il [!UICONTROL Dettagli di Media Reporting] tipo di dati per acquisire dettagli quali la posizione della testina di riproduzione all’interno del contenuto, identificatori di sessione univoci e varie proprietà nidificate relative, tra gli altri, alla sessione. Questo tipo di dati fornisce una panoramica completa dell’esperienza di riproduzione che consente il tracciamento e l’analisi dei modelli di consumo dei contenuti multimediali e degli eventi associati durante le sessioni di riproduzione.

>[!NOTE]
>
>I campi indicati di seguito non vengono utilizzati direttamente per creare richieste. Al contrario, la raccolta di campi inviata a Adobe Experience Platform o Adobe Analytics viene assemblata dai dati della richiesta e le metriche vengono quindi incorporate o elaborate dall’infrastruttura del server. Mentre Platform raccoglie vari tipi di eventi utente, i rapporti restituiti all’utente sono incentrati su eventi specifici, ad esempio `media.sessionStart`, `media.adStart`, e `media.sessionComplete`. Ciò significa che, anche se trasmetti 12 tipi di eventi durante la raccolta, i rapporti presenteranno solo raggruppamenti basati sui cinque eventi elencati di seguito.

+++Selezionare questa opzione per visualizzare un diagramma del [!UICONTROL Dettagli di Media Reporting] tipo di dati.
![Un diagramma del [!UICONTROL Dettagli di Media Reporting] tipo di dati.](../images/data-types/media-reporting-details.png)
+++

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Dettagli pubblicitari] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Dettagli pubblicitari si riferiscono a informazioni specifiche relative alle attività pubblicitarie durante l’evento esperienza. Ciò include metadati di annunci, specifiche di targeting e metriche delle prestazioni. |
| [!UICONTROL Dettagli Advertising Pod] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | I dettagli di Advertising Pod contengono informazioni sui pod di annunci all’interno dell’evento esperienza. Fornisce informazioni approfondite sulla sequenza degli annunci, sui contenuti e sulle metriche di coinvolgimento. |
| [!UICONTROL Dettagli capitolo] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Dettagli capitolo acquisisce i dati relativi ai capitoli o alle parti segmentate del contenuto. Fornisce informazioni sui marcatori capitolo, le timeline e i metadati associati. |
| [!UICONTROL Elenco Degli Stati] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | La proprietà States è un array che acquisisce vari stati durante l’evento esperienza. Questa proprietà fornisce dati sequenziali sulla riproduzione, sulle azioni dell’utente o sulle modifiche al contenuto. |
| [!UICONTROL Dettagli dati Qoe] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | I dettagli dei dati QoE (Quality of Experience) acquisiscono metriche relative alle prestazioni e dati sull&#39;esperienza utente. Fornisce informazioni approfondite sulla qualità, la reattività e le interazioni degli utenti. |
| [!UICONTROL Dettagli sessione] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | I dettagli della sessione includono informazioni complete associate all’evento esperienza, che offrono informazioni approfondite sulle interazioni degli utenti, sulla durata e sui dati contestuali relativi alla sessione di riproduzione. |
| [!UICONTROL I metadati personalizzati] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | I metadati personalizzati contengono metadati definiti dall&#39;utente o aggiuntivi associati all&#39;evento esperienza. Questi metadati consentono di includere dati personalizzati o specifici nel contesto dell’evento. |
| [!UICONTROL Playhead] | `playhead` | numero intero | La testina di riproduzione rappresenta la posizione di riproduzione corrente all’interno del contenuto multimediale. Per il contenuto live, indica il secondo corrente del giorno (0 &lt;= indicatore di riproduzione &lt; 86400). Per il contenuto registrato, riflette il secondo corrente della durata del contenuto (0 &lt;= indicatore di riproduzione &lt; lunghezza contenuto). |

{style="table-layout:auto"}
