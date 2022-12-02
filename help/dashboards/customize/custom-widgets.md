---
keywords: Experience Platform;interfaccia utente;interfaccia utente;dashboard;dashboard;profili;segmenti;destinazioni;utilizzo licenza;widget;metriche;
title: Creazione di widget personalizzati per dashboard
description: Questa guida fornisce istruzioni dettagliate per la creazione di widget personalizzati da utilizzare nelle dashboard di Adobe Experience Platform.
exl-id: 0168ab1e-0b7d-4faf-852e-7208a2b09a04
source-git-commit: 386d805eadf335b95b6eac92c7663fcee17b4b2d
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Creazione di widget personalizzati per dashboard

In Adobe Experience Platform puoi visualizzare e interagire con i dati dell’organizzazione utilizzando più dashboard. È inoltre possibile aggiornare alcune dashboard aggiungendo nuovi widget alla vista dashboard. Oltre ai widget standard forniti da Adobe, puoi anche creare widget personalizzati e condividerli all’interno della tua organizzazione.

Questa guida fornisce istruzioni dettagliate per la creazione e l’aggiunta di widget personalizzati al [!UICONTROL Profili], [!UICONTROL Segmenti]e [!UICONTROL Destinazioni] dashboard nell’interfaccia utente di Platform.

Per ulteriori informazioni sui widget standard, consulta la guida per [aggiunta di widget standard alle dashboard](standard-widgets.md).

>[!NOTE]
>
>I widget visualizzati nella [!UICONTROL Utilizzo della licenza] impossibile personalizzare il dashboard. Per ulteriori informazioni su questo dashboard univoco, consulta la sezione [documentazione del dashboard di utilizzo della licenza](../guides/license-usage.md).

## Libreria widget {#widget-library}

Questa guida richiede l’accesso al [!UICONTROL Libreria widget] all&#39;Experience Platform. Per ulteriori informazioni sulla libreria di widget e su come accedervi nell&#39;interfaccia utente, leggi la [panoramica della libreria widget](widget-library.md).

## Guida introduttiva ai widget personalizzati

Nella libreria dei widget, la **[!UICONTROL Personalizzato]** consente di creare widget e condividerli con altri utenti dell’organizzazione al fine di personalizzare l’aspetto delle dashboard.

>[!IMPORTANT]
>
>La tua organizzazione può creare un massimo di 20 widget personalizzati nella libreria dei widget.

Seleziona la **[!UICONTROL Personalizzato]** per iniziare a creare widget personalizzati o per visualizzare widget personalizzati già creati dalla tua organizzazione.

![Area di lavoro libreria widget con la scheda Personalizzato evidenziata.](../images/customization/custom-widgets.png)

## Creare un widget personalizzato

Per creare un widget personalizzato, seleziona **[!UICONTROL Widget per creazione]** dall&#39;angolo in alto a destra della libreria widget oppure, se si tratta del primo widget personalizzato della tua organizzazione, seleziona **[!UICONTROL Crea]** dal centro della libreria widget.

![Scheda Personalizzato dell’area di lavoro della libreria widget con Crea evidenziato.](../images/customization/create-widget.png)

In **[!UICONTROL Widget per creazione]** , fornisci un titolo e una descrizione per il nuovo widget e scegli l&#39;attributo che desideri visualizzare.

>[!NOTE]
>
>L’elenco degli attributi disponibili dipende dallo schema configurato per la tua organizzazione. Per ulteriori informazioni sulla selezione degli attributi e sulla configurazione dello schema, consulta la guida in [modifica dello schema per creare widget personalizzati](edit-schema.md).

Per scegliere un attributo, selezionare il pulsante di scelta accanto all&#39;attributo che si desidera aggiungere.

>[!NOTE]
>
>È possibile selezionare un solo attributo per widget e creare un solo widget per attributo. Se un widget è già stato creato per un attributo, questo viene visualizzato in grigio.

![Finestra di dialogo Crea widget .](../images/customization/create-widget-dialog.png)

## Selezionare una visualizzazione

Dopo aver selezionato un attributo, nella finestra di dialogo viene visualizzata un&#39;anteprima del nuovo widget. L’intelligenza artificiale viene utilizzata per selezionare automaticamente una visualizzazione che si adatta al meglio ai dati degli attributi e per fornire opzioni di visualizzazione aggiuntive selezionabili manualmente.

