---
keywords: Experience Platform;interfaccia utente;interfaccia utente;dashboard;dashboard;profili;segmenti;destinazioni
title: Panoramica sulla personalizzazione del dashboard
description: Ulteriori informazioni sui modi in cui è possibile personalizzare i dati visualizzati nelle dashboard di Adobe Experience Platform.
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Panoramica sulla personalizzazione del dashboard

Le dashboard di profili, segmenti e destinazioni disponibili in Adobe Experience Platform possono essere personalizzate in diversi modi. Questa guida fornisce una panoramica delle personalizzazioni disponibili, con collegamenti alle istruzioni dettagliate che illustrano come personalizzare i widget visualizzati nelle dashboard, nonché le dimensioni, la forma e la posizione di tali widget.

>[!NOTE]
>
>I widget visualizzati nella [!UICONTROL Utilizzo della licenza] impossibile personalizzare il dashboard. Per ulteriori informazioni su questo dashboard univoco, consulta la sezione [documentazione del dashboard di utilizzo della licenza](../guides/license-usage.md).

## Modifica dashboard

Selezione **[!UICONTROL Modifica dashboard]** dalle dashboard di profili, segmenti o destinazioni è possibile regolare dimensioni, ordine e posizione dei widget attualmente visibili nel dashboard. Per informazioni su come modificare l’aspetto dei widget nelle dashboard, consulta [modifica della guida alle dashboard](modify.md).

## Libreria widget

La libreria di widget all&#39;interno di Experience Platform è il luogo in cui puoi visualizzare tutti gli [standard](#standard-widgets) e [personalizzato](#custom-widgets) widget disponibili per la tua organizzazione. Dalle dashboard (ad esempio, dal dashboard dei profili), puoi selezionare **[!UICONTROL Modifica dashboard]** per visualizzare il **[!UICONTROL Libreria widget]** pulsante .

![Dashboard Profili con dashboard Modifica evidenziato.](../images/customization/modify-dashboard.png)

Seleziona **[!UICONTROL Libreria widget]** per aprire la libreria widget e visualizzare tutte le metriche standard disponibili o iniziare a creare widget personalizzati.

![Dashboard Profili con libreria Widget evidenziata.](../images/customization/widget-library-button.png)

### Widget standard {#standard-widgets}

I widget standard fanno riferimento ai widget che Adobe fornisce per l’uso all’interno delle dashboard. Questi widget sono di sola lettura e non possono essere modificati dall’organizzazione.

Nella libreria dei widget, la **[!UICONTROL Standard]** La scheda contiene tutti i widget standard disponibili forniti da Adobe. Puoi aggiornare le dashboard utilizzando una qualsiasi di queste metriche standard. Per ulteriori informazioni sull’aggiunta di widget standard al dashboard, consulta la guida per [utilizzo di widget standard nelle dashboard](standard-widgets.md).

### Widget personalizzati {#custom-widgets}

I widget personalizzati si riferiscono ai widget creati e condivisi dai membri dell’organizzazione. Questi widget vengono creati tramite **[!UICONTROL Personalizzato]** della libreria widget e richiedono alla tua organizzazione di specificare le metriche disponibili tramite un [schema](#edit-schema)

Per i passaggi completi per la creazione di widget personalizzati, consulta [guida ai widget personalizzati per dashboard](custom-widgets.md).

![Area di lavoro libreria widget con evidenziati Standard e Personalizzato.](../images/customization/widget-library.png)

#### Modifica di uno schema {#edit-schema}

Per creare un [widget personalizzato](#custom-widgets) per le dashboard, devi innanzitutto identificare l’attributo Profilo cliente in tempo reale su cui verrà basato il widget.

Per istruzioni dettagliate su come modificare lo schema dell’organizzazione per creare widget dashboard personalizzati, visita la guida per [modifica dello schema del dashboard](edit-schema.md).

## Passaggi successivi

Dopo aver letto questo documento, puoi iniziare a personalizzare le dashboard di Experience Platform modificando le dimensioni, la forma e l’ordine dei widget esistenti, aggiungendo widget standard forniti da Adobe o creando e condividendo widget personalizzati con la tua organizzazione.
