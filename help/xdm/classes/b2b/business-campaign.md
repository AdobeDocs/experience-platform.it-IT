---
title: Classe della campagna aziendale XDM
description: Scopri la classe della campagna aziendale XDM in Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# Classe [!UICONTROL XDM Business Campaign]

>[!IMPORTANT]
>
>Questa classe è destinata alle organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Per consentire a questa classe di partecipare a [Real-Time Customer Profile](../../../profile/home.md), è necessario avere accesso a Real-Time CDP B2B Edition.

[!UICONTROL XDM Business Campaign] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di una campagna aziendale.

![Struttura della classe XDM Business Campaign visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-campaign.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificatore composito per l’entità della campagna. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di Source esterni]](../../data-types/external-source-system-audit-attributes.md) | Se la campagna proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `campaignID`. |
| `campaignDescription` | Stringa | Descrizione della campagna. |
| `campaignID` | Stringa | Un identificatore univoco per l’entità della campagna. |
| `campaignName` | Stringa | Nome della campagna. |
| `campaignType` | Stringa | Il tipo di campagna o il pubblico di destinazione. |

{style="table-layout:auto"}

Per informazioni sulla correlazione concettuale tra questa classe e le altre classi B2B e su come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform, vedere la guida alle [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Per ulteriori campi compatibili con questa classe, vedere il riferimento al gruppo di campi per [[!UICONTROL Dettagli campagna aziendale XDM]](../../field-groups/b2b-campaign/details.md).
