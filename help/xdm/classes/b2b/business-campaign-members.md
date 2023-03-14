---
title: Classe membri della campagna aziendale XDM
description: Questo documento fornisce una panoramica della classe XDM Business Campaign Members in Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 2%

---

# [!UICONTROL Membri della campagna aziendale XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata all&#39;utilizzo da parte di organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition affinché questa classe possa partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Membri della campagna aziendale XDM] è una classe XDM (Experience Data Model) standard che descrive un contatto o un lead associato a una campagna aziendale.

![Struttura della classe XDM Business Campaign Members visualizzata nell’interfaccia utente](../../images/classes/b2b/business-campaign-members.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Un identificatore composito per la campagna associata. |
| `campaignMemberKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’entità di iscrizione alla campagna. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di sorgente esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l’appartenenza alla campagna proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Un identificatore composito per la persona che è membro della campagna associata. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `campaignMemberID`. |

{style="table-layout:auto"}

Per scoprire la correlazione concettuale di questa classe con le altre classi B2B e come stabilire queste relazioni nell’interfaccia utente di Adobe Experience Platform, consulta la guida su [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Per ulteriori campi compatibili con questa classe, consulta il riferimento al gruppo di campi per [[!UICONTROL Dettagli del membro della campagna aziendale XDM]](../../field-groups/b2b-campaign-members/details.md).
