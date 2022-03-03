---
title: Gruppo campi schema dettagli richiesta preventivo
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli richiesta preventivo.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 6%

---

# [!UICONTROL Dettagli richiesta preventivo] gruppo di campi schema

[!UICONTROL Dettagli richiesta preventivo] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo `quotes` oggetto di uno schema che acquisisce i dettagli del processo di richiesta per vari tipi di preventivi, inclusi polizze assicurative, assistenza sanitaria, ordini di produzione e ordini high-tech.

![](../../images/field-groups/quote-request-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `discount` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Importo dello sconto per un preventivo visualizzato a un visitatore. |
| `premium` | [[!UICONTROL Valuta]](../../data-types/currency.md) | L&#39;importo del premio per un preventivo visualizzato a un visitatore. |
| `location` | [!UICONTROL Stringa] | Il codice postale utilizzato per trovare rivenditori vicino alla posizione del visitatore. |
| `requestID` | [!UICONTROL Stringa] | Identificatore univoco per la richiesta del preventivo. |
| `selectedRetailer` | [!UICONTROL Stringa] | Il rivenditore selezionato per la richiesta del preventivo, se applicabile. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
