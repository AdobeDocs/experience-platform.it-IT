---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;ricerca;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati di ricerca
description: Questo documento fornisce una panoramica del tipo di dati XDM (Search Experience Data Model).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 7%

---

# [!UICONTROL Ricerca] tipo di dati

[!UICONTROL Ricerca] è un tipo di dati XDM (Experience Data Model) standard che contiene informazioni sull’attività di ricerca web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `isPaid` | Booleano | Utilizzato per indicare se la ricerca è pagata o meno. |
| `keywords` | Stringa | Le parole chiave per la ricerca. |
| `pageDepth` | Intero | Profondità della pagina nei risultati della ricerca. |
| `position` | Intero | Posizione o classificazione dell’elenco nella pagina dei risultati della ricerca. |
| `searchEngine` | Stringa | Il motore di ricerca utilizzato dalla ricerca. |
| `searchEngineID` | Stringa | Identificatore specifico dell&#39;applicazione utilizzato per identificare il motore di ricerca. |
| `slot` | Stringa | La sezione denominata della pagina in cui è stato visualizzato il risultato della ricerca. Il valore di questa proprietà deve essere uguale a uno dei valori enum noti definiti, ad esempio `top`, `side`oppure `bottom`. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
