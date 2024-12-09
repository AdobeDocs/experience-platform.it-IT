---
title: Tipo di dati per l’annotazione
description: Scopri il tipo di dati Annotation Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---

# Tipo di dati [!UICONTROL Annotation]

[!UICONTROL Annotation] è un tipo di dati Experience Data Model (XDM) standard che contiene un nodo di testo con attribuzione all&#39;autore. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati dell&#39;annotazione](../../images/data-types/healthcare/annotation.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Riferimento autore] | `authorReference` | [[!UICONTROL Riferimento]](../healthcare/reference.md) | Riferimento all&#39;autore. |
| [!UICONTROL Autore] | `authorString` | Stringa | Persona responsabile dell’annotazione. |
| [!UICONTROL Testo] | `text` | Stringa | Il contenuto dell’annotazione. |
| [!UICONTROL Tempo] | `time` | Data e ora | Quando è stata effettuata l’annotazione. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
