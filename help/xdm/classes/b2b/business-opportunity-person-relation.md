---
title: Classe di relazione tra persone opportunità aziendali XDM
description: Questo documento fornisce una panoramica della classe di relazione tra le persone opportunità commerciali XDM in Experience Data Model (XDM).
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---

# [!UICONTROL Classe di ] relazione tra persone opportunità aziendali XDM (Beta)

>[!IMPORTANT]
>
>Questa classe è disponibile come parte di Real-time Customer Data Platform B2B Edition, attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

[!UICONTROL XDM Business Opportunity Person ] Relationship è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste di una persona associata a un&#39;opportunità aziendale.

![](../../images/classes/b2b/business-opportunity-person-relation.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se la relazione uomo-lavoro proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `opportunityKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;opportunità nel rapporto persona-opportunità. |
| `opportunityPersonKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità relazione persona-opportunità. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la persona nella relazione persona-opportunità. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dagli altri campi ID acquisiti dalla classe . |
| `opportunityID` | Stringa | Identificatore univoco per l&#39;opportunità nella relazione persona-opportunità. |
| `opportunityPersonID` | Stringa | Identificatore univoco per l&#39;entità relazione persona-opportunità |
| `isPrimary` | Booleano | Indica se la persona è il contatto principale per questa opportunità. |
| `personID` | Stringa | Identificatore univoco per la persona nella relazione persona-opportunità. |
| `personRole` | Stringa | Il ruolo della persona nel rapporto opportunità-persona. |

Consulta la guida sulle [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
