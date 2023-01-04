---
title: Classe account business XDM
description: Questo documento fornisce una panoramica della classe Account aziendale XDM in Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 3%

---

# [!UICONTROL Account aziendale XDM] Classe

>[!IMPORTANT]
>
>Questa classe è destinata ad essere utilizzata dalle organizzazioni con accesso [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition per consentire a questa classe di partecipare a [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Account aziendale XDM] è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste di un account aziendale.

![Struttura della classe Account aziendale XDM visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-account.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità conto. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l&#39;account proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `accountKey` identificatore . |
| `isDeleted` | Booleano | Indica se l&#39;entità account è stata eliminata nel Marketo Engage.<br><br>Quando utilizzi [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente riflessi nel Profilo del cliente in tempo reale. Tuttavia, i record relativi a tali profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query sul Data Lake. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida su [relazioni di schema in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform.
