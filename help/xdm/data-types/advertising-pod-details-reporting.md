---
title: Tipo di dati per generazione rapporti dettagli pod pubblicitari
description: Scopri il tipo di dati Reporting Experience Data Model (XDM) di Advertising Pod Details.
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 4%

---

# [!UICONTROL Reporting sui dettagli dei pod pubblicitari] tipo di dati

[!UICONTROL Reporting sui dettagli dei pod pubblicitari] è un tipo di dati Experience Data Model (XDM) standard. Definisce una sequenza o un gruppo di annunci in genere riprodotti in successione durante le interruzioni di contenuto. Utilizza il [!UICONTROL Reporting sui dettagli dei pod pubblicitari] tipo di dati per acquisire dettagli quali l’ID dell’interruzione pubblicitaria, un nome descrittivo per l’interruzione pubblicitaria, l’indice degli annunci all’interno dell’interruzione pubblicitaria e l’offset dell’interruzione pubblicitaria all’interno della timeline del contenuto in secondi.

![Diagramma del tipo di dati Reporting dei dettagli del pod pubblicitario.](../images/data-types/advertising-pod-details-information.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID interruzione annuncio] | `ID` | string | ID dell’interruzione pubblicitaria. |
| [!UICONTROL Nome descrittivo del pod] | `friendlyName` | string | Il nome facilmente comprensibile dell’interruzione pubblicitaria. |
| [!UICONTROL Posizione annuncio nel pod] | `index` | numero intero | Indice dell’annuncio all’interno dell’inizio dell’interruzione pubblicitaria principale. |
| [!UICONTROL Offset pod] | `offset` | numero intero | **Obbligatorio** Lo scostamento dell’interruzione pubblicitaria all’interno del contenuto, in secondi. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
