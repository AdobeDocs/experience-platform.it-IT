---
title: Tipo di dati di origine B2B
description: Scopri il tipo di dati Origine B2B Experience Data Model (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# [!UICONTROL Origine B2B] tipo di dati

[!UICONTROL Origine B2B] è un tipo di dati Experience Data Model (XDM) standard che rappresenta un identificatore composito per un’entità B2B (ad esempio un [account](../classes/b2b/business-account.md), un [opportunità](../classes/b2b/business-opportunity.md)o un [campagna](../classes/b2b/business-campaign.md)).

Quando ci si basa esclusivamente su identificatori basati su stringhe, possono verificarsi sovrapposizioni tra gli ID in più sistemi (ad esempio, a un’opportunità potrebbe essere assegnato un ID stringa su un sistema CRM, ma tale ID potrebbe fare riferimento a un’opportunità completamente diversa). Questo può causare conflitti di dati durante l’unione di dati in [Profilo cliente in tempo reale](../../profile/home.md).

Il [!UICONTROL Origine B2B] Il tipo di dati ti consente di utilizzare l’ID stringa originale di un’entità e di combinarlo con informazioni contestuali specifiche per l’origine per garantire che rimanga completamente univoco nel sistema Platform, indipendentemente dall’origine da cui proviene.

![Struttura di origine B2B](../images/data-types/b2b-source.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `sourceID` | Stringa | ID univoco del record di origine. |
| `sourceInstanceID` | Stringa | ID dell’istanza o organizzazione dei dati sorgente. |
| `sourceKey` | Stringa | Un identificatore univoco composto da `sourceId`, `sourceInstanceId`, e `sourceType` concatenati insieme nel seguente formato: `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Alcuni connettori di origini come Marketo concatenano automaticamente questo valore per determinati identificatori. Gli altri devono essere concatenati manualmente utilizzando [Preparazione dati `concat` funzione](../../data-prep/functions.md#string), ad esempio: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Stringa | Nome della piattaforma che fornisce i dati di origine. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
