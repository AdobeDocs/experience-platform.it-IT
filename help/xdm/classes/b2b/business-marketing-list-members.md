---
title: Classe membri dell’elenco di marketing aziendale XDM
description: Scopri la classe XDM Business Marketing List Members in Experience Data Model (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 2%

---

# [!UICONTROL Membri elenco di marketing aziendale XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata alle organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Per consentire a questa classe di partecipare a [Real-Time Customer Profile](../../../profile/home.md), è necessario avere accesso a Real-Time CDP B2B Edition.

[!UICONTROL Membri elenco di marketing aziendale XDM] è una classe XDM (Experience Data Model) standard che descrive membri, persone o contatti associati a un elenco di marketing.

![La struttura della classe dei membri dell&#39;elenco di marketing aziendale XDM così come viene visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-marketing-list-members.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di Source esterni]](../../data-types/external-source-system-audit-attributes.md) | Se l’appartenenza all’elenco di marketing proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di audit per tale sistema. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificatore composito per l’elenco di marketing di cui la persona è membro. |
| `marketingListMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’entità di appartenenza all’elenco di marketing. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificatore composito per la persona che è membro dell’elenco di marketing. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `marketingListMemberID`. |
| `isDeleted` | Booleano | Indica se l&#39;entità membro dell&#39;elenco di marketing è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza il [connettore di origine di Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati nel profilo cliente in tempo reale. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Impostando `isDeleted` su `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `marketingListID` | Stringa | Un ID univoco per l’elenco di marketing. |
| `marketingListMemberID` | Stringa | ID univoco dell’entità di iscrizione all’elenco di marketing. |
| `personId` | Stringa | ID univoco della persona. |

{style="table-layout:auto"}

Consulta la guida sulle [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente con le altre classi B2B e come è possibile stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
