---
title: Classe elenco di marketing aziendale XDM
description: Scopri la classe XDM Business Marketing List in Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# Classe [!UICONTROL Elenco marketing aziendale XDM]

>[!IMPORTANT]
>
>Questa classe è destinata alle organizzazioni con accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Per consentire a questa classe di partecipare a [Real-Time Customer Profile](../../../profile/home.md), è necessario avere accesso a Real-Time CDP B2B Edition.

[!UICONTROL XDM Business Marketing List] è una classe XDM (Experience Data Model) standard che acquisisce le proprietà minime richieste di un elenco di marketing. Gli elenchi di marketing ti consentono di dare la priorità ai potenziali clienti che hanno maggiori probabilità di acquistare il tuo prodotto.

![Struttura della classe XDM Business Marketing List visualizzata nell&#39;interfaccia utente](../../images/classes/b2b/business-marketing-list.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di Source esterni]](../../data-types/external-source-system-audit-attributes.md) | Se l’elenco di marketing proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Un identificatore composito per l’entità dell’elenco di marketing. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `marketingListID`. |
| `isDeleted` | Booleano | Indica se l&#39;entità dell&#39;elenco di marketing è stata eliminata nel Marketo Engage.<br><br>Quando si utilizza il [connettore di origine di Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tutti i record eliminati in Marketo vengono automaticamente rispecchiati nel profilo cliente in tempo reale. Tuttavia, i record relativi a questi profili possono ancora persistere nel Data Lake. Impostando `isDeleted` su `true`, è possibile utilizzare il campo per filtrare i record eliminati dalle origini durante la query nel Data Lake. |
| `marketingListDescription` | Stringa | Descrizione dell&#39;elenco di marketing. |
| `marketingListID` | Stringa | ID univoco dell’entità dell’elenco di marketing. |
| `marketingListName` | Stringa | Nome dell’elenco di marketing. |

{style="table-layout:auto"}

Consulta la guida sulle [relazioni tra schemi in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente con le altre classi B2B e come è possibile stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
