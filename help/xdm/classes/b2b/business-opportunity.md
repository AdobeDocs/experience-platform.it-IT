---
title: Classe opportunità di business XDM
description: Questo documento fornisce una panoramica della classe Opportunità aziendale XDM in Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 5%

---

# [!UICONTROL Business ] Opportunityclass XDM (Beta)

>[!IMPORTANT]
>
>Questa classe è disponibile come parte di Real-time Customer Data Platform B2B Edition, attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

[!UICONTROL XDM Business ] Opportunityè una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste di un’opportunità aziendale.

![](../../images/classes/b2b/business-opportunity.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;account a cui è associata questa opportunità. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l&#39;opportunità proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `opportunityKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità opportunità. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `opportunityID`. |
| `accountID` | Stringa | Un ID univoco per l&#39;account a cui è associata questa opportunità. |
| `opportunityDescription` | Stringa | Descrizione dell&#39;opportunità. |
| `opportunityID` | Stringa | Un ID univoco per l&#39;entità opportunità. |
| `opportunityName` | Stringa | Nome dell&#39;opportunità. |
| `opportunityStage` | Stringa | La fase di vendita dell&#39;opportunità. |
| `opportunityType` | Stringa | Tipo di opportunità. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida sulle [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
