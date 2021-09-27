---
title: Classe membri elenco marketing commerciale XDM
description: Questo documento fornisce una panoramica della classe Membri elenco marketing aziendale XDM in Experience Data Model (XDM).
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# [!UICONTROL Classe di ] appartenenza all’elenco di marketing aziendale XDM (Beta)

>[!IMPORTANT]
>
>Questa classe è disponibile come parte di Real-time Customer Data Platform B2B Edition, attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

[!UICONTROL XDM Business Marketing List ] Membersis una classe standard Experience Data Model (XDM) che descrive membri, persone o contatti associati a un elenco di marketing.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l’appartenenza all’elenco di marketing proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `marketingListKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;elenco di marketing di cui la persona è membro. |
| `marketingListMemberKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità di appartenenza all&#39;elenco di marketing. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la persona che è membro dell&#39;elenco di marketing. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `marketingListMemberID`. |
| `marketingListID` | Stringa | Un ID univoco per l&#39;elenco di marketing. |
| `marketingListMemberID` | Stringa | Un ID univoco per l’entità di appartenenza all’elenco di marketing. |
| `personId` | Stringa | Un ID univoco per la persona. |

Consulta la guida sulle [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
