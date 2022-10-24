---
title: Tipo di dati attributi di audit del sistema di origine esterna
description: Questo documento fornisce una panoramica del tipo di dati XDM (External Source System Audit Attributes Experience Data Model).
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 3%

---

# [!UICONTROL Attributi di controllo del sistema di origine esterna] tipo di dati

>[!NOTE]
>
>Questo tipo di dati è disponibile solo per le organizzazioni che hanno accesso all’edizione B2B di Adobe Real-time Customer Data Platform.

[!UICONTROL Attributi di controllo del sistema di origine esterna] è un tipo di dati XDM (Experience Data Model) standard che acquisisce i dettagli di controllo relativi a un sistema sorgente esterno.

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
