---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore dati di Analytics
topic: overview
translation-type: tm+mt
source-git-commit: 9f0200af0310eafbcc1851b089cfc254cb34af8f

---


# Connettore dati di Analytics

Adobe Experience Platform consente di assimilare i dati di Adobe Analytics tramite il connettore dati di Analytics (ADC). ADC trasferisce in tempo reale i dati raccolti da Adobe Analytics in Platform, convertendo i dati di Analytics formattati SCDS in campi XDM (Experience Data Model) per il consumo in base alla piattaforma.

Questo documento fornisce una panoramica di Adobe Analytics e descrive i casi di utilizzo per i dati di Analytics.

## Dati di Adobe Analytics e Analytics

Adobe Analytics è un potente strumento per aiutarti a conoscere meglio i tuoi clienti, come interagiscono con le tue proprietà web, vedere dove la tua spesa di marketing digitale è efficace e identificare le aree di miglioramento. Adobe Analytics gestisce migliaia di miliardi di transazioni web all&#39;anno e ADC consente di sfruttare facilmente questi ricchi dati comportamentali e di arricchire il profilo cliente in tempo reale in pochi minuti.

![](./images/analytics-data-experience-platform.png)

Ad un livello elevato, Adobe Analytics raccoglie dati da diversi canali digitali e da più centri dati in tutto il mondo. Una volta raccolti i dati, le regole VISTA (Visitor Identification, Segmentation and Transformation Architecture) e le regole di elaborazione vengono applicate per modellare i dati in arrivo. Dopo che i dati grezzi sono stati sottoposti a questa elaborazione leggera, vengono considerati pronti per il consumo dal profilo cliente in tempo reale. In un processo parallelo a quanto sopra, gli stessi dati elaborati vengono sottoposti a micro-batch e trasferiti in set di dati della piattaforma da utilizzare in Data Science Workspace, Query Service e altre applicazioni di rilevamento dati.

Per ulteriori informazioni su VISTA e sulle regole di elaborazione, consulta i documenti seguenti:
* [Panoramica delle regole VISTA](https://marketing.adobe.com/resources/help/en_US/reference/VISTA.html)
* [Panoramica sulle regole di elaborazione](https://docs.adobe.com/content/help/it-IT/analytics/admin/admin-tools/processing-rules/processing-rules.html)

## Modello dati esperienza (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni per un&#39;applicazione da utilizzare per comunicare con i servizi in Adobe Experience Platform.

Il rispetto degli standard XDM consente di incorporare uniformemente i dati, facilitando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM, vedere la panoramica [del sistema](../../../xdm/home.md)XDM.

## Come vengono mappati i campi da Adobe Analytics a XDM?

Quando viene stabilita una connessione di origine per l&#39;inserimento dei dati di Analytics nella piattaforma Experience tramite l&#39;interfaccia utente della piattaforma, i campi di dati vengono automaticamente mappati e trasferiti nel profilo cliente in tempo reale in pochi minuti. Per istruzioni sulla creazione di una connessione di origine con Adobe Analytics tramite l&#39;interfaccia utente della piattaforma, consulta l&#39;esercitazione [sui connettori dati di](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/adobe-analytics-ui-tutorial.md)Analytics.

Per informazioni dettagliate sulla mappatura dei campi che si verifica tra Analytics e Experience Platform, consultate la guida alla mappatura [dei campi di](./analytics-mapping.md) Adobe Analytics.

## Qual è la latenza prevista per i dati di Analytics sulla piattaforma?

| Dati di Analytics | Latenza prevista |
| -------------- | ---------------- |
| Nuovi dati sul profilo cliente in tempo reale (A4T **non** abilitato) | &lt; 2 minuti |
| Nuovi dati sul profilo cliente in tempo reale (A4T **è** abilitato) | &lt; 15 minuti |
| Nuovi dati su Data Lake | &lt; 45 minuti |
| Dati di backfill (13 mesi di dati o 10 miliardi di eventi, a seconda di quale sia il valore inferiore) | &lt; 4 settimane |

>[!NOTE] La latenza varia a seconda della configurazione del cliente, dei volumi di dati e delle applicazioni consumer. Ad esempio, se l&#39;implementazione di Analytics è configurata con `A4T` la latenza a Pipeline, aumenterà a 5-10 minuti.