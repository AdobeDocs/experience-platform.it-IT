---
title: Tipo di dati di codifica
description: Scopri il tipo di dati Coding Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 10%

---

# [!UICONTROL Codifica] tipo di dati

[!UICONTROL Coding] è un tipo di dati XDM (Experience Data Model) standard che descrive un riferimento a un codice definito da un sistema terminologico. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Codifica della struttura del tipo di dati](../../images/data-types/healthcare/coding.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Codice] | `code` | Stringa | Simbolo nella sintassi definita dal sistema. |
| [!UICONTROL Visualizzazione] | `display` | Stringa | La rappresentazione definita dal sistema. |
| [!UICONTROL Sistema] | `system` | Stringa | Lo spazio dei nomi per il valore dell’identificatore, rappresentato come URI. |
| [!UICONTROL Selezionato Dall&#39;Utente] | `userSelected` | Booleano | Indica se la codifica è stata scelta dall’utente. Il valore predefinito è false. |
| [!UICONTROL Versione] | `version` | Stringa | Versione del sistema. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.schema.json)
