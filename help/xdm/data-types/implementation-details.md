---
title: Tipo di dati dettagli di implementazione
description: Questo documento fornisce una panoramica dei dettagli di implementazione del tipo di dati Experience Data Model (XDM) .
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 6%

---

# [!UICONTROL Dettagli di implementazione] tipo di dati

[!UICONTROL Dettagli di implementazione] è un tipo di dati XDM (Experience Data Model) standard che descrive un’implementazione di tecnologia, ad esempio un’API o un SDK.

![Struttura del tipo di dati](../images/data-types/implementation-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `environment` | Stringa | L&#39;ambiente dell&#39;attuazione. |
| `name` | Stringa | Identificatore per l&#39;SDK o l&#39;endpoint. Tutti gli SDK o gli endpoint sono identificati tramite un URI, incluse le estensioni. |
| `version` | Stringa | Versione dell’API o dell’SDK. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
