---
title: Classe elenco marketing aziendale XDM
description: Questo documento fornisce una panoramica della classe XDM Business Marketing List in Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 4%

---

# [!UICONTROL Classe ] elenco marketing aziendale XDM (Beta)

>[!IMPORTANT]
>
>Questa classe è disponibile come parte di Real-time Customer Data Platform B2B Edition, attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

[!UICONTROL XDM Business Marketing ] List è una classe standard Experience Data Model (XDM) che acquisisce le proprietà minime richieste di un elenco di marketing. Gli elenchi di marketing ti consentono di assegnare priorità ai clienti potenziali che hanno più probabilità di acquistare il tuo prodotto.

![](../../images/classes/b2b/business-marketing-list.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l’elenco di marketing proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `marketingListKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità elenco marketing. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `marketingListID`. |
| `marketingListDescription` | Stringa | Descrizione dell’elenco di marketing. |
| `marketingListID` | Stringa | Un ID univoco per l’entità elenco marketing. |
| `marketingListName` | Stringa | Nome dell&#39;elenco di marketing. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida sulle [relazioni di schema in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) per scoprire come questa classe si relaziona concettualmente alle altre classi B2B e come stabilire tali relazioni nell&#39;interfaccia utente di Adobe Experience Platform.
