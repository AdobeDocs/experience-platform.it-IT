---
title: Classe di relazione della persona dell’account aziendale XDM
description: Questo documento fornisce una panoramica della classe di relazione della persona dell’account aziendale XDM in Experience Data Model (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 3%

---

# [!UICONTROL Relazione della persona dell’account aziendale XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata all&#39;utilizzo da parte di organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition affinché questa classe possa partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Relazione della persona dell’account aziendale XDM] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di una persona associata a un account aziendale.

![Struttura della classe di relazione della persona dell’account aziendale XDM come visualizzata nell’interfaccia utente](../../images/classes/b2b/business-account-person-relation.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito dell’account nella relazione account-persona. |
| `accountPersonKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l’entità di relazione account-persona. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di sorgente esterna]](../../data-types/external-source-system-audit-attributes.md) | Se la relazione account-persona proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito della persona nella relazione account-persona. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dagli altri campi ID acquisiti dalla classe. |
| `accountID` | Stringa | Identificatore univoco dell’account nella relazione account-persona. |
| `accountPersonID` | Stringa | Identificatore univoco per l’entità di relazione account-persona. |
| `currencyCode` | Stringa | Il codice valuta ISO 4217 utilizzato per la relazione tra l’account e la persona. |
| `isActive` | Booleano | Indica se la relazione tra l’account e la persona è attiva. |
| `isDeleted` | Booleano | Indica se la relazione account-persona è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati in Real-Time Customer Profile. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `isDirect` | Booleano | Indica se si tratta di una relazione diretta tra l’account e la persona. |
| `isPrimary` | Booleano | Indica se la persona è il contatto principale in questo account. |
| `personID` | Stringa | Identificatore univoco della persona nella relazione account-persona. |
| `personRoles` | Array di stringhe | Elenca i ruoli della persona nella relazione account-persona. |
| `relationEndDate` | DateTime | La data in cui è terminata la relazione tra l’account e la persona. |
| `relationStartDate` | DateTime | La data in cui è iniziata la relazione tra l’account e la persona. |
| `relationshipSource` | Stringa | Origine della relazione account-persona. |

{style="table-layout:auto"}

Consulta la guida su [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come è possibile stabilire queste relazioni nell’interfaccia utente di Adobe Experience Platform.
