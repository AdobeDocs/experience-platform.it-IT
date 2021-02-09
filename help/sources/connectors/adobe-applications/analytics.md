---
keywords: ' Experience Platform;home;argomenti più comuni;Analytics Data Connector;analytics;Analytics'
solution: Experience Platform
title: ' Adobe Analytics Source Connector per i dati delle suite di rapporti'
topic: overview
description: Questo documento fornisce una panoramica di Analytics e descrive i casi di utilizzo per i dati di Analytics.
translation-type: tm+mt
source-git-commit: e480ce789c849db24713da312345ea3162e617a6
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 2%

---


#  connettore Adobe Analytics per i dati della suite di rapporti

Adobe Experience Platform consente di acquisire  dati Adobe Analytics tramite il connettore dati di Analytics (ADC). ADC trasferisce in tempo reale i dati raccolti da [!DNL Analytics] a [!DNL Platform], convertendo i dati in formato SCDS [!DNL Analytics] in campi [!DNL Experience Data Model] (XDM) da utilizzare in [!DNL Platform].

Questo documento fornisce una panoramica di [!DNL Analytics] e descrive i casi di utilizzo per i dati [!DNL Analytics].

##  dati Adobe Analytics e Analytics

[!DNL Analytics] è un potente strumento per aiutarti a conoscere meglio i tuoi clienti, come interagiscono con le tue proprietà web, vedere dove la tua spesa di marketing digitale è efficace e identificare le aree di miglioramento. [!DNL Analytics] gestisce migliaia di miliardi di transazioni web all&#39;anno e ADC consente di attingere facilmente a questi dati comportamentali complessi e arricchire il  [!DNL Real-time Customer Profile] tutto in pochi minuti.

![](./images/analytics-data-experience-platform.png)

Ad un livello elevato, [!DNL Analytics] raccoglie dati da diversi canali digitali e da più centri dati in tutto il mondo. Una volta raccolti i dati, le regole VISTA (Visitor Identification, Segmentation and Transformation Architecture) e le regole di elaborazione vengono applicate per modellare i dati in arrivo. Dopo che i dati grezzi sono stati sottoposti a questa elaborazione leggera, vengono considerati pronti per il consumo da [!DNL Real-time Customer Profile]. In un processo parallelo a quanto sopra, gli stessi dati elaborati vengono sottoposti a micro-batch e trasferiti in set di dati della piattaforma da utilizzare per [!DNL Data Science Workspace], [!DNL Query Service] e altre applicazioni di rilevamento dati.

Per ulteriori informazioni sulle regole di elaborazione, vedere [Panoramica sulle regole di elaborazione](https://docs.adobe.com/content/help/it-IT/analytics/admin/admin-tools/processing-rules/processing-rules.html).

## Modello dati esperienza (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni per un&#39;applicazione da utilizzare per comunicare con i servizi su [!DNL Experience Platform].

Il rispetto degli standard XDM consente di incorporare uniformemente i dati, facilitando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM, vedere la [Panoramica del sistema XDM](../../../xdm/home.md).

## Come vengono mappati i campi da  Adobe Analytics a XDM?

Quando viene stabilita una connessione di origine per l&#39;inserimento di dati [!DNL Analytics] in [!DNL Experience Platform] utilizzando l&#39;interfaccia utente [!DNL Platform], i campi di dati vengono mappati automaticamente e trasferiti in [!DNL Real-time Customer Profile] in pochi minuti. Per istruzioni su come creare una connessione di origine con [!DNL Analytics] utilizzando l&#39;interfaccia utente di [!DNL Platform], vedere l&#39;esercitazione sui connettori dati di [Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Per informazioni dettagliate sulla mappatura dei campi che si verifica tra [!DNL Analytics] e [!DNL Experience Platform], visitare la guida [ mappatura dei campi Adobe Analytics](./mapping/analytics.md).

## Qual è la latenza prevista per i dati di Analytics sulla piattaforma?

| Dati di Analytics | Latenza prevista |
| -------------- | ---------------- |
| Nuovi dati su [!DNL Real-time Customer Profile] (A4T **not** abilitato) | &lt; 2 minuti |
| Nuovi dati su [!DNL Real-time Customer Profile] (A4T **is** abilitato) | &lt; 15 minuti |
| Nuovi dati su Data Lake | &lt; 90 minuti |
| Dati di backfill (13 mesi di dati o 10 miliardi di eventi, a seconda di quale sia il valore inferiore) | &lt; 4 settimane |

>[!NOTE]
>
>La latenza varia a seconda della configurazione del cliente, dei volumi di dati e delle applicazioni consumer. Ad esempio, se l&#39;implementazione di Analytics è configurata con `A4T` la latenza nella pipeline aumenterà a 5-10 minuti.

## Identificatori principali nei dati di Analytics

Ogni hit dal connettore dati di Analytics contiene un identificatore primario, a seconda che esista un ECID o un AAID. In presenza di un ECID, l’ECID è designato come identificatore principale. Se è presente un AAID, l’AAID viene indicato come primario.