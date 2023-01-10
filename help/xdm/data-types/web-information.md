---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dettagli pagina web;tipo di dati;tipo di dati;tipo di dati;tipo di dati;pagina web
solution: Experience Platform
title: Tipo di dati di informazioni web
description: Questo documento fornisce una panoramica del tipo di dati XDM (Experience Data Model) per informazioni web.
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 4%

---

# [!UICONTROL Informazioni web] tipo di dati

[!UICONTROL Informazioni web] è un tipo di dati standard Experience Data Model (XDM) che descrive le informazioni registrate tramite un evento Experience che è specifico per il canale World Wide Web, inclusa la pagina web, il referente e/o il collegamento relativo all’interazione on-page.

![](../images/data-types/web-information.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Interazione web]](./web-interaction.md) | Descrive i dettagli del collegamento web o dell’URL che corrispondono all’interazione. |
| `webPageDetails` | [[!UICONTROL Dettagli della pagina web]](./webpage-details.md) | Descrive i dettagli della pagina web in cui si è verificata l’interazione web. |
| `webReferrer` | [!UICONTROL Oggetto] | Descrive il referente di un&#39;interazione web, che è l&#39;URL di provenienza di un visitatore immediatamente prima della registrazione dell&#39;interazione web corrente. Contiene le seguenti sottoproprietà: <ul><li>`URL`: URL del referente.</li><li>`type`: Tipo di referrer.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
