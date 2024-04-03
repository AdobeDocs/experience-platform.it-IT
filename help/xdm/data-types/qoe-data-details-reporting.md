---
title: Dettagli dei dati QoE (Quality of Experience) Tipo di dati di reporting
description: Scopri il tipo di dati QoE (Quality of Experience) Data Details Reporting Data Type Experience Data Model (XDM).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# Dettagli dei dati QoE (Quality of Experience) Tipo di dati di reporting

[!UICONTROL Dettagli dati QoE] Il reporting è un tipo di dati Experience Data Model (XDM) standard che fornisce metriche dettagliate relative alla qualità dell’esperienza (QoE) durante la riproduzione di contenuti multimediali. Utilizza il [!UICONTROL Dettagli dati QoE] Tipo di dati per acquisire dettagli quali informazioni sul bitrate, frame rate, eventi di buffering, fotogrammi saltati e così via. I servizi Adobe utilizzano i campi di reporting per contenuti multimediali per analizzare i campi di Media Collection inviati dagli utenti. Questi dati, insieme ad altre metriche utente specifiche, vengono calcolati e segnalati. Questo tipo di dati consente di analizzare la qualità di riproduzione e ottenere informazioni approfondite sulle prestazioni dello streaming, sull’esperienza utente e sui potenziali problemi riscontrati durante le sessioni di riproduzione.

+++Selezionare questa opzione per visualizzare il tipo di dati di reporting Dettagli dati QoE.
![Un diagramma del tipo di dati QoE (Quality of Experience) Data Details Reporting (Dettagli qualità dell’esperienza).](../images/data-types/qoe-data-details-reporting.png)
+++

>[!NOTE]
>
>Ogni nome visualizzato contiene un collegamento per ulteriori informazioni sui parametri audio e video. Le pagine collegate contengono dettagli sui dati degli annunci video raccolti da Adobe, i valori di implementazione, i parametri di rete, il reporting e considerazioni importanti.

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|---------------------------------------------------------------------------------------------------|
| [[!UICONTROL Bitrate medio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate-1) | `bitrateAverage` | number | Il bitrate medio (in kbps, numero intero). Calcolato come media ponderata dei valori del bitrate. |
| [[!UICONTROL Bucket bitrate medio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrateAverageBucket` | string | Il bitrate medio (in kbps) categorizzato in bucket predefiniti a intervalli di 100 kbps. |
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | numero intero | Il valore del bitrate (in kbps). |
| [[!UICONTROL Flussi interessati dalla modifica del bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-change-impacted-streams) | `hasBitrateChangeImpactedStreams` | booleano | Indica se i flussi sono stati interessati dalle modifiche del bitrate durante la riproduzione. |
| [[!UICONTROL Modifiche bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-changes) | `bitrateChangeCount` | numero intero | Numero totale di modifiche del bitrate durante la riproduzione. |
| [[!UICONTROL Eventi buffer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-events) | `bufferCount` | numero intero | Numero di stati del buffer diversi durante la riproduzione. |
| [[!UICONTROL Flussi interessati dal buffer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-impacted-streams) | `hasBufferImpactedStreams` | booleano | Indica se i flussi sono stati interessati dal buffering durante la riproduzione. |
| [[!UICONTROL Flussi interessati da fotogrammi saltati]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frame-impacted-streams) | `hasDroppedFrameImpactedStreams` | booleano | Indica se i flussi sono stati interessati dalla perdita di fotogrammi durante la riproduzione. |
| [[!UICONTROL Frame rilasciati]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames-1) | `droppedFrames` | numero intero | Numero totale di fotogrammi persi durante la riproduzione. |
| [[!UICONTROL Perdite prima degli inizi]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#drops-before-start) | `isDroppedBeforeStart` | booleano | Indica se gli utenti abbandonano il video prima del suo avvio, indipendentemente dagli annunci. |
| [[!UICONTROL Flussi interessati dall’errore]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#error-impacted-streams) | `hasErrorImpactedStreams` | booleano | Indica se i flussi hanno riscontrato errori durante la riproduzione. |
| [[!UICONTROL Errori]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#errors-%2F-error-events) | `errorCount` | numero intero | Numero totale di errori che si sono verificati durante la riproduzione. |
| [[!UICONTROL ID errore esterni]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#external-error-ids) | `externalErrors` | array di stringhe | ID di errore univoci da origini esterne, ad esempio errori CDN. |
| [[!UICONTROL Fotogrammi al secondo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | numero intero | Frame rate del flusso corrente (in fotogrammi al secondo). |
| [[!UICONTROL ID degli errori di Media SDK]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#media-sdk-error-ids) | `mediaSdkErrors` | array di stringhe | ID di errore univoci generati da Media SDK durante la riproduzione. |
| [[!UICONTROL ID degli errori dell’SDK del lettore]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#player-sdk-error-ids) | `playerSdkErrors` | array di stringhe | ID di errore univoci generati dall’SDK del lettore durante la riproduzione. |
| [[!UICONTROL Eventi di interruzione]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-events) | `stallCount` | numero intero | Numero di eventi di arresto durante la riproduzione. |
| [[!UICONTROL Flussi interessati da interruzioni]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-impacted-streams) | `hasStallImpactedStreams` | booleano | Indica se durante la riproduzione si è verificato uno stallo dei flussi. |
| [[!UICONTROL Ora di inizio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | numero intero | Durata (in secondi) tra il caricamento del video e l’avvio. |
| [[!UICONTROL Durata totale buffer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-buffer-duration-1) | `bufferTime` | numero intero | Tempo totale (in secondi) dedicato al buffering durante la riproduzione. |
| [[!UICONTROL Durata totale dello stallo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-stalling-duration) | `stallTime` | numero intero | Tempo totale (in secondi) in cui la riproduzione è stata arrestata durante la riproduzione. |

{style="table-layout:auto"}
