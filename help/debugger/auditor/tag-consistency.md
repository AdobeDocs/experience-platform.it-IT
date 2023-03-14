---
title: Riferimento test di coerenza tag
description: Scopri come la funzione di auditor verifica la coerenza dei tag in Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 43%

---

# Riferimento per la prova di coerenza dei tag

Questa documentazione fornisce ulteriori informazioni sulla funzionalità di auditor nei test di Adobe Experience Platform Debugger per verificare la coerenza dei tag.

>[!NOTE]
>
>Per ulteriori informazioni sui test dell’auditor in Platform Debugger, consulta [panoramica della funzione di auditor](./overview.md).

I test di coerenza dei tag rilevano incoerenze tra tutte le pagine digitalizzate. Si tratta di valori o configurazioni che devono essere identici in tutte le pagine del sito per garantire una raccolta accurata dei dati.

| Test | Peso | Criteri | Consiglio |
| --- | --- | --- | --- |
| Adobe Analytics - Versione codice coerente | 5 | È stata trovata più di una versione del codice Analytics. | Sostituisci tutte le istanze di Analytics con la versione corrente.<br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it) |

{style="table-layout:auto"}
