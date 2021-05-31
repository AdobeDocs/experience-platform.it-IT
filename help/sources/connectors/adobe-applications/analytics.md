---
keywords: Experience Platform;home;argomenti popolari;Connettore origine Analytics;analytics;Analytics
solution: Experience Platform
title: Connettore sorgente Adobe Analytics per i dati della suite di rapporti
topic-legacy: overview
description: Questo documento fornisce una panoramica di Analytics e descrive i casi d’uso per i dati di Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Connettore sorgente Adobe Analytics per i dati della suite di rapporti

Adobe Experience Platform consente di acquisire i dati di Adobe Analytics tramite il connettore di origine di Analytics. Il connettore di origine [!DNL Analytics] invia in tempo reale i dati raccolti da [!DNL Analytics] a Platform, convertendo i dati in formato SCDS [!DNL Analytics] in campi [!DNL Experience Data Model] (XDM) destinati all’utilizzo da parte di Platform.

Questo documento fornisce una panoramica di [!DNL Analytics] e descrive i casi d’uso per i dati [!DNL Analytics].

## Dati di Adobe Analytics e Analytics

[!DNL Analytics] è un motore potente che ti aiuta a scoprire di più sui tuoi clienti, su come interagiscono con le tue proprietà web, su dove le tue spese di marketing digitale sono efficaci e individua le aree di miglioramento. [!DNL Analytics] gestisce migliaia di miliardi di transazioni web all&#39;anno e il connettore  [!DNL Analytics] sorgente ti permette di sfruttare facilmente questi dati comportamentali e arricchire il  [!DNL Real-time Customer Profile] in pochi minuti.

![](./images/analytics-data-experience-platform.png)

Ad alto livello, [!DNL Analytics] raccoglie dati da diversi canali digitali e da più centri dati in tutto il mondo. Una volta raccolti i dati, vengono applicate le regole VISTA (Visitor Identification, Segmentation and Transformation Architecture) e le regole di elaborazione per modellare i dati in arrivo. Dopo che i dati grezzi sono stati sottoposti a questa elaborazione leggera, vengono considerati pronti per il consumo da [!DNL Real-time Customer Profile]. In un processo parallelo a quanto sopra, gli stessi dati elaborati vengono micro-batch e acquisiti nei set di dati Platform per l’utilizzo da parte di [!DNL Data Science Workspace], [!DNL Query Service] e altre applicazioni di rilevamento dati.

Per ulteriori informazioni sulle regole di elaborazione, consulta la [panoramica delle regole di elaborazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) .

## Experience Data Model (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni per un&#39;applicazione da utilizzare per comunicare con i servizi su Experience Platform.

Il rispetto degli standard XDM consente l&#39;integrazione uniforme dei dati, facilitando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM, consulta la [Panoramica del sistema XDM](../../../xdm/home.md).

## Come vengono mappati i campi da Adobe Analytics a XDM?

Quando viene stabilita una connessione di origine per l’inserimento di dati [!DNL Analytics] in Experience Platform tramite l’interfaccia utente di Platform, i campi di dati vengono mappati e acquisiti automaticamente in [!DNL Real-time Customer Profile] in pochi minuti. Per istruzioni su come creare una connessione sorgente con [!DNL Analytics] utilizzando l’interfaccia utente di Platform, consulta l’ [esercitazione sul connettore sorgente di Analytics](../../tutorials/ui/create/adobe-applications/analytics.md) .

Per informazioni dettagliate sulla mappatura dei campi che si verifica tra [!DNL Analytics] e l&#39;Experience Platform, consulta la guida [Mappatura dei campi Adobe Analytics](./mapping/analytics.md) .

## Qual è la latenza prevista per i dati di Analytics su Platform?

| Dati di Analytics | Latenza prevista |
| -------------- | ---------------- |
| Nuovi dati su [!DNL Real-time Customer Profile] (A4T **not** abilitato) | &lt; 2 minuti |
| Nuovi dati su [!DNL Real-time Customer Profile] (A4T **è** abilitato) | &lt; 15 minuti |
| Nuovi dati su Data Lake | &lt; 90 minuti |
| Dati di backfill (13 mesi di dati o 10 miliardi di eventi, a seconda di quale sia il valore inferiore). | &lt; 4 settimane |

>[!NOTE]
>
>La latenza varia a seconda della configurazione del cliente, dei volumi di dati e delle applicazioni consumer. Ad esempio, se l’implementazione [!DNL Analytics] è configurata con `A4T` la latenza alla pipeline aumenterà a 5-10 minuti.

## Identificatori principali nei dati [!DNL Analytics]

Ogni hit dal connettore di origine [!DNL Analytics] contiene un identificatore principale che dipende dall&#39;esistenza di un ECID o di un AAID. Se è presente un ECID, questo viene designato come identificatore principale. Se è presente un AAID, l’AAID è indicato come primario.
