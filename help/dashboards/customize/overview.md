---
keywords: Experience Platform;interfaccia utente;interfaccia utente;dashboard;dashboard;profili;segmenti;destinazioni
title: Panoramica sulla personalizzazione del dashboard
description: Ulteriori informazioni sui modi in cui è possibile personalizzare i dati visualizzati nelle dashboard di Adobe Experience Platform.
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Panoramica sulla personalizzazione del dashboard

Le dashboard di profili, segmenti e destinazioni disponibili in Adobe Experience Platform possono essere personalizzate in diversi modi. Questa guida fornisce una panoramica delle personalizzazioni disponibili, con collegamenti alle istruzioni dettagliate che illustrano come personalizzare i widget visualizzati nelle dashboard, nonché le dimensioni, la forma e la posizione di tali widget.

>[!NOTE]
>
>I widget visualizzati nel dashboard [!UICONTROL Utilizzo licenza] non possono essere personalizzati. Per ulteriori informazioni su questo dashboard univoco, consulta la [documentazione del dashboard di utilizzo della licenza](../guides/license-usage.md).

## Modifica dashboard

Selezionando **[!UICONTROL Modifica dashboard]** dai dashboard di profili, segmenti o destinazioni, puoi regolare le dimensioni, l&#39;ordine e la posizione dei widget attualmente visibili nel dashboard. Per informazioni su come modificare l&#39;aspetto dei widget nelle dashboard, consulta la [guida alla modifica delle dashboard](modify.md).

## Libreria widget

La libreria dei widget all&#39;interno di Experience Platform è il luogo in cui puoi visualizzare tutti i widget [standard](#standard-widgets) e [personalizzati](#custom-widgets) disponibili per la tua organizzazione. Dalle dashboard (ad esempio, dal dashboard dei profili), puoi selezionare **[!UICONTROL Modifica dashboard]** per visualizzare il pulsante **[!UICONTROL Libreria widget]**.

![](../images/customization/modify-dashboard.png)

Seleziona **[!UICONTROL Libreria widget]** per aprire la libreria dei widget e visualizzare tutte le metriche standard disponibili o iniziare a creare widget personalizzati.

![](../images/customization/widget-library-button.png)

### Widget standard {#standard-widgets}

I widget standard fanno riferimento ai widget che Adobe fornisce per l’uso all’interno delle dashboard. Questi widget sono di sola lettura e non possono essere modificati dall’organizzazione.

Nella libreria dei widget, la scheda **[!UICONTROL Standard]** contiene tutti i widget standard disponibili forniti da Adobe. Puoi aggiornare le dashboard utilizzando una qualsiasi di queste metriche standard. Per ulteriori informazioni sull’aggiunta di widget standard al dashboard, consulta la guida all’ [utilizzo dei widget standard nelle dashboard](standard-widgets.md).

### Widget personalizzati {#custom-widgets}

I widget personalizzati si riferiscono ai widget creati e condivisi dai membri dell’organizzazione. Questi widget vengono creati tramite la scheda **[!UICONTROL Personalizzato]** della libreria dei widget e richiedono alla tua organizzazione di specificare le metriche disponibili tramite un [schema](#edit-schema)

Per passaggi completi sulla creazione di widget personalizzati, consulta la guida [widget personalizzati per dashboard](custom-widgets.md).

![](../images/customization/widget-library.png)

#### Modifica di uno schema {#edit-schema}

Per creare un [widget personalizzato](#custom-widgets) per le dashboard, devi prima identificare l&#39;attributo Profilo cliente in tempo reale su cui verrà basato il widget.

Per istruzioni dettagliate su come modificare lo schema dell&#39;organizzazione per creare widget dashboard personalizzati, visita la guida per [modificare lo schema del dashboard](edit-schema.md).

## Passaggi successivi

Dopo aver letto questo documento, puoi iniziare a personalizzare le dashboard di Experience Platform modificando le dimensioni, la forma e l’ordine dei widget esistenti, aggiungendo widget standard forniti da Adobe o creando e condividendo widget personalizzati con la tua organizzazione.
