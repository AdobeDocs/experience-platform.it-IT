---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore dati di Analytics
topic: overview
translation-type: tm+mt
source-git-commit: 662ca170b7416dfb55cfb6b8cbaef640c1f83d31
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 2%

---


# Connettore dati di Analytics

Adobe Experience Platform consente di acquisire  dati Adobe Analytics tramite il connettore dati di Analytics (ADC). ADC trasferisce i dati raccolti da [!DNL Analytics] a [!DNL Platform] in tempo reale, convertendo i [!DNL Analytics] dati in formato SCDS in campi [!DNL Experience Data Model] (XDM) da utilizzare [!DNL Platform].

Questo documento fornisce una panoramica [!DNL Analytics] e descrive i casi di utilizzo dei [!DNL Analytics] dati.

##  dati Adobe Analytics e Analytics

[!DNL Analytics] è un potente strumento per aiutarti a conoscere meglio i tuoi clienti, come interagiscono con le tue proprietà web, vedere dove la tua spesa di marketing digitale è efficace e identificare le aree di miglioramento. [!DNL Analytics] gestisce migliaia di miliardi di transazioni web all&#39;anno e ADC consente di attingere facilmente a questi ricchi dati comportamentali e arricchire il [!DNL Real-time Customer Profile] tutto in pochi minuti.

![](./images/analytics-data-experience-platform.png)

Ad un livello elevato, [!DNL Analytics] raccoglie dati da diversi canali digitali e da più centri dati in tutto il mondo. Una volta raccolti i dati, le regole VISTA (Visitor Identification, Segmentation and Transformation Architecture) e le regole di elaborazione vengono applicate per modellare i dati in arrivo. Dopo che i dati grezzi sono stati sottoposti a questa elaborazione leggera, vengono considerati pronti per il consumo da [!DNL Real-time Customer Profile]. In un processo parallelo a quanto sopra, gli stessi dati elaborati vengono sottoposti a micro-batch e trasferiti in set di dati della piattaforma per l&#39;utilizzo da parte di [!DNL Data Science Workspace], [!DNL Query Service]e altre applicazioni di rilevamento dei dati.

Per ulteriori informazioni sulle regole di elaborazione, vedere Panoramica [delle regole di](https://docs.adobe.com/content/help/it-IT/analytics/admin/admin-tools/processing-rules/processing-rules.html) elaborazione.

## Modello dati esperienza (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni per un&#39;applicazione da utilizzare per comunicare con i servizi [!DNL Experience Platform].

Il rispetto degli standard XDM consente di incorporare uniformemente i dati, facilitando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM, vedere la panoramica [del sistema](../../../xdm/home.md)XDM.

## Come vengono mappati i campi da  Adobe Analytics a XDM?

Quando viene stabilita una connessione di origine per l&#39;inserimento [!DNL Analytics] dei dati [!DNL Experience Platform] nell&#39;interfaccia [!DNL Platform] utente, i campi dati vengono mappati automaticamente e trasferiti [!DNL Real-time Customer Profile] in pochi minuti. Per istruzioni su come creare una connessione di origine con [!DNL Analytics] l&#39; [!DNL Platform] interfaccia utente, consulta l&#39;esercitazione [sui connettori dati di](../../tutorials/ui/create/adobe-applications/analytics.md)Analytics.

Per informazioni dettagliate sulla mappatura dei campi che si verifica tra [!DNL Analytics] e [!DNL Experience Platform], consultare la guida alla mappatura [dei campi di](./mapping/analytics.md) Adobe Analytics.

## Qual è la latenza prevista per i dati di Analytics sulla piattaforma?

| Dati di Analytics | Latenza prevista |
| -------------- | ---------------- |
| Nuovi dati su [!DNL Real-time Customer Profile] (A4T **non** abilitato) | &lt; 2 minuti |
| Nuovi dati su [!DNL Real-time Customer Profile] (A4T **è** abilitato) | &lt; 15 minuti |
| Nuovi dati su Data Lake | &lt; 45 minuti |
| Dati di backfill (13 mesi di dati o 10 miliardi di eventi, a seconda di quale sia il valore inferiore) | &lt; 4 settimane |

>[!NOTE] La latenza varia a seconda della configurazione del cliente, dei volumi di dati e delle applicazioni consumer. Ad esempio, se l&#39;implementazione di Analytics è configurata con `A4T` la latenza a Pipeline, aumenterà a 5-10 minuti.

## Identificatori principali nei dati di Analytics

Ogni hit dal connettore dati di Analytics contiene un identificatore primario, a seconda che esista un ECID o un AAID. In presenza di un ECID, l’ECID è designato come identificatore principale. Se è presente un AAID, l’AAID viene indicato come primario.