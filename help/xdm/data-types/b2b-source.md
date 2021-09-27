---
title: Tipo di dati di origine B2B
description: Questo documento fornisce una panoramica del tipo di dati XDM (B2B Source Experience Data Model).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 3%

---

# [!UICONTROL Tipo ] di dati base B2B

>[!NOTE]
>
>Questo tipo di dati è disponibile solo per le organizzazioni che hanno accesso all’edizione B2B di Real-time Customer Data Platform.

[!UICONTROL B2B ] Sourceè un tipo di dati XDM (Experience Data Model) standard che rappresenta un identificatore composito per un’entità B2B (ad esempio un  [account](../classes/b2b/business-account.md), un’ [opportunità](../classes/b2b/business-opportunity.md) o una  [campagna](../classes/b2b/business-campaign.md)).

Quando fai affidamento solo su identificatori basati su stringhe, possono esserci sovrapposizioni tra ID in più sistemi (ad esempio, è possibile assegnare a un&#39;opportunità un ID stringa in un sistema CRM, ma lo stesso ID può fare riferimento a un&#39;opportunità completamente diversa). Questo può causare conflitti di dati durante l&#39;unione dei dati in [Profilo cliente in tempo reale](../../profile/home.md).

Il tipo di dati [!UICONTROL B2B Source] ti consente di utilizzare l’ID stringa originale di un’entità e di combinarla con informazioni contestuali specifiche per l’origine per garantire che rimanga completamente univoco nel sistema Platform, indipendentemente dall’origine da cui è stata generata.

![Struttura di origine B2B](../images/data-types/b2b-source.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `sourceID` | Stringa | Un ID univoco per il record sorgente. |
| `sourceInstanceID` | Stringa | L&#39;ID istanza o organizzazione dei dati di origine. |
| `sourceKey` | Stringa | Un identificatore univoco composto da `sourceId`, `sourceInstanceId` e `sourceType` concatenati nel seguente formato: `[sourceID]@$[sourceInstanceID].[sourceType]`.<br><br>Alcuni connettori sorgente come Marketo concatenano automaticamente questo valore per alcuni identificatori. Altri devono essere concatenati manualmente utilizzando la funzione [Preparazione dati `concat`](../../data-prep/functions.md#string), ad esempio: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Stringa | Nome della piattaforma che fornisce i dati di origine. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
