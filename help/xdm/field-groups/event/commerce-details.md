---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo campi schema dettagli commercio
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli commercio.
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 4%

---

# [!UICONTROL Dettagli Commerce] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Visualizza il documento in [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli Commerce] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md), utilizzato per descrivere i dati di e-commerce, ad esempio informazioni sui prodotti (SKU, nome, quantità) e operazioni standard sul carrello (ordine, pagamento, abbandono).

![](../../images/field-groups/commerce-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Oggetto che descrive le restituzioni dei prodotti, la registrazione della garanzia e i processi relativi al carrello o all&#39;ordine. |
| `productListItems` | Array di [Voci elenco prodotti](../../data-types/product-list-item.md) | Elenco di articoli che rappresentano i prodotti selezionati da un cliente, con opzioni e prezzi specifici in un determinato momento (che possono differire dal record del prodotto). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
