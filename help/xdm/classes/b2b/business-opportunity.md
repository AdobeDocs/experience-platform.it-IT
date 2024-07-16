---
title: Classe di opportunità di business XDM
description: Scopri la classe XDM Business Opportunity in Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# [!UICONTROL Opportunità di business XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata alle organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Per consentire a questa classe di partecipare a [Real-Time Customer Profile](../../../profile/home.md), è necessario avere accesso a Real-Time CDP B2B Edition.

[!UICONTROL Opportunità di business XDM] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di un&#39;opportunità di business.

![Struttura della classe dell&#39;opportunità di business XDM come visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-opportunity.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito dell’account a cui è associata questa opportunità. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di Source esterni]](../../data-types/external-source-system-audit-attributes.md) | Se l’opportunità proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `opportunityKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’entità opportunità. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `opportunityID`. |
| `accountID` | Stringa | ID univoco dell’account a cui è associata questa opportunità. |
| `isDeleted` | Booleano | Indica se l&#39;entità dell&#39;elenco di marketing è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza il [connettore di origine di Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati nel profilo cliente in tempo reale. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Impostando `isDeleted` su `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `opportunityDescription` | Stringa | Descrizione dell&#39;opportunità. |
| `opportunityID` | Stringa | Un ID univoco per l’entità opportunità. |
| `opportunityName` | Stringa | Nome dell’opportunità. |
| `opportunityStage` | Stringa | Fase di vendita dell’opportunità. |
| `opportunityType` | Stringa | Il tipo di opportunità. |

{style="table-layout:auto"}

Consulta la guida sulle [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente con le altre classi B2B e come è possibile stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
