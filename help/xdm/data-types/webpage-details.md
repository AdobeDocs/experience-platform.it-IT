---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dettagli pagina web;tipo di dati;tipo di dati;tipo di dati;tipo di dati;pagina web
solution: Experience Platform
title: Tipo di dati dettagli pagina web
description: Questo documento fornisce una panoramica del tipo di dati Experience Data Model (XDM) per i dettagli della pagina web.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 4%

---

# [!UICONTROL Dettagli della pagina web] tipo di dati

[!UICONTROL Dettagli della pagina web] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli di una pagina web che è stata appena caricata e visualizzata, come registrata da un ExperienceEvent.

Il tipo di dati è destinato ai dettagli di pagina completa e al caricamento iniziale di pagine di applicazioni web a pagina singola (SPA). Per le interazioni che si verificano su una pagina caricata e che non attivano un nuovo caricamento di pagina, vedi [interazione web](./web-interaction.md) tipo di dati.

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Misura]](./measure.md) | Il numero di visualizzazioni in una pagina web. |
| `URL` | Stringa | URL normativo o normale della pagina web. Questo potrebbe essere o meno l’URL effettivo utilizzato per raggiungere la pagina. Per registrare l’URL utilizzato per raggiungere la pagina utilizza `webLink`. Il formato URI deve seguire la [RFC 3986](https://tools.ietf.org/html/rfc3986) standard. |
| `isErrorPage` | Booleano | Questa proprietà utilizza un flag per indicare se la pagina è una pagina di errore o meno. Questo flag viene utilizzato per classificare in ampia misura le interazioni web. L&#39;errore è definito dall&#39;applicazione e può corrispondere a una pagina fornita con un codice di errore HTTP. |
| `isHomePage` | Booleano | Questa proprietà utilizza un flag per indicare se la pagina è una home page o meno. Questo flag viene utilizzato per classificare in ampia misura le interazioni web. La definizione della home page è determinata dall&#39;applicazione. |
| `name` | Stringa | Nome normativo della pagina web. Questo nome non è necessariamente il titolo della pagina o è direttamente associato al contenuto della pagina, ma viene utilizzato per organizzare le pagine di un sito a scopo di classificazione. |
| `server` | Stringa | Server normativo o normale che ospita la pagina web. Questo potrebbe essere o meno l&#39;host o il server che ha effettivamente servito l&#39;interazione della pagina. |
| `siteSection` | Stringa | Nome normativo della sezione del sito in cui si trova la pagina Web. Può essere utilizzato per classificare o classificare l’interazione. |
| `viewName` | Stringa | Nome della visualizzazione, all’interno di una pagina. Questa proprietà viene comunemente utilizzata nelle applicazioni a pagina singola o nelle pagine con schede o controlli che modificano la maggior parte del layout di pagina. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
