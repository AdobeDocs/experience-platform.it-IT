---
keywords: Experience Platform;home;argomenti comuni;Connettore dati Analytics;Analytics;Analytics
solution: Experience Platform
title: Connettore sorgente Adobe Analytics per i dati della suite di rapporti
topic: ' - Panoramica'
description: Questo documento fornisce una panoramica di Analytics e descrive i casi d’uso per i dati di Analytics.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---


# Connettore Adobe Analytics per i dati della suite di rapporti

Adobe Experience Platform ti consente di acquisire dati Adobe Analytics tramite Analytics Data Connector (ADC). ADC trasferisce in tempo reale i dati raccolti da [!DNL Analytics] a [!DNL Platform], convertendo i dati in formato SCDS [!DNL Analytics] in campi [!DNL Experience Data Model] (XDM) destinati all’uso da parte di [!DNL Platform].

Questo documento fornisce una panoramica di [!DNL Analytics] e descrive i casi d’uso per i dati [!DNL Analytics].

## Dati di Adobe Analytics e Analytics

[!DNL Analytics] è un potente motore per aiutarti a scoprire di più sui tuoi clienti, su come interagiscono con le tue proprietà web, su dove le tue spese di marketing digitale sono efficaci e individuare le aree di miglioramento. [!DNL Analytics] gestisce migliaia di miliardi di transazioni web all&#39;anno e ADC ti consente di sfruttare facilmente questi ricchi dati comportamentali e arricchire i dati  [!DNL Real-time Customer Profile] in pochi minuti.

![](./images/analytics-data-experience-platform.png)

Ad alto livello, [!DNL Analytics] raccoglie dati da diversi canali digitali e da più centri dati in tutto il mondo. Una volta raccolti i dati, le regole VISTA (Visitor Identification, Segmentation and Transformation Architecture) e le regole di elaborazione vengono applicate per modellare i dati in arrivo. Dopo che i dati grezzi sono stati sottoposti a questa elaborazione leggera, vengono considerati pronti per il consumo da [!DNL Real-time Customer Profile]. In un processo parallelo a quanto sopra, gli stessi dati elaborati vengono micro-batch e acquisiti nei set di dati Platform per l’utilizzo da parte di [!DNL Data Science Workspace], [!DNL Query Service] e altre applicazioni di rilevamento dati.

Per ulteriori informazioni sulle regole di elaborazione, consulta [Panoramica sulle regole di elaborazione](https://docs.adobe.com/content/help/it-IT/analytics/admin/admin-tools/processing-rules/processing-rules.html) .

## Experience Data Model (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni per un&#39;applicazione da utilizzare per comunicare con i servizi su [!DNL Experience Platform].

Il rispetto degli standard XDM consente l&#39;integrazione uniforme dei dati, facilitando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM, consulta la [Panoramica del sistema XDM](../../../xdm/home.md).

## Come vengono mappati i campi da Adobe Analytics a XDM?

Quando viene stabilita una connessione di origine per l’inserimento di dati [!DNL Analytics] in [!DNL Experience Platform] utilizzando l’interfaccia utente [!DNL Platform], i campi dati vengono mappati automaticamente e acquisiti in [!DNL Real-time Customer Profile] in pochi minuti. Per istruzioni su come creare una connessione sorgente con [!DNL Analytics] utilizzando l&#39;interfaccia utente [!DNL Platform], consulta l&#39; [esercitazione sui connettori dati di Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Per informazioni dettagliate sulla mappatura dei campi che si verifica tra [!DNL Analytics] e [!DNL Experience Platform], visita la guida alla [mappatura dei campi di Adobe Analytics](./mapping/analytics.md) .

## Qual è la latenza prevista per i dati di Analytics su Platform?

| Dati di Analytics | Latenza prevista |
| -------------- | ---------------- |
| Nuovi dati su [!DNL Real-time Customer Profile] (A4T **not** abilitato) | &lt; 2 minuti |
| Nuovi dati su [!DNL Real-time Customer Profile] (A4T **è** abilitato) | &lt; 15 minuti |
| Nuovi dati su Data Lake | &lt; 90 minuti |
| Dati di backfill (13 mesi di dati o 10 miliardi di eventi, a seconda di quale sia il valore inferiore). | &lt; 4 settimane |

>[!NOTE]
>
>La latenza varia a seconda della configurazione del cliente, dei volumi di dati e delle applicazioni consumer. Ad esempio, se l’implementazione di Analytics è configurata con `A4T` la latenza alla pipeline aumenterà a 5-10 minuti.

## Identificatori principali nei dati di Analytics

Ogni hit dal connettore dati di Analytics contiene un identificatore principale che dipende dall’esistenza di un ECID o di un AAID. Se è presente un ECID, questo viene designato come identificatore principale. Se è presente un AAID, l’AAID è indicato come primario.