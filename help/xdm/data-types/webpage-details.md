---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dettagli pagina web;tipo dati;tipo dati;tipo dati;pagina web;home;popular topic;schema;Schema;XDM;fields;schemas;Schemas;Webpage details;datatype;data-type;data type;data type;webpage
solution: Experience Platform
title: Tipo di dati Dettagli pagina web
description: Scopri i dettagli della pagina web Tipo di dati Experience Data Model (XDM).
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 11%

---

# [!UICONTROL Dettagli pagina Web] tipo di dati

[!UICONTROL Dettagli pagina Web] è un tipo di dati Experience Data Model (XDM) standard che descrive i dettagli di una pagina Web appena caricata e visualizzata, come registrato da un ExperienceEvent.

Il tipo di dati è destinato ai dettagli dell’intera pagina e al caricamento della pagina iniziale delle applicazioni web a pagina singola (SPA). Per le interazioni che si verificano in una pagina caricata e che non attivano il caricamento di una nuova pagina, vedi il tipo di dati [interazione web](./web-interaction.md).

![dettagli pagina Web](../images/data-types/web-page-details.PNG){width="500"}

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Misura]](./measure.md) | Il numero di visualizzazioni in una pagina web. |
| `URL` | Stringa | L’URL normativo o abituale della pagina web. Questo potrebbe essere o meno l’URL effettivo utilizzato per raggiungere la pagina. Per registrare l&#39;URL utilizzato per raggiungere la pagina, utilizzare `webLink`. Il formato URI deve seguire lo standard [RFC 3986](https://tools.ietf.org/html/rfc3986). |
| `isErrorPage` | Booleano | Questa proprietà utilizza un flag per indicare se la pagina è una pagina di errore o meno. Questo flag viene utilizzato per categorizzare in maniera generale le interazioni web. L’errore è definito dall’applicazione e può corrispondere a una pagina fornita con un codice di errore HTTP. |
| `isHomePage` | Booleano | Questa proprietà utilizza un flag per indicare se la pagina è una home page o meno. Questo flag viene utilizzato per categorizzare in maniera generale le interazioni web. La definizione della home page è determinata dall&#39;applicazione. |
| `name` | Stringa | Il nome normativo della pagina web. Questo nome non è necessariamente il titolo della pagina né è direttamente associato al contenuto della pagina, ma viene utilizzato per organizzare le pagine di un sito ai fini di classificazione. |
| `server` | Stringa | Il server normativo o abituale che ospita la pagina web. Questo potrebbe essere o meno l’host o il server che ha effettivamente fornito l’interazione con la pagina. |
| `siteSection` | Stringa | Il nome normativo della sezione del sito in cui risiede questa pagina web. Questa può essere utilizzata per classificare o categorizzare l’interazione. |
| `viewName` | Stringa | Nome della visualizzazione, all’interno di una pagina. Questa proprietà viene in genere utilizzata con le applicazioni a pagina singola o con le pagine contenenti schede o controlli che modificano la maggior parte del layout della pagina. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
