---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;
solution: Experience Platform
title: Gruppo di campi dello schema dei dettagli Commerce
description: Scopri il gruppo di campi dello schema Commerce Details.
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# [!UICONTROL Dettagli Commerce] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Vedi il documento su [aggiornamenti nome gruppo di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli Commerce] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilizzato per descrivere dati commerciali quali informazioni sul prodotto (SKU, nome, quantità) e operazioni standard del carrello (ordine, pagamento, abbandono).

![](../../images/field-groups/commerce-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Oggetto che descrive le restituzioni dei prodotti, la registrazione della garanzia e i processi relativi a carrello acquisti e ordini. |
| `productListItems` | Array di [Elementi dell’elenco prodotti](../../data-types/product-list-item.md) | Un elenco di articoli che rappresentano i prodotti selezionati da un cliente, con opzioni e prezzi specifici in un momento specifico (che possono differire dal record del prodotto). |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
