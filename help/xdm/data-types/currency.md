---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dispositivo;tipo di dati;tipo di dati;tipo di dati;valuta;
solution: Experience Platform
title: Tipo di dati valuta
description: Scopri il tipo di dati XDM Valuta.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 6%

---

# Tipo di dati [!UICONTROL Valuta]

[!UICONTROL Valuta] è un tipo di dati XDM standard che descrive un importo di valuta, inclusi il tipo di valuta e la data di conversione.

![](../images/data-types/currency.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `amount` | Doppio | Quantità di valuta definita da `currencyCode`. |
| `conversionDate` | Data e ora | Timestamp di quando è stata effettuata la conversione della valuta. |
| `currencyCode` | Stringa | Codice ISO 4217 che indica il tipo di valuta rappresentato da `amount`. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
