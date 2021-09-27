---
title: Classe membri della campagna aziendale XDM
description: Questo documento fornisce una panoramica della classe Membri di Business Campaign XDM in Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---

# [!UICONTROL Classe di ] appartenenza a una campagna aziendale XDM

>[!NOTE]
>
>Questa classe è disponibile solo per le organizzazioni che hanno accesso a Real-time Customer Data Platform B2B Edition.

[!UICONTROL XDM Business Campaign ] Membersis una classe standard Experience Data Model (XDM) che descrive un contatto o un lead associato a una campagna aziendale.

![](../../images/classes/b2b/business-campaign-members.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la campagna associata. |
| `campaignMemberKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità di appartenenza alla campagna. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l&#39;appartenenza alla campagna proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per quel sistema. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la persona che è membro della campagna associata. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `campaignMemberID`. |
| `campaignID` | Stringa | Un ID univoco per la campagna associata. |
| `campaignMemberID` | Stringa | Un ID univoco per l&#39;entità di appartenenza alla campagna. |
| `personId` | Stringa | Un ID univoco per la persona che è membro della campagna associata. |

Consulta la guida sulle [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
