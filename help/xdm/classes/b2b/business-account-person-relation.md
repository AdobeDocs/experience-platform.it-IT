---
title: Classe di relazione tra le persone dell'account aziendale XDM
description: Questo documento fornisce una panoramica della classe di relazione tra le persone dell’account aziendale XDM in Experience Data Model (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# [!UICONTROL Relazione personale account aziendale XDM] Classe

>[!IMPORTANT]
>
>Questa classe è destinata ad essere utilizzata dalle organizzazioni con accesso [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition per consentire a questa classe di partecipare a [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Relazione personale account aziendale XDM] è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste di una persona associata a un account aziendale.

![Struttura della classe Relazione tra persone dell&#39;account aziendale XDM visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-account-person-relation.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;account nella relazione account-persona. |
| `accountPersonKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità relazione conto-persona. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se la relazione account-persona proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `personKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per la persona nella relazione account-persona. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dagli altri campi ID acquisiti dalla classe . |
| `accountID` | Stringa | Identificatore univoco per l&#39;account nella relazione account-persona. |
| `accountPersonID` | Stringa | Identificatore univoco per l&#39;entità relazione conto-persona. |
| `currencyCode` | Stringa | Codice valuta ISO 4217 utilizzato per il rapporto tra il conto e la persona. |
| `isActive` | Booleano | Indica se la relazione tra l&#39;account e la persona è attiva. |
| `isDeleted` | Booleano | Indica se la relazione account-persona è stata eliminata nel Marketo Engage.<br><br>Quando utilizzi [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente riflessi nel Profilo del cliente in tempo reale. Tuttavia, i record relativi a tali profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query sul Data Lake. |
| `isDirect` | Booleano | Indica se si tratta di una relazione diretta tra l&#39;account e la persona. |
| `isPrimary` | Booleano | Indica se la persona è il contatto principale su questo account. |
| `personID` | Stringa | Identificatore univoco per la persona nella relazione account-persona. |
| `personRoles` | Matrice di stringhe | Elenca i ruoli della persona nella relazione account-persona. |
| `relationEndDate` | DateTime | Data di fine del rapporto tra l’account e la persona. |
| `relationStartDate` | DateTime | Data di inizio della relazione tra l&#39;account e la persona. |
| `relationshipSource` | Stringa | Origine della relazione conto-persona. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida su [relazioni di schema in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform.
