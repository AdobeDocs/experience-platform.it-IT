---
title: Tipo di dati raccolta dettagli capitolo
description: Scopri il tipo di dati Chapter Details Collection Experience Data Model (XDM).
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 8%

---

# Tipo di dati della raccolta [!UICONTROL Chapter Details]

La raccolta [!UICONTROL Chapter Details] è un tipo di dati XDM (Experience Data Model) standard che descrive vari attributi relativi a capitoli o segmenti all&#39;interno di contenuti multimediali. Utilizzare il tipo di dati della raccolta [!UICONTROL Chapter Details] per acquisire dettagli quali il nome del capitolo, l&#39;offset, la durata e l&#39;indice del capitolo. I campi di raccolta multimediale acquisiscono i dati e li inviano ad altri servizi Adobe per l’ulteriore elaborazione.

![Diagramma del tipo di dati Raccolta dettagli capitolo.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Ogni nome visualizzato contiene un collegamento per ulteriori informazioni sui parametri audio e video. Le pagine collegate contengono dettagli sui dati degli annunci video raccolti da Adobe, i valori di implementazione, i parametri di rete, il reporting e considerazioni importanti.

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-length) | `length` | intero | Sì | Durata del capitolo in secondi. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-name) | `friendlyName` | stringa | No | Nome del capitolo e/o del segmento. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-offset) | `offset` | intero | Sì | Offset del capitolo all’interno del contenuto, in secondi dall’inizio. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=it#chapter-position) | `index` | intero | Sì | Posizione (indice, numero intero) del capitolo all’interno del contenuto. |

{style="table-layout:auto"}
