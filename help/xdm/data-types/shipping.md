---
title: Tipo di dati di spedizione
description: Scopri il tipo di dati Shipping Experience Data Model (XDM).
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 18%

---

# Tipo di dati [!UICONTROL Spedizione]

[!UICONTROL Spedizione] è un tipo di dati XDM (Experience Data Model) standard che fornisce dettagli relativi alla spedizione di uno o più prodotti. Include dettagli sulla logistica e specifiche relative alla consegna degli articoli ordinati.


![Diagramma del tipo di dati [!UICONTROL Spedizione].](../images/data-types/shipping.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Metodo di spedizione] | `shippingMethod` | stringa | Il metodo di spedizione scelto dal cliente. |
| [!UICONTROL Importo spedizione] | `shippingAmount` | numero | L’importo che il cliente ha dovuto pagare per la spedizione. |
| [!UICONTROL Codice valuta] | `currencyCode` | stringa | Il codice di valuta alfabetico ISO 4217 utilizzato per la determinazione del prezzo del prodotto. |
| [!UICONTROL Destinazione spedizione] | `shippingDestination` | stringa | Destinazione di spedizione specificata dall&#39;utente (ad esempio, home, store e così via). |
| [!UICONTROL Data spedizione] | `shipDate` | stringa | Data di spedizione di uno o più articoli di un ordine. |
| [!UICONTROL Indirizzo di spedizione] | `address` | [[!UICONTROL indirizzo]](./address.md) | Indirizzo di spedizione. |
| [!UICONTROL Numero di tracciamento] | `trackingNumber` | numero | Il numero di registrazione fornito dal vettore di spedizione. |
| [!UICONTROL URL di tracciamento] | `trackingURL` | stringa | URL per tenere traccia dello stato di spedizione di un articolo dell&#39;ordine. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
