---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;Dettagli pagina Web;tipo di dati;tipo di dati;tipo di dati;pagina Web'
solution: Experience Platform
title: Tipo dati dettagli pagina Web
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Experience Data Model) per i dettagli della pagina Web.
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 2%

---


# [!UICONTROL Web page details] tipo di dati

[!UICONTROL Web page details] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli relativi a una pagina Web che è stata appena caricata e visualizzata, come registrato da un ExperienceEvent.

Il tipo di dati è destinato ai dettagli a pagina intera e ai carichi iniziali di pagine di applicazioni Web a pagina singola (SPA). Per le interazioni che si verificano su una pagina caricata e che non attivano un nuovo caricamento di pagina, vedere il tipo di dati [interazione Web](./web-interactions.md).

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Measure]](./measure.md) | Il numero di visualizzazioni in una pagina Web. |
| `URL` | Stringa | L’URL normativo o consueto della pagina Web. Può trattarsi dell’URL effettivo utilizzato per raggiungere la pagina. Per registrare l&#39;URL utilizzato per raggiungere la pagina, utilizzare `webLink`. Il formato URI deve seguire lo standard [RFC 3986](https://tools.ietf.org/html/rfc3986). |
| `isErrorPage` | Booleano | Questa proprietà utilizza un flag per indicare se la pagina è o meno una pagina di errore. Questo flag viene utilizzato per classificare in senso ampio le interazioni Web. L&#39;errore è definito dall&#39;applicazione e può corrispondere a una pagina gestita con un codice di errore HTTP. |
| `isHomePage` | Booleano | Questa proprietà utilizza un flag per indicare se la pagina è o meno una home page. Questo flag viene utilizzato per classificare in senso ampio le interazioni Web. La definizione della home page è determinata dall&#39;applicazione. |
| `name` | Stringa | Nome normativo della pagina Web. Questo nome non è necessariamente il titolo della pagina o è direttamente associato al contenuto della pagina, ma è utilizzato per organizzare le pagine di un sito a fini di classificazione. |
| `server` | Stringa | Server normativo o normale che ospita la pagina Web. Può trattarsi dell&#39;host o del server che ha effettivamente servito l&#39;interazione della pagina. |
| `siteSection` | Stringa | Nome normativo della sezione del sito in cui risiede la pagina Web. Può essere utilizzato per classificare o classificare l&#39;interazione. |
| `viewName` | Stringa | Nome della visualizzazione, all’interno di una pagina. Questa proprietà è comunemente utilizzata con applicazioni a pagina singola o pagine con schede o controlli che modificano la maggior parte del layout di pagina. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.example.2.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.schema.json)