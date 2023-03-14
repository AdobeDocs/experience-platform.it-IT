---
title: Classe di opportunità di business XDM
description: Questo documento fornisce una panoramica della classe XDM Business Opportunity in Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 3%

---

# [!UICONTROL Opportunità di business XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata all&#39;utilizzo da parte di organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition affinché questa classe possa partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Opportunità di business XDM] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di un’opportunità di business.

![Struttura della classe XDM Business Opportunity visualizzata nell’interfaccia utente](../../images/classes/b2b/business-opportunity.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito dell’account a cui è associata questa opportunità. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di sorgente esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l’opportunità proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `opportunityKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’entità opportunità. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `opportunityID`. |
| `accountID` | Stringa | ID univoco dell’account a cui è associata questa opportunità. |
| `isDeleted` | Booleano | Indica se l&#39;entità dell&#39;elenco di marketing è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati in Real-Time Customer Profile. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `opportunityDescription` | Stringa | Descrizione dell&#39;opportunità. |
| `opportunityID` | Stringa | Un ID univoco per l’entità opportunità. |
| `opportunityName` | Stringa | Nome dell’opportunità. |
| `opportunityStage` | Stringa | Fase di vendita dell’opportunità. |
| `opportunityType` | Stringa | Il tipo di opportunità. |

{style="table-layout:auto"}

Consulta la guida su [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come è possibile stabilire queste relazioni nell’interfaccia utente di Adobe Experience Platform.
