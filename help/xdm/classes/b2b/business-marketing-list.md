---
title: Classe elenco marketing aziendale XDM
description: Questo documento fornisce una panoramica della classe XDM Business Marketing List in Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL Classe ] elenco marketing aziendale XDM

>[!NOTE]
>
>Questa classe è disponibile solo per le organizzazioni che hanno accesso all’edizione B2B di Real-time Customer Data Platform.

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
