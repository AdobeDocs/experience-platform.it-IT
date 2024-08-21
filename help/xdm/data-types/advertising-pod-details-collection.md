---
title: Tipo di dati raccolta dettagli pod Advertising
description: Scopri il tipo di dati Experience Data Model (XDM) della raccolta dei dettagli del pod di Advertising.
exl-id: 401c393f-aeda-4ecd-89f4-458833190ced
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---

# [!UICONTROL Dettagli pod Advertising] Tipo di dati raccolta

[!UICONTROL Dettagli Advertising Pod] La raccolta è un tipo di dati XDM (Experience Data Model) standard. Definisce una sequenza o un gruppo di annunci in genere riprodotti in successione durante le interruzioni di contenuto. Utilizza il tipo di dati della raccolta [!UICONTROL Dettagli del pod di Advertising] per acquisire dettagli quali l&#39;ID dell&#39;interruzione pubblicitaria, un nome descrittivo per l&#39;interruzione pubblicitaria, l&#39;indice degli annunci all&#39;interno dell&#39;interruzione e l&#39;offset dell&#39;interruzione pubblicitaria all&#39;interno della timeline del contenuto in secondi.

![Diagramma del tipo di dati Raccolta informazioni dettagli pod di Advertising.](../images/data-types/advertising-pod-details-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|-----------------------------------------|-----------------|-----------|----------|---------------------------------------------------------|
| [!UICONTROL Annuncio In Posizione Pod] | `index` | intero | Sì | Indice dell’annuncio all’interno dell’inizio dell’interruzione pubblicitaria principale. |
| [!UICONTROL Nome descrittivo del pod] | `friendlyName` | stringa | No | Il nome facilmente comprensibile dell’interruzione pubblicitaria. |
| [!UICONTROL Offset pod] | `offset` | intero | Sì | Lo scostamento dell’interruzione pubblicitaria all’interno del contenuto, in secondi. |

{style="table-layout:auto"}
