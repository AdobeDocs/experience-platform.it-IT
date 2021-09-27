---
title: Classe campagna aziendale XDM
description: Questo documento fornisce una panoramica della classe Business Campaign XDM in Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 3%

---

# [!UICONTROL Classe Business ] Campaign XDM

>[!NOTE]
>
>Questa classe è disponibile solo per le organizzazioni che hanno accesso a Real-time Customer Data Platform B2B Edition.

[!UICONTROL XDM Business ] Campaign è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste per una campagna aziendale.

![](../../images/classes/b2b/business-campaign.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità campagna. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se la campagna proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `campaignID`. |
| `campaignDescription` | Stringa | Una descrizione della campagna. |
| `campaignID` | Stringa | Un identificatore univoco per l&#39;entità campagna. |
| `campaignName` | Stringa | Nome della campagna. |
| `campaignType` | Stringa | Il tipo di campagna o il pubblico di destinazione. |

Consulta la guida sulle [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
