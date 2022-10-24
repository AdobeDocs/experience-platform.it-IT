---
title: Classe opportunità di business XDM
description: Questo documento fornisce una panoramica della classe Opportunità aziendale XDM in Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 4%

---

# [!UICONTROL Opportunità aziendali XDM] Classe

>[!IMPORTANT]
>
>Questa classe è destinata ad essere utilizzata dalle organizzazioni con accesso [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition per consentire a questa classe di partecipare a [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Opportunità aziendali XDM] è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste di un’opportunità aziendale.

![Struttura della classe Opportunità aziendale XDM visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-opportunity.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;account a cui è associata questa opportunità. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l&#39;opportunità proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `opportunityKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità opportunità. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `opportunityID`. |
| `accountID` | Stringa | Un ID univoco per l&#39;account a cui è associata questa opportunità. |
| `isDeleted` | Booleano | Indica se l&#39;entità dell&#39;elenco di marketing è stata eliminata nel Marketo Engage.<br><br>Quando utilizzi [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente riflessi in Profilo cliente in tempo reale. Tuttavia, i record relativi a tali profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query sul Data Lake. |
| `opportunityDescription` | Stringa | Descrizione dell&#39;opportunità. |
| `opportunityID` | Stringa | Un ID univoco per l&#39;entità opportunità. |
| `opportunityName` | Stringa | Nome dell&#39;opportunità. |
| `opportunityStage` | Stringa | La fase di vendita dell&#39;opportunità. |
| `opportunityType` | Stringa | Tipo di opportunità. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida su [relazioni di schema in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform.
