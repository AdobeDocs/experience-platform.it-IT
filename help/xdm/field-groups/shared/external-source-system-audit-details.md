---
title: Dettagli sul controllo del sistema Source esterno
description: Scopri il gruppo di campi Dettagli audit sistema Source esterno Experience Data Model (XDM).
exl-id: 6aa154f3-620f-4a2e-9e33-a0757d0491c1
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 4%

---

# Gruppo di campi [!UICONTROL External Source System Audit Details]

[!UICONTROL External Source System Audit Details] è un gruppo di campi XDM (Experience Data Model) standard che estende il tipo di dati principale &#39;Attributi di controllo del sistema di Source esterno&#39; facendo riferimento alle relative proprietà e aggiungendo metadati contestuali. Ciò consente un tracciamento dettagliato dei controlli e un’integrazione flessibile dei dati da fonti esterne.

![Diagramma di schema del gruppo di campi Dettagli controllo sistema di Source esterno.](../../images/field-groups/shared/external-source-system-audit-details.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL External Source System Audit Details] | `external-source-system-audit-details` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Il gruppo di campi &#39;[!UICONTROL External Source System Audit Details]&#39; estende il tipo di dati principale &#39;External Source System Audit Attributes&#39; facendo riferimento alle relative proprietà e aggiungendo metadati contestuali. Questo facilita il tracciamento dettagliato dei controlli e l’integrazione flessibile dei dati per le sorgenti esterne, facilitando la natura asincrona dell’acquisizione dei profili. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Schema completo](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)
