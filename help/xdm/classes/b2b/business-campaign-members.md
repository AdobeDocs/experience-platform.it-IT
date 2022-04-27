---
title: Classe membri della campagna aziendale XDM
description: Questo documento fornisce una panoramica della classe Membri di Business Campaign XDM in Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---

# [!UICONTROL Membri di una campagna aziendale XDM] Classe

>[!IMPORTANT]
>
>Questa classe è destinata ad essere utilizzata dalle organizzazioni con accesso [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-time CDP B2B Edition per consentire a questa classe di partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Membri di una campagna aziendale XDM] è una classe standard Experience Data Model (XDM) che descrive un contatto o un lead associato a una campagna aziendale.

![Struttura della classe Membri di Business Campaign XDM visualizzata nell’interfaccia utente](../../images/classes/b2b/business-campaign-members.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la campagna associata. |
| `campaignMemberKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità di appartenenza alla campagna. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l&#39;appartenenza alla campagna proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per quel sistema. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la persona che è membro della campagna associata. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `campaignMemberID`. |

{style=&quot;table-layout:auto&quot;}

Per scoprire in che modo questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform, consulta la guida in [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Per ulteriori campi compatibili con questa classe, vedere il riferimento al gruppo di campi per [[!UICONTROL Dettagli membri della campagna aziendale XDM]](../../field-groups/b2b-campaign-members/details.md).
