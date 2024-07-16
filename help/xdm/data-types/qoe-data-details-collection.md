---
title: Tipo di dati raccolta dettagli dati QoE (Quality of Experience)
description: Scopri il tipo di dati QoE (Quality of Experience) Data Collection Type Experience Data Model (XDM).
exl-id: d99816d9-e207-434a-9a40-ee9ded46c4d2
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# QoE (Quality of Experience) Dettagli Data Collection tipo di dati

La raccolta [!UICONTROL Dettagli dati QoE] è un tipo di dati XDM (Experience Data Model) standard e fornisce metriche dettagliate relative alla qualità dell&#39;esperienza (QoE) durante la riproduzione di contenuti multimediali. Utilizza il tipo di dati della raccolta [!UICONTROL Dettagli dati QoE] per acquisire dettagli quali informazioni sul bitrate, frame rate, eventi di buffering, fotogrammi saltati e così via. I campi di raccolta multimediale acquisiscono i dati e li inviano ad altri servizi Adobe per l’ulteriore elaborazione. Questo tipo di dati consente di analizzare la qualità di riproduzione e ottenere informazioni approfondite sulle prestazioni dello streaming, sull’esperienza utente e sui potenziali problemi riscontrati durante le sessioni di riproduzione.

+++Selezionare per visualizzare il tipo di dati Dettagli dati QoE.
![Diagramma del tipo di dati Raccolta dettagli dati QoE (Quality of Experience).](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Ogni nome visualizzato contiene un collegamento per ulteriori informazioni sui parametri audio e video. Le pagine collegate contengono dettagli sui dati degli annunci video raccolti da Adobe, i valori di implementazione, i parametri di rete, il reporting e considerazioni importanti.

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | intero | No | Il valore del bitrate (in kbps). |
| [[!UICONTROL Frame rilasciati]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames) | `droppedFrames` | intero | No | Numero totale di fotogrammi persi durante la riproduzione. |
| [[!UICONTROL Frame al secondo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | intero | No | Frame rate del flusso corrente (in fotogrammi al secondo). |
| [[!UICONTROL Ora Di Inizio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | intero | No | Durata (in secondi) tra il caricamento del video e l’avvio. |

{style="table-layout:auto"}
