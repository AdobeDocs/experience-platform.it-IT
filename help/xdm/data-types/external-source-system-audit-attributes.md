---
title: Tipo di dati attributi di controllo del sistema Source esterno
description: Scopri il tipo di dati Experience Data Model (XDM) per gli attributi di controllo del sistema di Source esterno.
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 03735e7099ffb2cfd44fc7fffd35e3a4a858e3ba
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 6%

---

# [!UICONTROL Tipo di dati Attributi di controllo del sistema di Source esterno]

[!UICONTROL External Source System Audit Attributes] è un tipo di dati XDM (Experience Data Model) standard che acquisisce i dettagli di controllo di un sistema di origine esterno.

![](../images/data-types/external-source-system-audit-attributes.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Source B2B]](./b2b-source.md) | Identificatore composito per l&#39;origine utilizzata per il controllo. |
| `createdBy` | Stringa | Nome dell&#39;utente che ha creato il record. |
| `createdDate` | Data e ora | Data di creazione del record. |
| `externalID` | Stringa | Identificatore univoco esterno per la sorgente. Questo valore viene utilizzato per identificare e deduplicare, se necessario. |
| `lastActivityDate` | Data e ora | Data dell’ultima attività per il sistema di origine. |
| `lastReferencedDate` | Data e ora | Ultima data di riferimento per il sistema di origine. |
| `lastUpdatedBy` | Stringa | Nome dell&#39;ultima persona che ha aggiornato il record. |
| `lastUpdatedDate` | Data e ora | Data dell’ultimo aggiornamento per il sistema di origine. Questo valore viene utilizzato dal [criterio di unione attributi](../../profile/api/merge-policies.md#attribute-merge) per determinare la priorità in caso di conflitti di unione. |
| `lastViewedDate` | Data e ora | Data dell&#39;ultima visualizzazione per il sistema di origine. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
