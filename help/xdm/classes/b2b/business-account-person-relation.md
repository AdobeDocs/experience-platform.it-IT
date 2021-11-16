---
title: Classe di relazione tra le persone dell'account aziendale XDM
description: Questo documento fornisce una panoramica della classe di relazione tra le persone dell’account aziendale XDM in Experience Data Model (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# [!UICONTROL Relazione personale account aziendale XDM] Classe

>[!IMPORTANT]
>
>Questa classe è destinata ad essere utilizzata dalle organizzazioni con accesso [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-time CDP B2B Edition per consentire a questa classe di partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Relazione personale account aziendale XDM] è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste di una persona associata a un account aziendale.

![](../../images/classes/b2b/business-account-person-relation.png)

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
| `isDirect` | Booleano | Indica se si tratta di una relazione diretta tra l&#39;account e la persona. |
| `isPrimary` | Booleano | Indica se la persona è il contatto principale su questo account. |
| `personID` | Stringa | Identificatore univoco per la persona nella relazione account-persona. |
| `personRole` | Stringa | Il ruolo della persona nella relazione account-persona. |
| `relationEndDate` | DateTime | Data di fine del rapporto tra l’account e la persona. |
| `relationStartDate` | DateTime | Data di inizio della relazione tra l&#39;account e la persona. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida su [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell’interfaccia utente di Adobe Experience Platform.
