---
title: Classe di relazione della persona dell’opportunità di business XDM
description: Scopri la classe di relazione della persona dell’opportunità di business XDM in Experience Data Model (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 3%

---

# [!UICONTROL Relazione persona opportunità di business XDM]

>[!IMPORTANT]
>
>Questa classe è destinata alle organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Per consentire a questa classe di partecipare a [Real-Time Customer Profile](../../../profile/home.md), è necessario avere accesso a Real-Time CDP B2B Edition.

[!UICONTROL La relazione della persona dell&#39;opportunità di business XDM] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di una persona associata a un&#39;opportunità di business.

![Struttura della classe Persona dell&#39;opportunità di business XDM come visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-opportunity-person-relation.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di Source esterni]](../../data-types/external-source-system-audit-attributes.md) | Se la relazione della persona aziendale proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `opportunityKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’opportunità nella relazione opportunità-persona. |
| `opportunityPersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’entità di relazione opportunità-persona. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito della persona nella relazione opportunità-persona. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dagli altri campi ID acquisiti dalla classe. |
| `isDeleted` | Booleano | Indica se l&#39;entità dell&#39;elenco di marketing è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza il [connettore di origine di Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati nel profilo cliente in tempo reale. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Impostando `isDeleted` su `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `isPrimary` | Booleano | Indica se la persona è il contatto principale per questa opportunità. |
| `opportunityID` | Stringa | Identificatore univoco dell’opportunità nella relazione opportunità-persona. |
| `opportunityPersonID` | Stringa | Identificatore univoco per l’entità di relazione opportunità-persona |
| `personID` | Stringa | Identificatore univoco della persona nella relazione opportunità-persona. |
| `personRole` | Stringa | Il ruolo della persona nella relazione opportunità-persona. |

{style="table-layout:auto"}

Consulta la guida sulle [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente con le altre classi B2B e come è possibile stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
