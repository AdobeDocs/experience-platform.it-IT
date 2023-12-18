---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dettagli pagina web;tipo dati;tipo dati;tipo dati;pagina web;home;popular topic;schema;Schema;XDM;fields;schemas;Schemas;Webpage details;datatype;data-type;data type;data type;webpage
solution: Experience Platform
title: Tipo di dati del canale esperienza
description: Scopri il tipo di dati Experience Channel Experience Data Model (XDM).
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---

# [!UICONTROL Canale esperienza] tipo di dati

[!UICONTROL Canale esperienza] è un tipo di dati Experience Data Model (XDM) standard che descrive un canale di esperienza. Un canale di esperienza rappresenta un metodo o un percorso per il modo in cui vengono utilizzate le esperienze digitali.

Esistono più canali di esperienza, ciascuno con vincoli diversi relativi al modo in cui vengono forniti i contenuti, al modo in cui è possibile osservare l’interazione del cliente e alla modalità di raccolta dei dati. All’interno di un canale, le esperienze possono essere distribuite a posizioni specifiche. Le posizioni e i tipi di posizioni esistenti in un canale differiscono da canale a canale.

![](../images/data-types/experience-channel.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_id` | Stringa | Un ID che identifica in modo univoco il canale. Ogni canale di esperienza specifico definisce una costante `@id`. |
| `_type` | Stringa | Fornisce un’etichetta di classificazione approssimativa per i canali con proprietà simili. |
| `contentTypes` | Array di stringhe | I tipi di contenuto che questo canale può fornire. |
| `locationTypes` | Array di stringhe | I tipi di posizioni (luoghi virtuali) da cui questo canale è costituito e a cui può fornire contenuti. |
| `mediaAction` | Stringa | Descrive un’azione multimediale Experience Event, se applicabile. |
| `mediaType` | Stringa | Descrive se il tipo di file multimediale è pagato, di proprietà o guadagnato. |
| `metricTypes` | Array di stringhe | Le metriche che possono essere raccolte in questo canale. |
| `mode` | Stringa | Modalità di distribuzione delle esperienze in questo canale. |
| `typeAtSource` | Stringa | Un nome personalizzato per il canale. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
