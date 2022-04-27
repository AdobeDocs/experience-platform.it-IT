---
title: Classe account business XDM
description: Questo documento fornisce una panoramica della classe Account aziendale XDM in Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 2%

---

# [!UICONTROL Account aziendale XDM] Classe

>[!IMPORTANT]
>
>Questa classe è destinata ad essere utilizzata dalle organizzazioni con accesso [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-time CDP B2B Edition per consentire a questa classe di partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Account aziendale XDM] è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste di un account aziendale.

![Struttura della classe Account aziendale XDM visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-account.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità conto. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l&#39;account proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `accountKey` identificatore . |
| `isDeleted` | Booleano | Indica se l&#39;entità account è stata eliminata nel Marketo Engage.<br><br>Quando utilizzi [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente riflessi in Profilo cliente in tempo reale. Tuttavia, i record relativi a tali profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query sul Data Lake. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida su [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform.
