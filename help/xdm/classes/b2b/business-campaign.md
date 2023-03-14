---
title: Classe della campagna aziendale XDM
description: Questo documento fornisce una panoramica della classe XDM Business Campaign in Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# [!UICONTROL Campagna aziendale XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata all&#39;utilizzo da parte di organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition affinché questa classe possa partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Campagna aziendale XDM] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di una campagna aziendale.

![Struttura della classe XDM Business Campaign visualizzata nell’interfaccia utente](../../images/classes/b2b/business-campaign.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Un identificatore composito per l’entità della campagna. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di sorgente esterna]](../../data-types/external-source-system-audit-attributes.md) | Se la campagna proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `campaignID`. |
| `campaignDescription` | Stringa | Descrizione della campagna. |
| `campaignID` | Stringa | Un identificatore univoco per l’entità della campagna. |
| `campaignName` | Stringa | Nome della campagna. |
| `campaignType` | Stringa | Il tipo di campagna o il pubblico di destinazione. |

{style="table-layout:auto"}

Per scoprire la correlazione concettuale di questa classe con le altre classi B2B e come stabilire queste relazioni nell’interfaccia utente di Adobe Experience Platform, consulta la guida su [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Per ulteriori campi compatibili con questa classe, consulta il riferimento al gruppo di campi per [[!UICONTROL Dettagli della campagna aziendale XDM]](../../field-groups/b2b-campaign/details.md).
