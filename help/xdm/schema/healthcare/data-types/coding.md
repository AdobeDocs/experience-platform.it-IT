---
title: Tipo di dati di codifica
description: Scopri il tipo di dati Coding Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 23b789da-1feb-4001-8268-f0d7e2e8563b
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 10%

---

# [!UICONTROL Codifica] tipo di dati

[!UICONTROL Coding] è un tipo di dati XDM (Experience Data Model) standard che descrive un riferimento a un codice definito da un sistema terminologico. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Codifica della struttura del tipo di dati](../../../images/healthcare/data-types/coding.png)

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
