---
title: Tipo di dati Dettagli di Media Reporting
description: Scopri il tipo di dati Dettagli di Media Reporting Experience Data Model (XDM).
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# [!UICONTROL Media Reporting Details] tipo di dati

>[!NOTE]
>
>I campi di Media Collection acquisiscono i dati e li inviano ad altri servizi Adobe per un’ulteriore elaborazione. I servizi Adobe utilizzano i campi di Media Reporting per analizzare i campi di Media Collection inviati dagli utenti. Questi dati, insieme ad altre metriche utente specifiche, vengono calcolati e segnalati.

[!UICONTROL Media Reporting Details] è un tipo di dati Experience Data Model (XDM) standard che acquisisce dettagli essenziali sugli eventi di riproduzione multimediale. Utilizza il tipo di dati [!UICONTROL Dettagli di Media Reporting] per acquisire dettagli quali, tra gli altri, la posizione della testina di riproduzione all&#39;interno del contenuto, identificatori di sessione univoci e varie proprietà nidificate relative alla sessione. Questo tipo di dati fornisce una panoramica completa dell’esperienza di riproduzione che consente il tracciamento e l’analisi dei modelli di consumo dei contenuti multimediali e degli eventi associati durante le sessioni di riproduzione.

>[!NOTE]
>
>I campi indicati di seguito non vengono utilizzati direttamente per creare richieste. Al contrario, la raccolta di campi inviata a Adobe Experience Platform o Adobe Analytics viene assemblata dai dati della richiesta e le metriche vengono quindi incorporate o elaborate dall’infrastruttura del server. Anche se Platform raccoglie vari tipi di eventi utente, i rapporti restituiti all&#39;utente sono incentrati su eventi specifici, ad esempio `media.sessionStart`, `media.adStart` e `media.sessionComplete`. Ciò significa che, anche se trasmetti 12 tipi di eventi durante la raccolta, i rapporti presenteranno solo raggruppamenti basati sui cinque eventi elencati di seguito.

+++Selezionare per visualizzare un diagramma del tipo di dati [!UICONTROL Dettagli report multimediali].
![Diagramma del tipo di dati [!UICONTROL Dettagli report multimediali].](../images/data-types/media-reporting-details.png)
+++

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Dettagli Advertising] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | I dettagli di Advertising si riferiscono a informazioni specifiche relative alle attività pubblicitarie durante l’evento esperienza. Ciò include metadati di annunci, specifiche di targeting e metriche delle prestazioni. |
| [!UICONTROL Dettagli pod Advertising] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | I Dettagli del pod di Advertising contengono informazioni sui pod di annunci all’interno dell’evento esperienza. Fornisce informazioni approfondite sulla sequenza degli annunci, sui contenuti e sulle metriche di coinvolgimento. |
| [!UICONTROL Dettagli capitolo] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Dettagli capitolo acquisisce i dati relativi ai capitoli o alle parti segmentate del contenuto. Fornisce informazioni sui marcatori capitolo, le timeline e i metadati associati. |
| [!UICONTROL Elenco Stati] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | La proprietà States è un array che acquisisce vari stati durante l’evento esperienza. Questa proprietà fornisce dati sequenziali sulla riproduzione, sulle azioni dell’utente o sulle modifiche al contenuto. |
| [!UICONTROL Dettagli dati Qoe] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | I dettagli dei dati QoE (Quality of Experience) acquisiscono metriche relative alle prestazioni e dati sull&#39;esperienza utente. Fornisce informazioni approfondite sulla qualità, la reattività e le interazioni degli utenti. |
| [!UICONTROL Dettagli sessione] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | I dettagli della sessione includono informazioni complete associate all’evento esperienza, che offrono informazioni approfondite sulle interazioni degli utenti, sulla durata e sui dati contestuali relativi alla sessione di riproduzione. |
| [!UICONTROL Metadati Personalizzati] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | I metadati personalizzati contengono metadati definiti dall&#39;utente o aggiuntivi associati all&#39;evento esperienza. Questi metadati consentono di includere dati personalizzati o specifici nel contesto dell’evento. |
| [!UICONTROL Testina di riproduzione] | `playhead` | intero | La testina di riproduzione rappresenta la posizione di riproduzione corrente all’interno del contenuto multimediale. Per il contenuto live, indica il secondo corrente del giorno (0 &lt;= indicatore di riproduzione &lt; 86400). Per il contenuto registrato, riflette il secondo corrente della durata del contenuto (0 &lt;= indicatore di riproduzione &lt; lunghezza contenuto). |

{style="table-layout:auto"}
