---
title: Dettagli sul controllo del sistema di sorgente esterna
description: Scopri il gruppo di campi Dettagli audit sistema Source esterno Experience Data Model (XDM).
source-git-commit: 656070cf69e3713c7889f53d51937e0e70085d96
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 6%

---

# [!UICONTROL Dettagli controllo del sistema Source esterno] gruppo di campi

[!UICONTROL Dettagli controllo del sistema di Source esterno] è un gruppo di campi XDM (Experience Data Model) standard che estende il tipo di dati principale &#39;Attributi di controllo del sistema di Source esterno&#39; facendo riferimento alle relative proprietà e aggiungendo metadati contestuali. Ciò consente un tracciamento dettagliato dei controlli e un’integrazione flessibile dei dati da fonti esterne.

![Diagramma di schema del gruppo di campi Dettagli controllo sistema di Source esterno.](../../images/field-groups/shared/external-source-system-audit-details.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL Dettagli controllo sistema Source esterno] | `external-source-system-audit-details` | [[!UICONTROL Attributi di controllo del sistema di Source esterni]](../../data-types/external-source-system-audit-attributes.md) | Il gruppo di campi &#39;[!UICONTROL Dettagli controllo del sistema di Source esterno]&#39; estende il tipo di dati principale &#39;Attributi di controllo del sistema di Source esterno&#39; facendo riferimento alle relative proprietà e aggiungendo metadati contestuali. Questo facilita il tracciamento dettagliato dei controlli e l’integrazione flessibile dei dati per le sorgenti esterne, facilitando la natura asincrona dell’acquisizione dei profili. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Schema completo](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)