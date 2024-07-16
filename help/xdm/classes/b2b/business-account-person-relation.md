---
title: Classe di relazione della persona dell’account aziendale XDM
description: Scopri la classe di relazione della persona dell’account aziendale XDM in Experience Data Model (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 12%

---

# [!UICONTROL Relazione della persona dell&#39;account aziendale XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata alle organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Per consentire a questa classe di partecipare a [Real-Time Customer Profile](../../../profile/home.md), è necessario avere accesso a Real-Time CDP B2B Edition.

[!UICONTROL La relazione della persona dell&#39;account aziendale XDM] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di una persona associata a un account aziendale.

![Struttura della classe di relazione della persona dell&#39;account aziendale XDM come visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-account-person-relation.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito dell’account nella relazione account-persona. |
| `accountPersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’entità di relazione account-persona. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di Source esterni]](../../data-types/external-source-system-audit-attributes.md) | Se la relazione account-persona proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identificatore composito della persona nella relazione account-persona. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dagli altri campi ID acquisiti dalla classe. |
| `accountID` | Stringa | Identificatore univoco dell’account nella relazione account-persona. |
| `accountPersonID` | Stringa | Identificatore univoco per l’entità di relazione account-persona. |
| `currencyCode` | Stringa | Il codice valuta ISO 4217 utilizzato per la relazione tra l’account e la persona. |
| `isActive` | Booleano | Indica se la relazione tra l’account e la persona è attiva. |
| `isDeleted` | Booleano | Indica se la relazione account-persona è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza il [connettore di origine di Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati nel profilo cliente in tempo reale. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Impostando `isDeleted` su `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `isDirect` | Booleano | Indica se si tratta di una relazione diretta tra l’account e la persona. |
| `isPrimary` | Booleano | Indica se la persona è il contatto principale in questo account. |
| `personID` | Stringa | Identificatore univoco della persona nella relazione account-persona. |
| `personRoles` | Array di stringhe | Elenca i ruoli della persona nella relazione account-persona. |
| `relationEndDate` | Data e ora | La data in cui è terminata la relazione tra l’account e la persona. |
| `relationStartDate` | Data e ora | La data in cui è iniziata la relazione tra l’account e la persona. |
| `relationshipSource` | Stringa | Origine della relazione account-persona. |

{style="table-layout:auto"}

Consulta la guida sulle [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente con le altre classi B2B e come è possibile stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
