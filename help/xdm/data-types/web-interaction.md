---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;interazione web;tipo dati;tipo dati;tipo dati;
solution: Experience Platform
title: Tipo di dati dell’interazione web
description: Scopri il tipo di dati Experience Data Model (XDM) di interazione web.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 10%

---

# [!UICONTROL Interazione Web] tipo di dati

[!UICONTROL Interazione Web] è un tipo di dati XDM (Experience Data Model) standard che descrive informazioni sulle interazioni eseguite in una pagina Web dopo il completamento del caricamento della pagina iniziale. È stato progettato per registrare le interazioni in applicazioni web avanzate che non attivano il caricamento di una nuova pagina, come le app web a pagina singola (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Misura]](./measure.md) | Una misurazione che tiene traccia del clic di un collegamento web. |
| `URL` | Stringa | Il link o l’URL effettivo utilizzato per questa interazione web. |
| `name` | Stringa | Il nome normativo utilizzato per questo collegamento web. Viene utilizzato a scopo di classificazione. |
| `type` | Stringa | Il tipo di collegamento. Questa proprietà deve essere uguale a uno dei seguenti valori enum: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
