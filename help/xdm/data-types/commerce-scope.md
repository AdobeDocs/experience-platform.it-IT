---
title: Tipo di dati ambito Commerce
description: Scopri il tipo di dati Commerce Scope Experience Data Model (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 6%

---

# [!UICONTROL Ambito Commerce] tipo di dati

[!UICONTROL Ambito Commerce] è un tipo di dati Experience Data Model (XDM) standard che definisce gli identificatori per i casi in cui si è verificato un evento all’interno di un ecosistema commerciale. Distingue ambienti, siti web, store e visualizzazioni dello store.

![Diagramma del tipo di dati Ambito Commerce.](../images/data-types/commerce-scope.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID ambiente] | `environmentID` | string | ID ambiente. Un ID alfanumerico di 32 cifre. |
| [!UICONTROL Codice sito Web] | `websiteCode` | string | Il codice univoco del sito web all’interno di un ambiente. |
| [!UICONTROL Codice store] | `storeCode` | string | Il codice univoco del negozio all’interno di un sito web. |
| [!UICONTROL Codice visualizzazione store] | `storeViewCode` | string | Il codice univoco di visualizzazione del negozio all’interno di un negozio. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
