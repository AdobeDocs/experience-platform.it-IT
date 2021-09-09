---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dispositivo;tipo di dati;tipo di dati;tipo di dati;tipo di dati;valuta;
solution: Experience Platform
title: Tipo di dati della valuta
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM della valuta.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 5e92b288bb8c996cfcf343d8ac1ab1665b0d3ad0
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

#  Tipo di dati valuta

 La valuta è un tipo di dati XDM standard che descrive un importo in valuta, inclusi il tipo di valuta e la data di conversione.

![](../images/data-types/currency.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `amount` | Doppio | L&#39;ammontare della valuta definito da `currencyCode`. |
| `conversionDate` | DateTime | Una marca temporale di quando è stata effettuata la conversione della valuta. |
| `currencyCode` | Stringa | Un codice ISO 4217 che indica il tipo di valuta che `amount` rappresenta. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
