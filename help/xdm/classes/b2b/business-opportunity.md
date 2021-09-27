---
title: Classe opportunità di business XDM
description: Questo documento fornisce una panoramica della classe Opportunità aziendale XDM in Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 4%

---

# [!UICONTROL Classe ] opportunità aziendale XDM

>[!NOTE]
>
>Questa classe è disponibile solo per le organizzazioni che hanno accesso a Real-time Customer Data Platform B2B Edition.

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

Consulta la guida sulle [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
