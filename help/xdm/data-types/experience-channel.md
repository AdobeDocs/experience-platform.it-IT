---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dettagli pagina web;tipo di dati;tipo di dati;tipo di dati;tipo di dati;pagina web
solution: Experience Platform
title: Tipo di dati del canale esperienza
description: Questo documento fornisce una panoramica del tipo di dati XDM (Experience Channel Experience Data Model).
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# [!UICONTROL Canale esperienza] tipo di dati

[!UICONTROL Canale esperienza] è un tipo di dati XDM (Experience Data Model) standard che descrive un canale di esperienza. Un canale di esperienza rappresenta un metodo o un percorso per il consumo delle esperienze digitali.

Esistono diversi canali di esperienza, ciascuno con vincoli diversi su come viene distribuito il contenuto, come si può osservare l’interazione con il cliente e come vengono raccolti i dati. All’interno di un canale, le esperienze possono essere distribuite in posizioni specifiche. Le posizioni e i tipi di posizioni esistenti in un canale variano da canale a canale.

![](../images/data-types/experience-channel.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_id` | Stringa | Un ID che identifica il canale in modo univoco. Ogni canale di esperienza specifico definisce una costante `@id`. |
| `_type` | Stringa | Fornisce un&#39;etichetta di classificazione approssimativa per canali con proprietà simili. |
| `contentTypes` | Matrice di stringhe | I tipi di contenuto che questo canale può fornire. |
| `locationTypes` | Matrice di stringhe | I tipi di posizioni (posizioni virtuali) in cui è composto questo canale e a cui può essere trasmesso il contenuto. |
| `mediaAction` | Stringa | Descrive un&#39;azione multimediale Experience Event, se applicabile. |
| `mediaType` | Stringa | Descrive se il tipo di supporto è pagato, posseduto o ottenuto. |
| `metricTypes` | Matrice di stringhe | Le metriche che possono essere raccolte in questo canale. |
| `mode` | Stringa | Come vengono distribuite le esperienze in questo canale. |
| `typeAtSource` | Stringa | Un nome personalizzato per il canale. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
