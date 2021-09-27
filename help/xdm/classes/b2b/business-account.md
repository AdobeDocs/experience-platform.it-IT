---
title: Classe account business XDM
description: Questo documento fornisce una panoramica della classe Account aziendale XDM in Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%

---

# [!UICONTROL Classe ] contabile aziendale XDM

>[!NOTE]
>
>Questa classe è disponibile solo per le organizzazioni che hanno accesso a Real-time Customer Data Platform B2B Edition.

[!UICONTROL XDM Business ] Accountability una classe Experience Data Model (XDM) standard che acquisisce le proprietà minime richieste di un account aziendale.

![](../../images/classes/b2b/business-account.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità conto. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l&#39;account proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `accountID`. |
| `accountID` | Stringa | Identificatore univoco per l&#39;entità conto. |

Consulta la guida sulle [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
