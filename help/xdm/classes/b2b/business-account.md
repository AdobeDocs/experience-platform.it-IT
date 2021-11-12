---
title: Classe account business XDM
description: Questo documento fornisce una panoramica della classe Account aziendale XDM in Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%

---

# [!UICONTROL Account aziendale XDM] Classe

[!UICONTROL Account aziendale XDM] è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste di un account aziendale.

![](../../images/classes/b2b/business-account.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità conto. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l&#39;account proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `accountID`. |
| `accountID` | Stringa | Identificatore univoco per l&#39;entità conto. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida su [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform.
