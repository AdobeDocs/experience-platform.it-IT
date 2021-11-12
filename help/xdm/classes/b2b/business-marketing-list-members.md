---
title: Classe membri elenco marketing commerciale XDM
description: Questo documento fornisce una panoramica della classe Membri elenco marketing aziendale XDM in Experience Data Model (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# [!UICONTROL Membri elenco marketing commerciale XDM] Classe

[!UICONTROL Membri elenco marketing commerciale XDM] è una classe standard Experience Data Model (XDM) che descrive membri, persone o contatti associati a un elenco di marketing.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l’appartenenza all’elenco di marketing proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `marketingListKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;elenco di marketing di cui la persona è membro. |
| `marketingListMemberKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità di appartenenza all&#39;elenco di marketing. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la persona che è membro dell&#39;elenco di marketing. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `marketingListMemberID`. |
| `marketingListID` | Stringa | Un ID univoco per l&#39;elenco di marketing. |
| `marketingListMemberID` | Stringa | Un ID univoco per l’entità di appartenenza all’elenco di marketing. |
| `personId` | Stringa | Un ID univoco per la persona. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida su [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform.
