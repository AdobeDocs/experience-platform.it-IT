---
title: Classe membri elenco marketing commerciale XDM
description: Questo documento fornisce una panoramica della classe Membri elenco marketing aziendale XDM in Experience Data Model (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# [!UICONTROL Membri elenco marketing commerciale XDM] Classe

>[!IMPORTANT]
>
>Questa classe è destinata ad essere utilizzata dalle organizzazioni con accesso [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-time CDP B2B Edition per consentire a questa classe di partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Membri elenco marketing commerciale XDM] è una classe standard Experience Data Model (XDM) che descrive membri, persone o contatti associati a un elenco di marketing.

![Struttura della classe Membri elenco marketing aziendale XDM visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-marketing-list-members.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l’appartenenza all’elenco di marketing proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `marketingListKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;elenco di marketing di cui la persona è membro. |
| `marketingListMemberKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità di appartenenza all&#39;elenco di marketing. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la persona che è membro dell&#39;elenco di marketing. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `marketingListMemberID`. |
| `isDeleted` | Booleano | Indica se l&#39;entità membro dell&#39;elenco di marketing è stata eliminata nel Marketo Engage.<br><br>Quando utilizzi [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente riflessi in Profilo cliente in tempo reale. Tuttavia, i record relativi a tali profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query sul Data Lake. |
| `marketingListID` | Stringa | Un ID univoco per l&#39;elenco di marketing. |
| `marketingListMemberID` | Stringa | Un ID univoco per l’entità di appartenenza all’elenco di marketing. |
| `personId` | Stringa | Un ID univoco per la persona. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida su [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform.
