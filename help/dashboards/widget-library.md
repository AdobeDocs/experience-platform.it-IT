---
keywords: Experience Platform;interfaccia utente;interfaccia utente;dashboard;dashboard;profili;segmenti;destinazioni;utilizzo licenza
title: Utilizzo della libreria Widget per aggiungere e creare widget dashboard
description: 'Questa guida fornisce istruzioni dettagliate per l’aggiunta di widget standard e la creazione di widget personalizzati per la visualizzazione dei dati del dashboard in Adobe Experience Platform. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: 63f855d7dd3c3591da76a23ca8d673477378c1c3
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---

# Libreria widget {#widget-library}

Nell’interfaccia utente di Adobe Experience Platform, puoi visualizzare e interagire con i dati dell’organizzazione utilizzando più dashboard. Puoi anche aggiornare alcune di queste dashboard aggiungendo nuovi widget alla vista dashboard. Oltre ai widget standard forniti da Adobe, puoi creare widget personalizzati e condividerli all’interno della tua organizzazione.

Questa guida fornisce istruzioni dettagliate per l’aggiunta di widget standard e la creazione di widget personalizzati per personalizzare le informazioni visualizzate nei dashboard [!UICONTROL Profili], [!UICONTROL Segmenti] e [!UICONTROL Destinazioni] nell’interfaccia utente di Platform.

Per informazioni su come modificare la posizione e le dimensioni dei widget nei dashboard [!UICONTROL Profili], [!UICONTROL Destinazioni] e [!UICONTROL Segmenti], fai riferimento alla guida [modifica delle dashboard](modify.md).

>[!NOTE]
>
>I widget visualizzati nel dashboard [!UICONTROL Utilizzo licenza] non possono essere personalizzati. Per ulteriori informazioni su questo dashboard univoco, consulta la [documentazione del dashboard di utilizzo della licenza](guides/license-usage.md).

## Accedere alla libreria dei widget

Da qualsiasi dashboard (ad esempio, il dashboard Profili), è possibile selezionare **[!UICONTROL Modifica dashboard]** seguito da **[!UICONTROL Libreria widget]** per accedere alla libreria dei widget.

>[!NOTE]
>
>Il pulsante [!UICONTROL Libreria widget] viene visualizzato solo una volta selezionato [!UICONTROL Modifica dashboard].

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

## Visualizza la libreria widget

La [!UICONTROL Libreria widget] contiene due schede, [!UICONTROL Standard] e [!UICONTROL Personalizzato].

