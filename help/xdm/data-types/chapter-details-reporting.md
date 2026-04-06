---
title: Dettagli capitolo Tipo di dati di reporting
description: Scopri il tipo di dati Chapter Details Reporting Experience Data Model (XDM).
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 6%

---

# [!UICONTROL Chapter Details] Tipo di dati di reporting

Il reporting di [!UICONTROL Chapter Details] è un tipo di dati XDM (Experience Data Model) standard che descrive vari attributi relativi a capitoli o segmenti all&#39;interno di contenuti multimediali. Utilizzare il tipo di dati di reporting [!UICONTROL Chapter Details] per acquisire dettagli quali il nome del capitolo, la durata, la posizione, l&#39;ID, lo stato di riproduzione (avviato/completato) e il tempo trascorso su ciascun capitolo. I servizi Adobe utilizzano i campi di reporting per contenuti multimediali per analizzare i campi di Media Collection inviati dagli utenti. Questi dati, insieme ad altre metriche utente specifiche, vengono calcolati e segnalati.

![Diagramma del tipo di dati di report Dettagli capitolo.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Ogni nome visualizzato contiene un collegamento per ulteriori informazioni sui parametri audio e video. Le pagine collegate contengono dettagli sui dati degli annunci video raccolti da Adobe, i valori di implementazione, i parametri di rete, il reporting e considerazioni importanti.

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Chapter Completed]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-complete) | `isCompleted` | booleano | Indica se il capitolo è stato completato o meno. |
| [[!UICONTROL Chapter ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter) | `ID` | stringa | ID del capitolo generato automaticamente. |
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-length) | `length` | intero | Durata del capitolo in secondi. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-name) | `friendlyName` | stringa | Nome del capitolo e/o del segmento. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-offset) | `offset` | intero | Offset del capitolo all’interno del contenuto, in secondi dall’inizio. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-position) | `index` | intero | Posizione (indice, numero intero) del capitolo all’interno del contenuto. |
| [[!UICONTROL Chapter Started]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-start) | `isStarted` | booleano | Indica se il capitolo è stato avviato o meno. |
| [[!UICONTROL Chapter Time Played]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-time-spent) | `timePlayed` | intero | Tempo trascorso sul capitolo, in secondi. |
