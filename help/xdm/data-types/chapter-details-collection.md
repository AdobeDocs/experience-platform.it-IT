---
title: Tipo di dati raccolta dettagli capitolo
description: Scopri il tipo di dati Chapter Details Collection Experience Data Model (XDM).
source-git-commit: c6108bb692c80c79e115ac7b1488d95a7039ffcf
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 6%

---

# [!UICONTROL Dettagli capitolo] Tipo di dati della raccolta

[!UICONTROL Dettagli capitolo] La raccolta è un tipo di dati Experience Data Model (XDM) standard che descrive vari attributi relativi a capitoli o segmenti all’interno di contenuti multimediali. Utilizza il [!UICONTROL Dettagli capitolo] Tipo di dati di raccolta per acquisire dettagli quali il nome del capitolo, l&#39;offset, la durata e l&#39;indice del capitolo. I campi di raccolta multimediale acquisiscono i dati e li inviano ad altri servizi Adobe per l’ulteriore elaborazione.

![Diagramma del tipo di dati Raccolta dettagli capitolo.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Ogni nome visualizzato contiene un collegamento per ulteriori informazioni sui parametri audio e video. Le pagine collegate contengono dettagli sui dati degli annunci video raccolti da Adobe, i valori di implementazione, i parametri di rete, il reporting e considerazioni importanti.

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Durata O Lunghezza Del Capitolo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | numero intero | Sì | Durata del capitolo in secondi. |
| [[!UICONTROL Nome del capitolo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | string | No | Nome del capitolo e/o del segmento. |
| [[!UICONTROL Offset capitolo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | numero intero | Sì | Offset del capitolo all’interno del contenuto, in secondi dall’inizio. |
| [[!UICONTROL Posizione capitolo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | numero intero | Sì | Posizione (indice, numero intero) del capitolo all’interno del contenuto. |

{style="table-layout:auto"}
