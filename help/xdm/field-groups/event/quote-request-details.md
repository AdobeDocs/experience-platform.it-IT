---
title: Gruppo di campi schema dettagli richiesta preventivo
description: Questo documento fornisce una panoramica del gruppo di campi schema Dettagli richiesta preventivo.
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 6%

---

# [!UICONTROL Dettagli richiesta preventivo] gruppo di campi schema

[!UICONTROL Dettagli richiesta preventivo] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo `quotes` object to a schema, che acquisisce i dettagli del processo di richiesta per vari tipi di preventivi, tra cui polizze assicurative, assistenza sanitaria, ordini di produzione e ordini high-tech.

![](../../images/field-groups/quote-request-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `discount` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Importo dello sconto per un preventivo visualizzato a un visitatore. |
| `premium` | [[!UICONTROL Valuta]](../../data-types/currency.md) | L’importo del premio per un preventivo mostrato a un visitatore. |
| `location` | [!UICONTROL Stringa] | Il codice postale utilizzato per trovare i rivenditori vicino alla posizione del visitatore. |
| `requestID` | [!UICONTROL Stringa] | Identificatore univoco della richiesta di preventivo. |
| `selectedRetailer` | [!UICONTROL Stringa] | Il rivenditore selezionato per la richiesta di preventivo, se applicabile. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
