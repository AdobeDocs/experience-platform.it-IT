---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore dati  Analytics
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 2%

---


#  Analytics Data Connector

 Adobe Experience Platform consente di acquisire  dati Adobe Analytics tramite il connettore dati  Analytics (ADC). ADC trasferisce in tempo reale i dati raccolti da  Adobe Analytics ad Platform, convertendo i dati Analytics  formati SCDS in campi XDM (Experience Data Model) per l’utilizzo da parte di Platform.

Questo documento fornisce una panoramica di  Adobe Analytics e descrive i casi di utilizzo per  dati Analytics.

##  dati Adobe Analytics e  Analytics

 Adobe Analytics è un potente strumento per aiutarti a conoscere meglio i tuoi clienti, come interagiscono con le tue proprietà web, vedere dove la tua spesa di marketing digitale è efficace e identificare le aree di miglioramento.  Adobe Analytics gestisce migliaia di miliardi di transazioni web all&#39;anno e ADC ti permette di attingere facilmente a questi ricchi dati comportamentali e arricchire il profilo cliente in tempo reale in pochi minuti.

![](./images/analytics-data-experience-platform.png)

Ad un livello elevato,  Adobe Analytics raccoglie dati da diversi canali digitali e centri dati in tutto il mondo. Una volta raccolti i dati, le regole VISTA (Visitor Identification, Segmentation and Transformation Architecture) e le regole di elaborazione vengono applicate per modellare i dati in arrivo. Dopo che i dati grezzi sono stati sottoposti a questa elaborazione leggera, vengono considerati pronti per il consumo dal profilo cliente in tempo reale. In un processo parallelo a quanto sopra, gli stessi dati elaborati vengono assemblati in batch micro e inseriti in set di dati Platform da utilizzare in Data Science Workspace, Query Service e altre applicazioni di rilevamento dati.

Per ulteriori informazioni sulle regole di elaborazione, vedere Panoramica [delle regole di](https://docs.adobe.com/content/help/it-IT/analytics/admin/admin-tools/processing-rules/processing-rules.html) elaborazione.

## Modello dati esperienza (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni per un&#39;applicazione da utilizzare per comunicare con i servizi  Adobe Experience Platform.

Il rispetto degli standard XDM consente di incorporare uniformemente i dati, facilitando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM, vedere la panoramica [del sistema](../../../xdm/home.md)XDM.

## Come vengono mappati i campi da  Adobe Analytics a XDM?

Quando viene stabilita una connessione di origine per l&#39;inserimento  dati Analytics nel Experience Platform  utilizzando l&#39;interfaccia utente di Platform, i campi di dati vengono automaticamente mappati e trasferiti nel profilo cliente in tempo reale in pochi minuti. Per istruzioni sulla creazione di una connessione di origine con  Adobe Analytics tramite l&#39;interfaccia utente di Platform, vedere l&#39;esercitazione [sul connettore dati di](../../tutorials/ui/create/adobe-applications/analytics.md)Analytics.

Per informazioni dettagliate sulla mappatura dei campi che si verifica tra  Analytics e  Experience Platform, visitare la guida alla mappatura [dei campi di Adobe Analytics](./mapping/analytics.md) .

## Qual è la latenza prevista per  dati Analytics su Platform?

|  dati Analytics | Latenza prevista |
| -------------- | ---------------- |
| Nuovi dati sul profilo cliente in tempo reale (A4T **non** abilitato) | &lt; 2 minuti |
| Nuovi dati sul profilo cliente in tempo reale (A4T **è** abilitato) | &lt; 15 minuti |
| Nuovi dati su Data Lake | &lt; 45 minuti |
| Dati di backfill (13 mesi di dati o 10 miliardi di eventi, a seconda di quale sia il valore inferiore) | &lt; 4 settimane |

>[!NOTE]
>
>La latenza varia a seconda della configurazione del cliente, dei volumi di dati e delle applicazioni consumer. Ad esempio, se l&#39;implementazione di Analytics  è configurata con `A4T` la latenza su Pipeline, aumenterà a 5-10 minuti.