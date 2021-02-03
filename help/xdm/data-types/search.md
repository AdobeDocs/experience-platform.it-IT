---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;ricerca;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo dati di ricerca
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Search Experience Data Model).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 4%

---


# [!UICONTROL Search] tipo di dati

[!UICONTROL Search] è un tipo di dati XDM (Experience Data Model) standard che contiene informazioni sull&#39;attività di ricerca Web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `isPaid` | Booleano | Utilizzato per indicare se la ricerca è pagata o meno. |
| `keywords` | Stringa | Le parole chiave per la ricerca. |
| `pageDepth` | Intero | Profondità della pagina nei risultati della ricerca. |
| `position` | Intero | Posizione o livello dell&#39;elenco nella pagina dei risultati della ricerca. |
| `searchEngine` | Stringa | Il motore di ricerca utilizzato dalla ricerca. |
| `searchEngineID` | Stringa | Identificatore specifico dell&#39;applicazione utilizzato per identificare il motore di ricerca. |
| `slot` | Stringa | La sezione denominata della pagina in cui è stato visualizzato il risultato della ricerca. Il valore di questa proprietà deve essere uguale a uno dei valori enum noti definiti, ad esempio `top`, `side` o `bottom`. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)