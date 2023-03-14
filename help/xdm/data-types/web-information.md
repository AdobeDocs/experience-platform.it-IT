---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dettagli pagina web;tipo dati;tipo dati;tipo dati;pagina web;home;popular topic;schema;Schema;XDM;fields;schemas;Schemas;Webpage details;datatype;data-type;data type;data type;webpage
solution: Experience Platform
title: Tipo di dati informazioni web
description: Questo documento fornisce una panoramica del tipo di dati Experience Data Model (XDM) delle informazioni web.
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# [!UICONTROL Informazioni web] tipo di dati

[!UICONTROL Informazioni web] è un tipo di dati Experience Data Model (XDM) standard che descrive le informazioni registrate tramite un evento esperienza specifico per il canale World Wide Web, inclusi la pagina web, il referrer e/o il collegamento relativo all’interazione su pagina.

![](../images/data-types/web-information.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Interazione web]](./web-interaction.md) | Descrive i dettagli del collegamento web o dell’URL che corrisponde all’interazione. |
| `webPageDetails` | [[!UICONTROL Dettagli pagina web]](./webpage-details.md) | Descrive i dettagli della pagina web in cui si è verificata l’interazione web. |
| `webReferrer` | [!UICONTROL Oggetto] | Descrive il referente di un’interazione web, che è l’URL da cui un visitatore proviene immediatamente prima che l’interazione web corrente sia stata registrata. Contiene le seguenti sottoproprietà: <ul><li>`URL`: URL del referente.</li><li>`type`: tipo di referente.</li></ul> |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
