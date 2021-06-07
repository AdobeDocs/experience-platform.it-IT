---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo campi schema dettagli commercio
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli commercio.
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL Gruppo di campi ] di Commerce Detailsschema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL Commerce ] Details è un gruppo di campi di schema standard per la  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilizzato per descrivere dati di e-commerce come informazioni sui prodotti (SKU, nome, quantità) e operazioni carrello standard (ordine, pagamento, abbandono).

![](../../images/field-groups/commerce-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Oggetto che descrive le restituzioni dei prodotti, la registrazione della garanzia e i processi relativi al carrello o all&#39;ordine. |
| `productListItems` | Array di [voci dell&#39;elenco di prodotti](../../data-types/product-list-item.md) | Elenco di articoli che rappresentano i prodotti selezionati da un cliente, con opzioni e prezzi specifici in un determinato momento (che possono differire dal record del prodotto). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-commerce.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-commerce.schema.json)
