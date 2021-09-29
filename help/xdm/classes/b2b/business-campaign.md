---
title: Classe campagna aziendale XDM
description: Questo documento fornisce una panoramica della classe Business Campaign XDM in Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 5%

---

# [!UICONTROL Classe Business ] Campaign XDM (Beta)

>[!IMPORTANT]
>
>Questa classe è disponibile come parte di Real-time Customer Data Platform B2B Edition, attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

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

{style=&quot;table-layout:auto&quot;}

Consulta la guida sulle [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
