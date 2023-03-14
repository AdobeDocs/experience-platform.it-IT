---
title: Classe elenco di marketing aziendale XDM
description: Questo documento fornisce una panoramica della classe XDM Business Marketing List in Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 2%

---

# [!UICONTROL Elenco di marketing aziendale XDM] classe

>[!IMPORTANT]
>
>Questa classe è destinata all&#39;utilizzo da parte di organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). È necessario avere accesso a Real-Time CDP B2B Edition affinché questa classe possa partecipare [Profilo cliente in tempo reale](../../../profile/home.md).

[!UICONTROL Elenco di marketing aziendale XDM] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di un elenco di marketing. Gli elenchi di marketing ti consentono di dare la priorità ai potenziali clienti che hanno maggiori probabilità di acquistare il tuo prodotto.

![Struttura della classe XDM Business Marketing List visualizzata nell’interfaccia utente](../../images/classes/b2b/business-marketing-list.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di sorgente esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l’elenco di marketing proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `marketingListKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Un identificatore composito per l’entità dell’elenco di marketing. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato dal `marketingListID`. |
| `isDeleted` | Booleano | Indica se l&#39;entità dell&#39;elenco di marketing è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza [Connettore sorgente Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati in Real-Time Customer Profile. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Per impostazione `isDeleted` a `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `marketingListDescription` | Stringa | Descrizione dell&#39;elenco di marketing. |
| `marketingListID` | Stringa | ID univoco dell’entità dell’elenco di marketing. |
| `marketingListName` | Stringa | Nome dell’elenco di marketing. |

{style="table-layout:auto"}

Consulta la guida su [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come è possibile stabilire queste relazioni nell’interfaccia utente di Adobe Experience Platform.
