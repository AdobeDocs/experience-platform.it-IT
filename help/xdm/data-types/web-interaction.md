---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;interazione web;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati di interazione web
description: Questo documento fornisce una panoramica del tipo di dati XDM (Experience Data Model) per l’interazione web.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 5%

---

# [!UICONTROL Interazione web] tipo di dati

[!UICONTROL Interazione web] è un tipo di dati XDM (Experience Data Model) standard che descrive informazioni sulle interazioni che si sono verificate in una pagina web al termine del caricamento della pagina iniziale. È destinato a registrare le interazioni in applicazioni web avanzate che non attivano un nuovo caricamento di pagina, come le app web a pagina singola (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Misura]](./measure.md) | Misurazione che tiene traccia del clic su un collegamento web. |
| `URL` | Stringa | Il collegamento o l’URL effettivo utilizzato per questa interazione web. |
| `name` | Stringa | Nome normativo utilizzato per il collegamento web. Viene utilizzato a scopo di classificazione. |
| `type` | Stringa | Tipo di collegamento. Questa proprietà deve essere uguale a uno dei seguenti valori enum: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
