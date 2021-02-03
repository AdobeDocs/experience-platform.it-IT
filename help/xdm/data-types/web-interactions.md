---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;interazione Web;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo dati interazione Web
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Experience Data Model) di interazione Web.
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 2%

---


# [!UICONTROL Web interaction] tipo di dati

[!UICONTROL Web interaction] è un tipo di dati XDM (Experience Data Model) standard che descrive le informazioni sulle interazioni che si sono verificate in una pagina Web dopo il completamento del caricamento iniziale della pagina. È destinato alla registrazione di interazioni in applicazioni Web avanzate che non attivano un nuovo caricamento di pagina, come le app Web a pagina singola (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Measure]](./measure.md) | Misura che monitora il clic di un collegamento Web. |
| `URL` | Stringa | Il collegamento o l&#39;URL effettivo utilizzato per questa interazione Web. |
| `name` | Stringa | Nome normativo utilizzato per il collegamento Web. Questa opzione è utilizzata per scopi di classificazione. |
| `type` | Stringa | Tipo di collegamento. Questa proprietà deve essere uguale a uno dei seguenti valori enum: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)