---
title: Classe membri della campagna aziendale XDM
description: Questo documento fornisce una panoramica della classe Membri di Business Campaign XDM in Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---

# [!UICONTROL Classe di ] appartenenza a una campagna aziendale XDM

>[!NOTE]
>
>Questa classe è disponibile solo per le organizzazioni che hanno accesso all’edizione B2B di Real-time Customer Data Platform.

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
