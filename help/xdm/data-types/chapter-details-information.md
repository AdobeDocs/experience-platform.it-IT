---
title: Tipo di dati informazioni dettagli capitolo
description: Scopri il tipo di dati XDM (Experience Data Model) per i dettagli del capitolo.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 6%

---

# [!UICONTROL Informazioni sui dettagli dei capitoli] tipo di dati

[!UICONTROL Informazioni sui dettagli dei capitoli] è un tipo di dati Experience Data Model (XDM) standard che descrive vari attributi relativi a capitoli o segmenti all’interno di contenuti multimediali. Utilizza il [!UICONTROL Informazioni sui dettagli dei capitoli] tipo di dati per acquisire dettagli quali il nome del capitolo, la durata, la posizione, l’ID, lo stato di riproduzione (avviato/completato) e il tempo trascorso su ciascun capitolo.

![Diagramma del tipo di dati Informazioni dettagli capitolo.](../images/data-types/chapter-details-information.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|---------------------------|---------------|-----------|---------------------------------------------------|
| [!UICONTROL Nome del capitolo] | `friendlyName` | string | Nome del capitolo e/o del segmento. |
| [!UICONTROL Durata O Lunghezza Del Capitolo] | `length` | numero intero | **Obbligatorio** Durata del capitolo in secondi. |
| [!UICONTROL Offset capitolo] | `offset` | numero intero | **Obbligatorio** Offset del capitolo all’interno del contenuto, in secondi dall’inizio. |
| [!UICONTROL Posizione capitolo] | `index` | numero intero | **Obbligatorio** Posizione (indice, numero intero) del capitolo all’interno del contenuto. |
| [!UICONTROL ID capitolo] | `ID` | string | ID del capitolo generato automaticamente. |
| [!UICONTROL Capitolo avviato] | `isStarted` | booleano | Indica se il capitolo è stato avviato. |
| [!UICONTROL Capitolo completato] | `isCompleted` | booleano | Se il capitolo è stato completato. |
| [!UICONTROL Tempo capitolo riprodotto] | `timePlayed` | numero intero | Tempo trascorso sul capitolo, in secondi. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json)
