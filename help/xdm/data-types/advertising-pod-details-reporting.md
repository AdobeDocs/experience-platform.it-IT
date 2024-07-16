---
title: Tipo di dati per generazione rapporti dettagli pod di Advertising
description: Scopri il tipo di dati Experience Data Model (XDM) per la generazione di rapporti Dettagli pod di Advertising.
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---

# [!UICONTROL Tipo di dati per generazione rapporti dettagli pod Advertising]

[!UICONTROL Segnalazione dettagli pod Advertising] è un tipo di dati Experience Data Model (XDM) standard. Definisce una sequenza o un gruppo di annunci in genere riprodotti in successione durante le interruzioni di contenuto. Utilizza il tipo di dati [!UICONTROL Generazione rapporti Dettagli pod di Advertising] per acquisire dettagli quali l&#39;ID dell&#39;interruzione pubblicitaria, un nome descrittivo per l&#39;interruzione pubblicitaria, l&#39;indice degli annunci all&#39;interno dell&#39;interruzione pubblicitaria e l&#39;offset dell&#39;interruzione pubblicitaria all&#39;interno della timeline del contenuto in secondi.

![Diagramma del tipo di dati di reporting Dettagli pod di Advertising.](../images/data-types/advertising-pod-details-information.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID interruzione annuncio] | `ID` | stringa | ID dell’interruzione pubblicitaria. |
| [!UICONTROL Nome descrittivo del pod] | `friendlyName` | stringa | Il nome facilmente comprensibile dell’interruzione pubblicitaria. |
| [!UICONTROL Annuncio In Posizione Pod] | `index` | intero | Indice dell’annuncio all’interno dell’inizio dell’interruzione pubblicitaria principale. |
| [!UICONTROL Offset pod] | `offset` | intero | **Obbligatorio** Offset dell&#39;interruzione pubblicitaria all&#39;interno del contenuto, in secondi. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
