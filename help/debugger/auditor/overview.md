---
title: Scheda Auditor
description: Scopri come utilizzare la scheda Auditor in Adobe Experience Platform Debugger per testare le implementazioni Adobe Experience Cloud.
keywords: debugger;estensione debugger di experience platform;chrome;estensione;auditor;dtm;target
exl-id: 409094f8-a7d9-45f7-ba12-b5e6250abc0f
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 32%

---

# Scheda Auditor

Ad Adobe Experience Platform Debugger, puoi utilizzare la scheda **[!UICONTROL Auditor]** per eseguire una serie di test di audit sulla pagina.

Per utilizzare questa funzione:

1. Seleziona **[!UICONTROL Auditor]** nella navigazione a sinistra.
1. Selezionare **[!UICONTROL Esegui test Auditor]**. Una volta completati i test, i relativi risultati vengono visualizzati di seguito.

![Schermata dei risultati del test nella scheda Auditor](../images/auditor-results.png)

L’elenco mostra il test e il relativo risultato e fornisce suggerimenti per risolvere eventuali problemi.

## Interpretazione dei risultati dei test

Ogni test è ponderato e il punteggio del test è uguale al peso assegnato. Se supera un test con un peso di 5, riceverà cinque punti.

| Punteggio | Descrizione |
| --- | --- |
| 0 | Segnala eventuali problemi di cui dovresti essere a conoscenza, ma che non influiscono sul punteggio. |
| 1 | Consiglia un’ottimizzazione. Nessun impatto sulla precisione dei dati. |
| 2 | Se il test non viene superato, non potrai accedere alle funzioni e alle correzioni più recenti in Adobe Experience Cloud. |
| 3 | Test di efficienza e verifica se l’implementazione segue le best practice. |
| 4 | In caso di errore, è possibile che si raccolgano dati non affidabili. |
| 5 | In caso di errore, è possibile che si verifichi una perdita di dati. |

Tutti i test hanno esito positivo o negativo. Essi verificano la conformità o la non conformità alle condizioni di prova, pertanto non vi sono punteggi parziali per la conformità parziale. Ad esempio, se il test verifica la versione più recente di una soluzione Adobe e si è in ritardo di una sola versione, si ottiene la stessa valutazione come se si fosse in ritardo di cinque versioni. Le versioni più recenti includono miglioramenti delle prestazioni e correzioni di bug, per cui si consiglia di utilizzare la versione più recente.

È **vivamente consigliato** correggere i risultati di livello 4 o 5.

È **consigliato** correggere i risultati di livello da 1 a 3.

## Tecnologie Adobe supportate

La funzione di auditor è in grado di valutare le seguenti tecnologie di Adobe:

* Adobe Advertising Cloud DSP
* Adobe Advertising Cloud Search
* Adobe Analytics
* Adobe Experience Cloud Identity Service
* Adobe Target
* Tag (precedentemente Adobe Experience Platform Launch)

## Valutazioni dei test

Per ulteriori informazioni sulle valutazioni dei test fornite da questa funzione, consulta i seguenti documenti:

* [Coerenza tag](./tag-consistency.md)
* [Presenza tag](./tag-presence.md)
* [Configurazione](./configuration.md)
* [Avvisi](./alerts.md)
