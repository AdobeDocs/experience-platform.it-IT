---
title: Tipo di dati informazioni dettagli Advertising Pod
description: Scopri il tipo di dati Experience Data Model (XDM) per i dettagli dei pod di Advertising.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 4%

---

# [!UICONTROL Informazioni sui dettagli di Advertising Pod] tipo di dati

[!UICONTROL Informazioni sui dettagli di Advertising Pod] è un tipo di dati Experience Data Model (XDM) standard. Definisce una sequenza o un gruppo di annunci in genere riprodotti in successione durante le interruzioni di contenuto. Utilizza il [!UICONTROL Informazioni sui dettagli di Advertising Pod] tipo di dati per acquisire dettagli quali l’ID dell’interruzione pubblicitaria, un nome descrittivo per l’interruzione pubblicitaria, l’indice degli annunci all’interno dell’interruzione pubblicitaria e l’offset dell’interruzione pubblicitaria all’interno della timeline del contenuto in secondi.

![Diagramma del tipo di dati Dettagli contenitore pubblicitario.](../images/data-types/advertising-pod-details-information.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID interruzione annuncio] | `ID` | string | ID dell’interruzione pubblicitaria. |
| [!UICONTROL Nome descrittivo del pod] | `friendlyName` | string | Il nome facilmente comprensibile dell’interruzione pubblicitaria. |
| [!UICONTROL Posizione annuncio nel pod] | `index` | numero intero | Indice dell’annuncio all’interno dell’inizio dell’interruzione pubblicitaria principale. |
| [!UICONTROL Offset pod] | `offset` | numero intero | **Obbligatorio** Lo scostamento dell’interruzione pubblicitaria all’interno del contenuto, in secondi. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
