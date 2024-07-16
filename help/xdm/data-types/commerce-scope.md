---
title: Tipo di dati ambito Commerce
description: Scopri il tipo di dati Commerce Scope Experience Data Model (XDM).
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# Tipo di dati [!UICONTROL Ambito Commerce]

[!UICONTROL Ambito Commerce] è un tipo di dati XDM (Experience Data Model) standard che definisce gli identificatori per la posizione in cui si è verificato un evento all&#39;interno di un ecosistema commerciale. Distingue ambienti, siti web, store e visualizzazioni dello store.

![Diagramma del tipo di dati Ambito di Commerce.](../images/data-types/commerce-scope.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID ambiente] | `environmentID` | stringa | ID ambiente. Un ID alfanumerico di 32 cifre. |
| [!UICONTROL Codice sito Web] | `websiteCode` | stringa | Il codice univoco del sito web all’interno di un ambiente. |
| [!UICONTROL Codice archivio] | `storeCode` | stringa | Il codice univoco del negozio all’interno di un sito web. |
| [!UICONTROL Codice visualizzazione store] | `storeViewCode` | stringa | Il codice univoco di visualizzazione del negozio all’interno di un negozio. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
