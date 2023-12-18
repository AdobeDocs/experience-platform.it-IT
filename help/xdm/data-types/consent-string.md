---
solution: Experience Platform
title: Tipo di dati della stringa di consenso
description: Scopri il tipo di dati XDM per la stringa di consenso.
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 5%

---

# [!UICONTROL Stringa di consenso] tipo di dati

[!UICONTROL Stringa di consenso] è un tipo di dati XDM standard che descrive un valore stringa che rappresenta il consenso di un cliente. Include informazioni contestuali come lo standard per la stringa di consenso (ad esempio, [IAB Transparency and Consent Framework (TCF) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `consentStandard` | Stringa | Lo standard per la stringa di consenso. Questo aiuta a determinare il formato della stringa di consenso come impostato dai servizi di gestione del consenso. |
| `consentStandardVersion` | Stringa | La versione dello standard di consenso, utilizzata per definire accuratamente il formato della stringa di consenso come impostato dai servizi di gestione del consenso. |
| `consentStringValue` | Stringa | Stringa di consenso completa fornita dal servizio di gestione del consenso. `consentStandard` e `consentStandardVersion` per definire la modalità di analisi di questa stringa. |
| `containsPersonalData` | Booleano | Quando questo campo è true, significa che questa stringa di consenso deve essere elaborata per l’applicazione del consenso. |
| `gdprApplies` | Booleano | Quando questo campo è true, significa che il consenso include dati personali. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
