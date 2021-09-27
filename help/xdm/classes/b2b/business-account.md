---
title: Classe account business XDM
description: Questo documento fornisce una panoramica della classe Account aziendale XDM in Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL Classe ] contabile aziendale XDM

>[!NOTE]
>
>Questa classe è disponibile solo per le organizzazioni che hanno accesso all’edizione B2B di Real-time Customer Data Platform.

[!UICONTROL XDM Business ] Accountability una classe Experience Data Model (XDM) standard che acquisisce le proprietà minime richieste di un account aziendale.

![](../../images/classes/b2b/business-account.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origine B2B]](../../data-types/b2b-source.md) | Identificatore composito per l&#39;entità conto. |
| `extSourceSystemAudit` | [[!UICONTROL Attributi di controllo del sistema di origine esterna]](../../data-types/external-source-system-audit-attributes.md) | Se l&#39;account proviene da un sistema di origine esterno, questo oggetto acquisisce gli attributi di controllo per tale sistema. |
| `_id` | Stringa | Identificatore univoco del record. Si tratta di un valore generato dal sistema e separato da `accountID`. |
| `accountID` | Stringa | Identificatore univoco per l&#39;entità conto. |
