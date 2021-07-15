---
solution: Experience Platform
title: Tipo di dati della stringa di consenso
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM della stringa di consenso.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 3%

---

# [!UICONTROL Tipo di dati ] stringa del consenso

[!UICONTROL Consent ] String è un tipo di dati XDM standard che descrive un valore stringa che rappresenta il consenso di un cliente. Include informazioni contestuali, come lo standard per la stringa di consenso (ad esempio, il [IAB Transparency and Consent Framework (TCF) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `consentStandard` | Stringa | Lo standard della stringa di consenso. Questo consente di determinare il formato della stringa di consenso impostato dai servizi di gestione del consenso. |
| `consentStandardVersion` | Stringa | Versione dello standard di consenso, utilizzata per definire con precisione il formato della stringa di consenso impostato dai servizi di gestione del consenso. |
| `consentStringValue` | Stringa | Stringa di consenso completa fornita dal servizio di gestione del consenso. `consentStandard` e  `consentStandardVersion` consente di definire come analizzare questa stringa. |
| `containsPersonalData` | Booleano | Quando questo campo è true, significa che questa stringa di consenso deve essere elaborata per l’applicazione del consenso. |
| `gdprApplies` | Booleano | Quando questo campo è vero significa che il consenso viene fornito con dati personali. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
