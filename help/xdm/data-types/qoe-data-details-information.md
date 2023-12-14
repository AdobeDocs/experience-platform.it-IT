---
title: QoE (Quality of Experience) Dettagli Dati Informazioni Tipo di dati
description: Scopri il tipo di dati QoE (Quality of Experience) Data Details Information Data Type Experience Data Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# QoE (Quality of Experience) Dettagli Dati Tipo di dati Informazioni

[!UICONTROL Informazioni dettagli dati QoE] è un tipo di dati Experience Data Model (XDM) standard che fornisce metriche dettagliate relative alla qualità dell’esperienza (QoE) durante la riproduzione di contenuti multimediali. Utilizza il [!UICONTROL Informazioni dettagli dati QoE] tipo di dati per acquisire dettagli quali informazioni sul bitrate, frame rate, eventi di buffering, fotogrammi saltati e così via. Questo tipo di dati consente di analizzare la qualità di riproduzione e ottenere informazioni approfondite sulle prestazioni dello streaming, sull’esperienza utente e sui potenziali problemi riscontrati durante le sessioni di riproduzione.

+++Selezionare questa opzione per visualizzare il tipo di dati Dettagli dati QoE.
![Un diagramma del tipo di dati Dettagli dati QoE (Quality of Experience).](../images/data-types/qoe-data-details-information.png)
+++

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------------------|----------------------------|-----------|--------------------------------------------------------------------------------------------------|
| [!UICONTROL Bucket bitrate medio] | `bitrateAverageBucket` | string | Il bitrate medio (in kbps) categorizzato in bucket predefiniti a intervalli di 100 kbps. |
| [!UICONTROL Bitrate] | `bitrate` | numero intero | Il valore del bitrate (in kbps). |
| [!UICONTROL Bitrate medio] | `bitrateAverage` | number | Il bitrate medio (in kbps, numero intero). Calcolato come media ponderata dei valori del bitrate. |
| [!UICONTROL Flussi interessati dalla modifica del bitrate] | `hasBitrateChangeImpactedStreams` | booleano | Indica se i flussi sono stati interessati dalle modifiche del bitrate durante la riproduzione. |
| [!UICONTROL Modifiche bitrate] | `bitrateChangeCount` | numero intero | Numero totale di modifiche del bitrate durante la riproduzione. |
| [!UICONTROL Flussi interessati da fotogrammi saltati] | `hasDroppedFrameImpactedStreams` | booleano | Indica se i flussi sono stati interessati dalla perdita di fotogrammi durante la riproduzione. |
| [!UICONTROL Frame rilasciati] | `droppedFrames` | numero intero | Numero totale di fotogrammi persi durante la riproduzione. |
| [!UICONTROL Perdite prima degli inizi] | `isDroppedBeforeStart` | booleano | Indica se gli utenti abbandonano il video prima del suo avvio, indipendentemente dagli annunci. |
| [!UICONTROL Fotogrammi al secondo] | `framesPerSecond` | numero intero | Frame rate del flusso corrente (in fotogrammi al secondo). |
| [!UICONTROL Ora di inizio] | `timeToStart` | numero intero | Durata (in secondi) tra il caricamento del video e l’avvio. |
| [!UICONTROL Flussi interessati dal buffer] | `hasBufferImpactedStreams` | booleano | Indica se i flussi sono stati interessati dal buffering durante la riproduzione. |
| [!UICONTROL Eventi buffer] | `bufferCount` | numero intero | Numero di stati del buffer diversi durante la riproduzione. |
| [!UICONTROL Durata totale buffer] | `bufferTime` | numero intero | Tempo totale (in secondi) dedicato al buffering durante la riproduzione. |
| [!UICONTROL Flussi interessati dall’errore] | `hasErrorImpactedStreams` | booleano | Indica se i flussi hanno riscontrato errori durante la riproduzione. |
| [!UICONTROL Errori] | `errorCount` | numero intero | Numero totale di errori che si sono verificati durante la riproduzione. |
| [!UICONTROL Flussi interessati da interruzioni] | `hasStallImpactedStreams` | booleano | Indica se durante la riproduzione si è verificato uno stallo dei flussi. |
| [!UICONTROL Eventi di interruzione] | `stallCount` | numero intero | Numero di eventi di arresto durante la riproduzione. |
| [!UICONTROL Durata totale dello stallo] | `stallTime` | numero intero | Tempo totale (in secondi) in cui la riproduzione è stata arrestata durante la riproduzione. |
| [!UICONTROL ID degli errori dell’SDK del lettore] | `playerSdkErrors` | array di stringhe | ID di errore univoci generati dall’SDK del lettore durante la riproduzione. |
| [!UICONTROL ID errore esterni] | `externalErrors` | array di stringhe | ID di errore univoci da origini esterne, ad esempio errori CDN. |
| [!UICONTROL ID degli errori di Media SDK] | `mediaSdkErrors` | array di stringhe | ID di errore univoci generati da Media SDK durante la riproduzione. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json).

