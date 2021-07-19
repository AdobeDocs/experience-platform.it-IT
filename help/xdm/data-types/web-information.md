---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dettagli pagina web;tipo di dati;tipo di dati;tipo di dati;tipo di dati;pagina web
solution: Experience Platform
title: Tipo di dati di informazioni web
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Experience Data Model) per informazioni web.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 3%

---

# [!UICONTROL Tipo di dati ] per informazioni web

[!UICONTROL Le ] informazioni web sono tipi di dati XDM (Experience Data Model) standard che descrivono le informazioni registrate tramite un evento esperienza specifico per il canale Web mondiale, inclusa la pagina web, il referente e/o il collegamento relativo all’interazione sulla pagina.

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
