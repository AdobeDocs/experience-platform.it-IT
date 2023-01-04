---
title: Classe campagna aziendale XDM
description: Questo documento fornisce una panoramica della classe Business Campaign XDM in Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# [!UICONTROL Campagna aziendale XDM] Classe

>[!IMPORTANT]
>
>Questa classe è destinata ad essere utilizzata dalle organizzazioni con accesso [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition per consentire a questa classe di partecipare a [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Campagna aziendale XDM] è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste per una campagna aziendale.

![Struttura della classe Business Campaign XDM visualizzata nell’interfaccia utente](../../images/classes/b2b/business-campaign.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità campagna. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se la campagna proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `campaignID`. |
| `campaignDescription` | Stringa | Una descrizione della campagna. |
| `campaignID` | Stringa | Un identificatore univoco per l&#39;entità campagna. |
| `campaignName` | Stringa | Nome della campagna. |
| `campaignType` | Stringa | Il tipo di campagna o il pubblico di destinazione. |

{style=&quot;table-layout:auto&quot;}

Per scoprire in che modo questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform, consulta la guida in [relazioni di schema in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Per ulteriori campi compatibili con questa classe, vedere il riferimento al gruppo di campi per [[!UICONTROL Dettagli della campagna aziendale XDM]](../../field-groups/b2b-campaign/details.md).
