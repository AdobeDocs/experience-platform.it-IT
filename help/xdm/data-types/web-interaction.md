---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;interazione web;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati di interazione web
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Experience Data Model) per l’interazione web.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: e31f92146deade8132965667e7d09e01f627be7a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 4%

---

# [!UICONTROL Tipo ] di dati interazionali web

[!UICONTROL L’] interazione web è un tipo di dati XDM (Experience Data Model) standard che descrive informazioni sulle interazioni che si sono verificate in una pagina web al termine del caricamento della pagina iniziale. È destinato a registrare le interazioni in applicazioni web avanzate che non attivano un nuovo caricamento di pagina, come le app web a pagina singola (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Misura]](./measure.md) | Misurazione che tiene traccia del clic su un collegamento web. |
| `URL` | Stringa | Il collegamento o l’URL effettivo utilizzato per questa interazione web. |
| `name` | Stringa | Nome normativo utilizzato per il collegamento web. Viene utilizzato a scopo di classificazione. |
| `type` | Stringa | Tipo di collegamento. Questa proprietà deve essere uguale a uno dei seguenti valori enum: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)
