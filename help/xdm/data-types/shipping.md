---
title: Tipo di dati di spedizione
description: Scopri il tipo di dati Shipping Experience Data Model (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 6%

---

# [!UICONTROL Spedizione] tipo di dati

[!UICONTROL Spedizione] è un tipo di dati Experience Data Model (XDM) standard che fornisce dettagli relativi alla spedizione di uno o più prodotti. Include dettagli sulla logistica e specifiche relative alla consegna degli articoli ordinati.


![Un diagramma del [!UICONTROL Spedizione] tipo di dati.](../images/data-types/shipping.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Metodo di spedizione] | `shippingMethod` | string | Il metodo di spedizione scelto dal cliente. |
| [!UICONTROL Importo spedizione] | `shippingAmount` | number | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |
| [!UICONTROL Codice valuta] | `currencyCode` | string | Il codice valuta alfabetico ISO 4217 utilizzato per la determinazione del prezzo del prodotto. |
| [!UICONTROL Destinazione spedizione] | `shippingDestination` | string | Destinazione di spedizione specificata dall&#39;utente (ad esempio, home, store e così via). |
| [!UICONTROL Data di spedizione] | `shipDate` | string | Data di spedizione di uno o più articoli di un ordine. |
| [!UICONTROL Indirizzo di spedizione] | `address` | [[!UICONTROL indirizzo]](./address.md) | Indirizzo di spedizione. |
| [!UICONTROL Numero di tracciamento] | `trackingNumber` | number | Il numero di registrazione fornito dal vettore di spedizione. |
| [!UICONTROL URL di tracciamento] | `trackingURL` | string | URL per tenere traccia dello stato di spedizione di un articolo dell&#39;ordine. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
