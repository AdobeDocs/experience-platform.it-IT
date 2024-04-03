---
title: Dettagli capitolo Tipo di dati di reporting
description: Scopri il tipo di dati Chapter Details Reporting Experience Data Model (XDM).
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 4%

---

# [!UICONTROL Dettagli capitolo] Tipo di dati di reporting

[!UICONTROL Dettagli capitolo] Il reporting è un tipo di dati Experience Data Model (XDM) standard che descrive vari attributi relativi a capitoli o segmenti all’interno di contenuti multimediali. Utilizza il [!UICONTROL Dettagli capitolo] Tipo di dati per acquisire dettagli quali nome del capitolo, durata, posizione, ID, stato di riproduzione (avviato/completato) e tempo trascorso su ciascun capitolo. I servizi Adobe utilizzano i campi di reporting per contenuti multimediali per analizzare i campi di Media Collection inviati dagli utenti. Questi dati, insieme ad altre metriche utente specifiche, vengono calcolati e segnalati.

![Diagramma del tipo di dati di reporting Dettagli capitolo.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Ogni nome visualizzato contiene un collegamento per ulteriori informazioni sui parametri audio e video. Le pagine collegate contengono dettagli sui dati degli annunci video raccolti da Adobe, i valori di implementazione, i parametri di rete, il reporting e considerazioni importanti.

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Capitolo completato]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-complete) | `isCompleted` | booleano | Indica se il capitolo è stato completato o meno. |
| [[!UICONTROL ID capitolo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter) | `ID` | string | ID del capitolo generato automaticamente. |
| [[!UICONTROL Durata O Lunghezza Del Capitolo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | numero intero | Durata del capitolo in secondi. |
| [[!UICONTROL Nome del capitolo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | string | Nome del capitolo e/o del segmento. |
| [[!UICONTROL Offset capitolo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | numero intero | Offset del capitolo all’interno del contenuto, in secondi dall’inizio. |
| [[!UICONTROL Posizione capitolo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | numero intero | Posizione (indice, numero intero) del capitolo all’interno del contenuto. |
| [[!UICONTROL Capitolo avviato]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-start) | `isStarted` | booleano | Indica se il capitolo è stato avviato o meno. |
| [[!UICONTROL Tempo capitolo riprodotto]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-time-spent) | `timePlayed` | numero intero | Tempo trascorso sul capitolo, in secondi. |
