---
title: Tipo di dati raccolta dettagli pod pubblicitari
description: Scopri il tipo di dati Experience Data Model (XDM) della raccolta dei dettagli dei pod di Advertising.
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 6%

---

# [!UICONTROL Dettagli Advertising Pod] Tipo di dati della raccolta

[!UICONTROL Dettagli Advertising Pod] La raccolta è un tipo di dati Experience Data Model (XDM) standard. Definisce una sequenza o un gruppo di annunci in genere riprodotti in successione durante le interruzioni di contenuto. Utilizza il [!UICONTROL Dettagli Advertising Pod] Tipo di dati di raccolta per acquisire dettagli quali l’ID dell’interruzione pubblicitaria, un nome descrittivo per l’interruzione pubblicitaria, l’indice degli annunci all’interno dell’interruzione pubblicitaria e l’offset dell’interruzione pubblicitaria all’interno della timeline del contenuto in secondi.

![Diagramma del tipo di dati Raccolta informazioni dettagli contenitore pubblicitario.](../images/data-types/advertising-pod-details-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| [!UICONTROL Posizione annuncio nel pod] | `index` | numero intero | Sì | Indice dell’annuncio all’interno dell’inizio dell’interruzione pubblicitaria principale. |
| [!UICONTROL Nome descrittivo del pod] | `friendlyName` | string | No | Il nome facilmente comprensibile dell’interruzione pubblicitaria. |
| [!UICONTROL Offset pod] | `offset` | numero intero | Sì | Lo scostamento dell’interruzione pubblicitaria all’interno del contenuto, in secondi. |
