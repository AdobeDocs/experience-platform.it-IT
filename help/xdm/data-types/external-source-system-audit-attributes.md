---
title: Tipo di dati attributi di audit del sistema di origine esterna
description: Questo documento fornisce una panoramica del tipo di dati XDM (External Source System Audit Attributes Experience Data Model).
source-git-commit: 8bf0c63f33ae9cbfb01d4db9e5220c6762575c5b
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 3%

---

# [!UICONTROL Tipo di dati Audit ] Attributesdata del sistema di origine esterna

>[!NOTE]
>
>Questo tipo di dati è disponibile solo per le organizzazioni che hanno accesso all’edizione B2B di Real-time Customer Data Platform.

[!UICONTROL External Source System Audit ] Attributesis è un tipo di dati XDM (Experience Data Model) standard che acquisisce i dettagli di controllo relativi a un sistema sorgente esterno.

![](../images/data-types/external-source-system-audit-attributes.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Origine B2B]](./b2b-source.md) | Identificatore composito per l&#39;origine utilizzata per il controllo. |
| `createdBy` | Stringa | Nome dell&#39;utente che ha creato il record. |
| `createdDate` | DateTime | Data di creazione del record. |
| `externalID` | Stringa | Identificatore univoco esterno per l&#39;origine. Questo valore viene utilizzato per identificare e deduplicare se necessario. |
| `lastActivityDate` | DateTime | Data dell’ultima attività per il sistema di origine. |
| `lastReferencedDate` | DateTime | Data ultimo riferimento per il sistema di origine. |
| `lastUpdatedBy` | Stringa | Nome dell&#39;ultima persona che ha aggiornato il record. |
| `lastUpdatedDate` | DateTime | Data ultimo aggiornamento del sistema di origine. |
| `lastViewedDate` | DateTime | Data dell&#39;ultima visualizzazione del sistema di origine. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
