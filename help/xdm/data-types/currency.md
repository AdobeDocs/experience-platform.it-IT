---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dispositivo;tipo di dati;tipo di dati;tipo di dati;tipo di dati;valuta;
solution: Experience Platform
title: Tipo di dati della valuta
description: Questo documento fornisce una panoramica del tipo di dati XDM della valuta.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 7%

---

# [!UICONTROL Valuta] tipo di dati

[!UICONTROL Valuta] è un tipo di dati XDM standard che descrive un ammontare di valuta, inclusi il tipo di valuta e la data di conversione.

![](../images/data-types/currency.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `amount` | Doppio | L&#39;ammontare della valuta definita dalla `currencyCode`. |
| `conversionDate` | DateTime | Una marca temporale di quando è stata effettuata la conversione della valuta. |
| `currencyCode` | Stringa | Un codice ISO 4217 che indica il tipo di valuta che `amount` rappresenta. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
