---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;ricerca;tipo di dati;tipo di dati;tipo di dati;home;popular topic;schema;Schema;XDM;fields;schemas;Schemas;search;datatype;data-type;data type;
solution: Experience Platform
title: Cerca tipo di dati
description: Questo documento fornisce una panoramica del tipo di dati XDM (Search Experience Data Model).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 6%

---

# [!UICONTROL Ricerca] tipo di dati

[!UICONTROL Ricerca] è un tipo di dati Experience Data Model (XDM) standard che contiene informazioni sull’attività di ricerca web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `isPaid` | Booleano | Utilizzato per indicare se la ricerca è a pagamento o no. |
| `keywords` | Stringa | Parole chiave per la ricerca. |
| `pageDepth` | Intero | Profondità della pagina nei risultati di ricerca. |
| `position` | Intero | Posizione o classificazione dell&#39;elenco nella pagina dei risultati della ricerca. |
| `searchEngine` | Stringa | Il motore di ricerca utilizzato dalla ricerca. |
| `searchEngineID` | Stringa | Identificatore specifico dell’applicazione utilizzato per identificare il motore di ricerca. |
| `slot` | Stringa | La sezione denominata della pagina in cui è apparso il risultato della ricerca. Il valore di questa proprietà deve essere uguale a uno dei valori enum noti definiti, ad esempio `top`, `side`, o `bottom`. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
