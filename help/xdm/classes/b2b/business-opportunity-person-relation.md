---
title: Classe di relazione tra persone opportunità aziendali XDM
description: Questo documento fornisce una panoramica della classe di relazione tra le persone opportunità commerciali XDM in Experience Data Model (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 3%

---

# [!UICONTROL Relazione personale opportunità di business XDM] Classe

>[!IMPORTANT]
>
>Questa classe è destinata ad essere utilizzata dalle organizzazioni con accesso [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-time CDP B2B Edition per consentire a questa classe di partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Relazione personale opportunità di business XDM] è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste di una persona associata a un’opportunità di business.

![Struttura della classe Business Opportunity Person XDM visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-opportunity-person-relation.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se la relazione uomo-lavoro proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `opportunityKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;opportunità nel rapporto persona-opportunità. |
| `opportunityPersonKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità relazione persona-opportunità. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la persona nella relazione persona-opportunità. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dagli altri campi ID acquisiti dalla classe . |
| `isDeleted` | Booleano | Indica se l&#39;entità dell&#39;elenco di marketing è stata eliminata nel Marketo Engage.<br><br>Quando utilizzi [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente riflessi in Profilo cliente in tempo reale. Tuttavia, i record relativi a tali profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query sul Data Lake. |
| `isPrimary` | Booleano | Indica se la persona è il contatto principale per questa opportunità. |
| `opportunityID` | Stringa | Identificatore univoco per l&#39;opportunità nella relazione persona-opportunità. |
| `opportunityPersonID` | Stringa | Identificatore univoco per l&#39;entità relazione persona-opportunità |
| `personID` | Stringa | Identificatore univoco per la persona nella relazione persona-opportunità. |
| `personRole` | Stringa | Il ruolo della persona nel rapporto opportunità-persona. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida su [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform.
