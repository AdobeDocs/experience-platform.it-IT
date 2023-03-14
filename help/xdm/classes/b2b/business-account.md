---
title: Classe account aziendale XDM
description: Questo documento fornisce una panoramica della classe XDM Business Account in Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 2%

---

# [!UICONTROL Account aziendale XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata all&#39;utilizzo da parte di organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition affinché questa classe possa partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Account aziendale XDM] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di un account aziendale.

![Struttura della classe XDM Business Account visualizzata nell’interfaccia utente](../../images/classes/b2b/business-account.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’entità account. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di sorgente esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l’account proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `accountKey` identificatore. |
| `isDeleted` | Booleano | Indica se l&#39;entità conto è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati in Real-Time Customer Profile. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |

{style="table-layout:auto"}

Consulta la guida su [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come è possibile stabilire queste relazioni nell’interfaccia utente di Adobe Experience Platform.
