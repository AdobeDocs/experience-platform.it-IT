---
keywords: Experience Platform;interfaccia utente;interfaccia utente;dashboard;dashboard;profili;segmenti;destinazioni;utilizzo licenza;widget;metriche;
title: Creazione di widget personalizzati per dashboard
description: 'Questa guida fornisce istruzioni dettagliate per la creazione di widget personalizzati da utilizzare nelle dashboard di Adobe Experience Platform. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Creazione di widget personalizzati per dashboard

In Adobe Experience Platform puoi visualizzare e interagire con i dati dell’organizzazione utilizzando più dashboard. È inoltre possibile aggiornare alcune dashboard aggiungendo nuovi widget alla vista dashboard. Oltre ai widget standard forniti da Adobe, puoi anche creare widget personalizzati e condividerli all’interno della tua organizzazione.

Questa guida fornisce istruzioni dettagliate per creare e aggiungere widget personalizzati ai dashboard [!UICONTROL Profili], [!UICONTROL Segmenti] e [!UICONTROL Destinazioni] nell’interfaccia utente di Platform.

Per ulteriori informazioni sui widget standard, consulta la guida all’ [aggiunta di widget standard alle dashboard](standard-widgets.md).

>[!NOTE]
>
>I widget visualizzati nel dashboard [!UICONTROL Utilizzo licenza] non possono essere personalizzati. Per ulteriori informazioni su questo dashboard univoco, consulta la [documentazione del dashboard di utilizzo della licenza](../guides/license-usage.md).

## Libreria widget {#widget-library}

Questa guida richiede l&#39;accesso alla [!UICONTROL Libreria widget] all&#39;interno di Experience Platform. Per ulteriori informazioni sulla libreria di widget e su come accedervi nell&#39;interfaccia utente, inizia leggendo la [panoramica della libreria di widget](widget-library.md).

## Guida introduttiva ai widget personalizzati

Nella libreria dei widget, la scheda **[!UICONTROL Personalizzato]** consente di creare widget e condividerli con altri utenti dell’organizzazione al fine di personalizzare l’aspetto delle dashboard.

>[!IMPORTANT]
>
>La tua organizzazione può creare un massimo di 20 widget personalizzati nella libreria dei widget.

Seleziona la scheda **[!UICONTROL Personalizzato]** per iniziare a creare widget personalizzati o per visualizzare widget personalizzati già creati dalla tua organizzazione.

![](../images/customization/custom-widgets.png)

## Creare un widget personalizzato

Per creare un widget personalizzato, seleziona **[!UICONTROL Crea]** dal centro della libreria dei widget oppure, se i widget personalizzati sono già stati creati, seleziona **[!UICONTROL Crea widget]** dall&#39;angolo in alto a destra della libreria dei widget.

![](../images/customization/create-widget.png)

Nella finestra di dialogo **[!UICONTROL Crea widget]**, puoi fornire un titolo e una descrizione per il nuovo widget e scegliere l&#39;attributo che desideri visualizzare.

>[!NOTE]
>
>L’elenco degli attributi disponibili dipende dallo schema configurato per la tua organizzazione. Per ulteriori informazioni sulla selezione degli attributi e sulla configurazione dello schema, consulta la guida alla [modifica dello schema per creare widget personalizzati](edit-schema.md).

Per scegliere un attributo, selezionare il pulsante di scelta accanto all&#39;attributo che si desidera aggiungere.

>[!NOTE]
>
>È possibile selezionare un solo attributo per widget e creare un solo widget per attributo. Se un widget è già stato creato per un attributo, questo viene visualizzato in grigio.

![](../images/customization/create-widget-dialog.png)

## Anteprima widget personalizzato

Nella finestra di dialogo viene visualizzata un&#39;anteprima del nuovo widget, che mostra un grafico a barre orizzontale con dati simmetrici.

>[!NOTE]
>
>L’unica metrica attualmente supportata per tutti gli attributi è il conteggio dei profili e l’unica visualizzazione attualmente supportata per i widget personalizzati è un grafico a barre orizzontale.
>
>I dati mostrati nel widget di esempio sono solo a scopo illustrativo. L’anteprima non visualizza i dati effettivi provenienti dall’organizzazione.

![](../images/customization/create-widget-select-attribute.png)

Per salvare il nuovo widget e tornare alla scheda [!UICONTROL Personalizzato], seleziona **[!UICONTROL Crea]**. Il nuovo widget è ora disponibile per essere aggiunto a un dashboard scegliendo il widget dalla libreria e selezionando **[!UICONTROL Aggiungi widget]**.

## Archiviare un widget personalizzato

Dopo aver aggiunto un widget alla libreria, può essere archiviato utilizzando il pulsante **[!UICONTROL Archivia]** . Puoi anche modificare il widget per aggiornare i campi titolo o descrizione.

## Passaggi successivi

Dopo aver letto questo documento, potrai accedere alla libreria widget e utilizzarla per creare e aggiungere widget personalizzati per la tua organizzazione. Per modificare le dimensioni e la posizione dei widget visualizzati nel dashboard, fare riferimento alla [guida alla modifica delle dashboard](modify.md).
