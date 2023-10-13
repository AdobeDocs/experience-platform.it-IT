---
title: Tipo di dati attributi di controllo del sistema di sorgente esterna
description: Questo documento fornisce una panoramica del tipo di dati Attributi di controllo del sistema di sorgente esterna Experience Data Model (XDM).
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: a7e6ebfe09566e6e027b13efc95dda97ff8f0315
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 3%

---

# [!UICONTROL Attributi di controllo del sistema di sorgente esterna] tipo di dati

[!UICONTROL Attributi di controllo del sistema di sorgente esterna] è un tipo di dati Experience Data Model (XDM) standard che acquisisce dettagli di audit su un sistema di origine esterno.

![](../images/data-types/external-source-system-audit-attributes.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Origine B2B]](./b2b-source.md) | Identificatore composito per l&#39;origine utilizzata per il controllo. |
| `createdBy` | Stringa | Nome dell&#39;utente che ha creato il record. |
| `createdDate` | DateTime | Data di creazione del record. |
| `externalID` | Stringa | Identificatore univoco esterno per la sorgente. Questo valore viene utilizzato per identificare e deduplicare, se necessario. |
| `lastActivityDate` | DateTime | Data dell’ultima attività per il sistema di origine. |
| `lastReferencedDate` | DateTime | Ultima data di riferimento per il sistema di origine. |
| `lastUpdatedBy` | Stringa | Nome dell&#39;ultima persona che ha aggiornato il record. |
| `lastUpdatedDate` | DateTime | Data dell’ultimo aggiornamento per il sistema di origine. |
| `lastViewedDate` | DateTime | Data dell&#39;ultima visualizzazione per il sistema di origine. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
