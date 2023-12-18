---
title: Tipo di dati Dettagli implementazione
description: Scopri i dettagli dell’implementazione per il tipo di dati Experience Data Model (XDM).
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 6%

---

# [!UICONTROL Dettagli di implementazione] tipo di dati

[!UICONTROL Dettagli di implementazione] è un tipo di dati Experience Data Model (XDM) standard che descrive un’implementazione di tecnologia, ad esempio un’API o un SDK.

![Struttura del tipo di dati](../images/data-types/implementation-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `environment` | Stringa | L’ambiente dell’implementazione. |
| `name` | Stringa | Identificatore dell’SDK o dell’endpoint. Tutti gli SDK o endpoint sono identificati tramite un URI, incluse le estensioni. |
| `version` | Stringa | Versione dell’API o dell’SDK. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
