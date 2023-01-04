---
title: Tipo di dati di origine B2B
description: Questo documento fornisce una panoramica del tipo di dati XDM (B2B Source Experience Data Model).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 4%

---

# [!UICONTROL Origine B2B] tipo di dati

[!UICONTROL Origine B2B] è un tipo di dati XDM (Experience Data Model) standard che rappresenta un identificatore composito per un’entità B2B (ad esempio un [account](../classes/b2b/business-account.md), un [opportunità](../classes/b2b/business-opportunity.md)o [campagna](../classes/b2b/business-campaign.md)).

Quando fai affidamento solo su identificatori basati su stringhe, possono esserci sovrapposizioni tra ID in più sistemi (ad esempio, è possibile assegnare a un&#39;opportunità un ID stringa in un sistema CRM, ma lo stesso ID può fare riferimento a un&#39;opportunità completamente diversa). Ciò può causare conflitti di dati durante l’unione dei dati in [Profilo cliente in tempo reale](../../profile/home.md).

La [!UICONTROL Origine B2B] il tipo di dati ti consente di utilizzare l’ID stringa originale di un’entità e di combinarla con informazioni contestuali specifiche per l’origine per garantire che rimanga completamente univoco nel sistema Platform, indipendentemente dall’origine da cui proviene.

![Struttura di origine B2B](../images/data-types/b2b-source.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `sourceID` | Stringa | Un ID univoco per il record sorgente. |
| `sourceInstanceID` | Stringa | L&#39;ID istanza o organizzazione dei dati di origine. |
| `sourceKey` | Stringa | Un identificatore univoco composto da `sourceId`, `sourceInstanceId`e `sourceType` concatenati nel seguente formato: `[sourceID]@$[sourceInstanceID].[sourceType]`.<br><br>Alcuni connettori sorgente come Marketo concatenano automaticamente questo valore per alcuni identificatori. Gli altri devono essere concatenati manualmente utilizzando la variabile [Preparazione dei dati `concat` Funzione](../../data-prep/functions.md#string)ad esempio: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Stringa | Nome della piattaforma che fornisce i dati di origine. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
