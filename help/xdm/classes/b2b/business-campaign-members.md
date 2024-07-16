---
title: Classe membri della campagna aziendale XDM
description: Scopri la classe XDM Business Campaign Members in Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# [!UICONTROL Membri della campagna aziendale XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata alle organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Per consentire a questa classe di partecipare a [Real-Time Customer Profile](../../../profile/home.md), è necessario avere accesso a Real-Time CDP B2B Edition.

[!UICONTROL Membri della campagna aziendale XDM] è una classe XDM (Experience Data Model) standard che descrive un contatto o un lead associato a una campagna aziendale.

![Struttura della classe Membri della campagna aziendale XDM come visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-campaign-members.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificatore composito per la campagna associata. |
| `campaignMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’entità di iscrizione alla campagna. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di Source esterni]](../../data-types/external-source-system-audit-attributes.md) | Se l’appartenenza alla campagna proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificatore composito per la persona che è membro della campagna associata. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `campaignMemberID`. |

{style="table-layout:auto"}

Per informazioni sulla correlazione concettuale tra questa classe e le altre classi B2B e su come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform, vedere la guida alle [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Per ulteriori campi compatibili con questa classe, vedere il riferimento al gruppo di campi per [[!UICONTROL Dettagli membro della campagna aziendale XDM]](../../field-groups/b2b-campaign-members/details.md).
