---
title: Classe di relazione della persona dell’opportunità di business XDM
description: Questo documento fornisce una panoramica della classe di relazione della persona dell’opportunità di business XDM in Experience Data Model (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 3%

---

# [!UICONTROL Relazione della persona dell’opportunità di business XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata all&#39;utilizzo da parte di organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition affinché questa classe possa partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Relazione della persona dell’opportunità di business XDM] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di una persona associata a un’opportunità di business.

![Struttura della classe Persona dell’opportunità di business XDM come visualizzata nell’interfaccia utente](../../images/classes/b2b/business-opportunity-person-relation.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di sorgente esterna]](../../data-types/external-source-system-audit-attributes.md) | Se la relazione della persona aziendale proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `opportunityKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’opportunità nella relazione opportunità-persona. |
| `opportunityPersonKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’entità di relazione opportunità-persona. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito della persona nella relazione opportunità-persona. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dagli altri campi ID acquisiti dalla classe. |
| `isDeleted` | Booleano | Indica se l&#39;entità dell&#39;elenco di marketing è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati in Real-Time Customer Profile. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `isPrimary` | Booleano | Indica se la persona è il contatto principale per questa opportunità. |
| `opportunityID` | Stringa | Identificatore univoco dell’opportunità nella relazione opportunità-persona. |
| `opportunityPersonID` | Stringa | Identificatore univoco per l’entità di relazione opportunità-persona |
| `personID` | Stringa | Identificatore univoco della persona nella relazione opportunità-persona. |
| `personRole` | Stringa | Il ruolo della persona nella relazione opportunità-persona. |

{style="table-layout:auto"}

Consulta la guida su [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come è possibile stabilire queste relazioni nell’interfaccia utente di Adobe Experience Platform.