A seconda dell’attributo , l’intelligenza artificiale consiglia diverse opzioni di visualizzazione. L’elenco completo delle visualizzazioni include:

* Grafico a barre orizzontali: Le linee orizzontali vengono utilizzate per rappresentare i valori.
* Grafico a barre verticale: Le linee verticali sono utilizzate per rappresentare i valori.
* Grafico a torta: Analogamente a un grafico a torta, i valori vengono visualizzati come parti o parti di un intero.
* Grafico a dispersione: Utilizza un asse orizzontale e verticale per indicare i valori.
* Grafico a linee: I valori vengono visualizzati utilizzando una singola riga per mostrare le modifiche nel corso di un periodo di tempo.
* Scheda numerata: Visualizza un numero di riepilogo che rappresenta un singolo valore chiave.
* Tabella dati: I valori vengono visualizzati come righe in una tabella.

>[!NOTE]
>
>L’unica metrica attualmente supportata per tutti gli attributi è il conteggio dei profili.
>
>I dati mostrati nel widget di esempio sono solo a scopo illustrativo. L’anteprima non visualizza i dati effettivi provenienti dall’organizzazione.

Per salvare il nuovo widget e tornare al [!UICONTROL Personalizzato] scheda , seleziona **[!UICONTROL Crea]**.

![Finestra di dialogo Crea widget con le opzioni di visualizzazione e Crea evidenziato.](../images/customization/create-widget-select-attribute.png)

Il nuovo widget è ora disponibile per essere aggiunto a un dashboard scegliendo il widget dalla libreria e selezionando **[!UICONTROL Aggiungi widget]**.

![La scheda Personalizzato dell&#39;area di lavoro della libreria widget con i nuovi widget e Aggiungi widget evidenziati.](../images/customization/custom-widgets-new.png)

## Nascondere un widget personalizzato

Dopo aver aggiunto un widget alla libreria, può essere nascosto selezionando i puntini di sospensione (`...`) sulla scheda widget e quindi seleziona **[!UICONTROL Nascondi widget]**. Puoi anche visualizzare in anteprima e modificare il widget dallo stesso menu a discesa.

Per visualizzare i widget nascosti, seleziona **[!UICONTROL Mostra widget nascosti]** dall&#39;angolo in alto a destra della libreria widget.

>[!WARNING]
>
>Nascondere un widget nella libreria non rimuove il widget dai dashboard dei singoli utenti. Se un widget non deve più essere utilizzato nella tua organizzazione, assicurati di comunicarlo direttamente a tutti gli utenti di Platform in quanto dovranno rimuovere il widget dalle loro dashboard.

![La scheda Personalizzato dell’area di lavoro della libreria widget con le opzioni del menu a discesa dei widget e Mostra widget nascosti evidenziati.](../images/customization/hide-widget.png)

## Modificare un widget personalizzato

Per modificare i widget personalizzati nella libreria dei widget, seleziona i puntini di sospensione (`...`) sulla scheda widget e quindi seleziona **[!UICONTROL Modifica]** dal menu a discesa .

![Le opzioni del menu a discesa dei widget con i puntini di sospensione e Modifica evidenziate.](../images/customization/custom-widget-edit.png)

Sulla **[!UICONTROL Widget di modifica]** Puoi modificare il titolo e la descrizione del widget, nonché visualizzare in anteprima e selezionare diverse visualizzazioni. Dopo aver apportato le modifiche, seleziona **[!UICONTROL Salva]** per salvare le modifiche e tornare alla scheda widget personalizzati.

>[!WARNING]
>
>La modifica di un widget nella libreria non aggiorna il widget per i singoli utenti. Se un widget è stato aggiornato, assicurati di comunicarlo direttamente a tutti gli utenti di Platform in quanto dovranno rimuovere il widget obsoleto dalle loro dashboard, quindi selezionare e aggiungere il widget aggiornato dalla libreria dei widget.

![Finestra di dialogo Modifica widget.](../images/customization/edit-widget.png)

## Passaggi successivi

Dopo aver letto questo documento, potrai accedere alla libreria widget e utilizzarla per creare e aggiungere widget personalizzati per la tua organizzazione. Per modificare le dimensioni e la posizione dei widget visualizzati nel dashboard, fare riferimento alla [guida alla modifica delle dashboard](modify.md).
