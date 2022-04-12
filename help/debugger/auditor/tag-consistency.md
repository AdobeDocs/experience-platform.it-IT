---
title: Riferimento per il test di coerenza dei tag
description: Scopri come la funzione di revisione verifica la coerenza dei tag in Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 44%

---

# Riferimento test di coerenza tag

Questo riferimento fornisce ulteriori informazioni sulla funzione di auditor nei test di Adobe Experience Platform Debugger per la coerenza dei tag.

>[!NOTE]
>
>Per ulteriori informazioni sui test di auditor in Platform Debugger, consulta la sezione [panoramica delle funzioni di auditor](./overview.md).

I test di coerenza dei tag rilevano incoerenze tra tutte le pagine digitalizzate. Si tratta di valori o configurazioni che devono essere identici in tutte le pagine del sito per garantire una raccolta accurata dei dati.

| Test | Peso | Criteri | Consiglio |
| --- | --- | --- | --- |
| Adobe Analytics - Versione codice coerente | 5 | È stata trovata più di una versione del codice Analytics. | Sostituisci tutte le istanze di Analytics con la versione corrente.<br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it) |

{style=&quot;table-layout:auto&quot;}