* La scheda **[!UICONTROL Standard]** contiene i widget creati da Adobe e consente di aggiornare il dashboard utilizzando queste metriche standard. Per ulteriori informazioni sull’aggiunta di widget standard al dashboard, consulta la sezione [widget standard](#standard-widgets) in questa guida.
* La scheda **[!UICONTROL Personalizzato]** ti consente di creare e condividere widget all’interno della tua organizzazione. Per i passaggi completi per la creazione di widget personalizzati, fai riferimento alla sezione [widget personalizzati](#custom-widgets) in questa guida.

![](images/customization/widget-library.png)

## Widget standard {#standard-widgets}

La scheda **[!UICONTROL Standard]** contiene i widget creati da Adobe, suddivisi in categorie in base alle dashboard disponibili. La categoria selezionata corrisponde al dashboard da cui è stata immessa la libreria dei widget. In altre parole, se hai selezionato la libreria dei widget dal dashboard [!UICONTROL Profili], la categoria [!UICONTROL Profili] viene selezionata e le altre categorie vengono visualizzate in grigio.

Vengono visualizzati i widget disponibili per la categoria selezionata. Ogni widget viene visualizzato come una scheda, con titolo, descrizione e una visualizzazione di esempio della metrica.

>[!NOTE]
>
>I widget possono essere aggiunti solo al dashboard che corrisponde alla categoria selezionata. Ad esempio, solo i widget della categoria [!UICONTROL Profili] possono essere aggiunti al dashboard [!UICONTROL Profili].

![](images/customization/standard-widgets.png)

### Aggiungi widget standard al dashboard

Per scegliere un widget standard da aggiungere al dashboard, evidenzia il widget e seleziona la casella di controllo del widget. Con almeno un widget selezionato, il pulsante **[!UICONTROL Aggiungi widget]** è illuminato.

>[!NOTE]
>
>Il contatore nell’angolo in alto a destra della libreria widget mostra il numero totale di widget selezionati.

Seleziona **[!UICONTROL Aggiungi widget]** per aggiungere i widget selezionati al dashboard.

![](images/customization/add-widget.png)

## Widget personalizzati {#custom-widgets}

Per personalizzare ulteriormente l’aspetto delle dashboard all’interno di Experience Platform, puoi creare widget e condividerli con altri utenti dell’organizzazione.

>[!IMPORTANT]
>
>La tua organizzazione può creare un massimo di 20 widget personalizzati nella libreria dei widget.

Dalla libreria dei widget, seleziona la scheda **[!UICONTROL Personalizzato]** per iniziare a creare widget personalizzati o per visualizzare widget personalizzati già creati dalla tua organizzazione.

![](images/customization/custom-widgets.png)

### Modifica schema

Per creare widget personalizzati, è necessario identificare gli attributi Profilo cliente in tempo reale per garantire che i dati siano inclusi come parte dello snapshot giornaliero. Se la tua organizzazione non ha selezionato alcun attributo Profilo, il pulsante [!UICONTROL Configura schema] viene visualizzato nell&#39;angolo in alto a destra della libreria dei widget.

Quando è stato selezionato almeno un attributo personalizzato, il pulsante [!UICONTROL Modifica schema] viene visualizzato nell&#39;angolo in alto a destra della libreria dei widget. Seleziona **[!UICONTROL Modifica schema]** per aprire la finestra di dialogo **[!UICONTROL Seleziona campo schema unione]** per visualizzare gli attributi selezionati e aggiungere altri attributi.

>[!IMPORTANT]
>
>Un&#39;organizzazione può selezionare un massimo di 20 attributi.

![](images/customization/edit-schema.png)

Per selezionare un attributo, accedi all&#39;attributo nello schema dell&#39;unione (o utilizza la ricerca) e seleziona la casella di controllo accanto all&#39;attributo. Selezionando la casella di controllo, l&#39;attributo viene aggiunto anche all&#39;elenco **[!UICONTROL Attributi selezionati]** sul lato destro della finestra di dialogo.

>[!NOTE]
>
>Affinché un attributo sia visibile per la selezione, deve essere uno dei seguenti: Stringa, data, data-ora, booleano, breve, lungo, intero o byte. I tipi di dati Mappa e Doppio non sono supportati e sono disattivati in modo che non possano essere selezionati.

Dopo aver selezionato gli attributi che si desidera aggiungere, selezionare **[!UICONTROL Salva]** per salvare gli attributi e tornare alla scheda widget personalizzati.

Gli attributi appena selezionati sono disponibili dopo lo snapshot giornaliero quando i dati vengono aggiornati.

![](images/customization/select-attribute.png)

### Creare un widget personalizzato

Per creare un widget personalizzato, seleziona **[!UICONTROL Crea]** dal centro della libreria dei widget oppure, se i widget personalizzati sono già stati creati, seleziona **[!UICONTROL Crea widget]** dall&#39;angolo in alto a destra della libreria dei widget.

![](images/customization/create-widget.png)

Nella finestra di dialogo **[!UICONTROL Crea widget]**, puoi fornire un titolo e una descrizione per il nuovo widget e scegliere l&#39;attributo che desideri visualizzare. Per scegliere un attributo, selezionare il pulsante di scelta accanto all&#39;attributo che si desidera aggiungere.

>[!NOTE]
>
>È possibile selezionare un solo attributo per widget. Inoltre, se un widget è già stato creato per un attributo, questo viene visualizzato in grigio.

![](images/customization/create-widget-dialog.png)

Nella finestra di dialogo viene visualizzata un&#39;anteprima del nuovo widget, che mostra un grafico a barre orizzontale con dati simmetrici.

>[!NOTE]
>
>L’unica metrica attualmente supportata per tutti gli attributi è il conteggio dei profili e l’unica visualizzazione attualmente supportata per i widget personalizzati è un grafico a barre orizzontale.
>
>I dati mostrati nel widget di esempio sono solo a scopo illustrativo. L’anteprima non visualizza i dati effettivi provenienti dall’organizzazione.

![](images/customization/create-widget-select-attribute.png)

Per salvare il nuovo widget e tornare alla scheda [!UICONTROL Personalizzato], seleziona **[!UICONTROL Crea]**. Il nuovo widget è ora disponibile per essere aggiunto a un dashboard scegliendo il widget dalla libreria e selezionando **[!UICONTROL Aggiungi widget]**.

### Archiviare un widget personalizzato

Dopo aver aggiunto un widget alla libreria, può essere archiviato utilizzando il pulsante **[!UICONTROL Archivia]** . Puoi anche modificare il widget per aggiornare i campi titolo o descrizione.

## Passaggi successivi

Dopo aver letto questo documento, ora puoi accedere alla [!UICONTROL Libreria widget] e utilizzarla per aggiungere widget a un dashboard o creare widget personalizzati per la tua organizzazione. Per modificare le dimensioni e la posizione dei widget nel dashboard, fare riferimento alla [guida alla modifica delle dashboard](modify.md).
