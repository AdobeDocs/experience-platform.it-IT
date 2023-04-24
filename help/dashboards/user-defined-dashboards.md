---
title: Dashboard definiti dall'utente
description: Scopri come creare e gestire dashboard personalizzati per creare, aggiungere e modificare widget personalizzati per visualizzare le metriche chiave.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: a0be2f8625ca60f9c8f355c1230a889002436d6d
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 4%

---

# Dashboard definiti dall&#39;utente

Le dashboard di Adobe Experience Platform consentono di accelerare le informazioni e personalizzare la visualizzazione tramite la funzione dashboard definita dall’utente. Questa funzione ti consente di creare e gestire dashboard personalizzati per creare, aggiungere e modificare widget personalizzati per visualizzare le metriche chiave pertinenti per la tua organizzazione.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Creare un dashboard personalizzato

Per creare un dashboard personalizzato, prima di tutto, accedi all’inventario del dashboard. Seleziona **[!UICONTROL Dashboard]** dalla navigazione a sinistra dell’interfaccia utente di Platform, seguita da **[!UICONTROL Crea dashboard]**.

![Inventario del dashboard con dashboard nella navigazione a sinistra e &quot;Crea dashboard&quot; evidenziato.](./images/user-defined-dashboards/create-dashboard.png)

Prima di aggiungere una dashboard personalizzata, l’inventario delle dashboard è vuoto e visualizza un messaggio &quot;Nessun dashboard trovato&quot;. messaggio. Una volta create, tutte le dashboard definite dall’utente sono elencate nell’inventario del dashboard.

>[!NOTE]
>
>Per modificare un dashboard esistente, seleziona il nome del dashboard dall’elenco Inventario seguito dall’icona a forma di matita (![Icona a forma di matita.](./images/user-defined-dashboards/edit-icon.png))

La [!UICONTROL Crea dashboard] viene visualizzata la finestra di dialogo . Inserisci un nome descrittivo e descrittivo per la raccolta di widget che intendi creare e seleziona **[!UICONTROL Salva]**.

![Finestra di dialogo Crea dashboard.](./images/user-defined-dashboards/create-dashboard-dialog.png)

Il dashboard vuoto appena creato viene visualizzato con il nome scelto nell’angolo in alto a sinistra della visualizzazione.

## Creare un widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Numero massimo di widget"
>abstract="Le dashboard definite dall’utente supportano fino a dieci widget. Dopo aver aggiunto dieci widget alla dashboard, l’opzione [!UICONTROL Aggiungi nuovo widget] è disabilitata e appare grigia."

Dalla nuova vista dashboard, seleziona **[!UICONTROL Aggiungi nuovo widget]** per avviare il processo di creazione del widget.

>[!IMPORTANT]
>
>Le dashboard definite dall’utente supportano fino a dieci widget. Dopo aver aggiunto dieci widget alla dashboard, l’opzione [!UICONTROL Aggiungi nuovo widget] è disabilitata e appare grigia.

![Il nuovo dashboard vuoto con Aggiungi nuovo widget evidenziato.](./images/user-defined-dashboards/add-new-widget.png)

### Compositore esperienza visivo

Viene visualizzata l&#39;area di lavoro del compositore widget. Quindi, seleziona **[!UICONTROL Seleziona dati]** per scegliere il modello dati da cui aggiungere gli attributi ai widget.

![Area di lavoro del compositore widget.](./images/user-defined-dashboards/widget-composer.png)

#### Seleziona il modello dati {#select-data-model}

La [!UICONTROL Seleziona il modello dati] viene visualizzata la finestra di dialogo . Selezionare un modello dati dalla colonna a sinistra per visualizzare un elenco di anteprima di tutte le tabelle disponibili. Il modello dati preconfigurato per Real-time Customer Data Platform è denominato [!UICONTROL CDPInsights].

>[!TIP]
>
>Seleziona l’icona delle informazioni (![Icona di informazioni.](./images/user-defined-dashboards/info-icon.png)) per visualizzare il nome completo del modello dati, se la visualizzazione nella barra dei dati è troppo lunga.

![Finestra di dialogo Seleziona dati .](./images/user-defined-dashboards/select-data-model-dialog.png)

L’elenco di anteprima fornisce dettagli sulle tabelle contenute nel modello dati. La tabella seguente fornisce una descrizione dei campi colonna e dei relativi valori potenziali.

| Campo colonna | Descrizione |
|---|---|
| [!UICONTROL Titolo] | Nome della tabella. |
| [!UICONTROL Tipo di tabella] | Tipo di tabella. I tipi potenziali includono: `fact`, `dimension`e `none`. |
| [!UICONTROL Record] | Numero di record associati alla tabella selezionata. |
| [!UICONTROL Ricerche] | Numero di tabelle unite alla tabella selezionata. |
| [!UICONTROL Attributi] | Numero di attributi per la tabella selezionata. |

Seleziona **[!UICONTROL Successivo]** per confermare la scelta del modello dati. Nella vista successiva viene visualizzato un elenco delle tabelle disponibili nella barra a sinistra. Selezionare una tabella per visualizzare un raggruppamento completo dei dati contenuti nella tabella selezionata.

### Widget Popolamento {#populate-widget}

La [!UICONTROL Anteprima] il pannello contiene schede per [!UICONTROL Record di esempio] e [!UICONTROL Attributi]. La [!UICONTROL Record di esempio] In una vista tabulata, la scheda fornisce un sottoinsieme dei record della tabella selezionata. La [!UICONTROL Attributi] scheda fornisce il nome dell’attributo, il tipo di dati e la tabella di origine per ogni attributo associato alla tabella selezionata.

Seleziona una tabella dall’elenco disponibile nella barra a sinistra per fornire i dati del widget, quindi seleziona **[!UICONTROL Seleziona]** per tornare al compositore widget.

![Finestra di dialogo Seleziona dati con selezione evidenziata.](./images/user-defined-dashboards/select-a-table.png)

Il compositore di widget ora viene compilato con i dati della tabella selezionata.

Il modello dati e la tabella attualmente selezionata vengono visualizzati nella parte superiore della barra a sinistra e gli attributi disponibili per creare il widget sono elencati nella sezione [!UICONTROL Attributi] colonna. Puoi usare la barra di ricerca per cercare gli attributi invece di scorrere l’elenco, oppure modificare il modello dati selezionato selezionando l’icona a forma di matita (![Icona a forma di matita.](./images/user-defined-dashboards/edit-icon.png)) nella barra a sinistra.

![Un widget popolato con dati all&#39;interno del compositore di widget.](./images/user-defined-dashboards/populated-widget-composer.png)

#### Aggiungere e filtrare gli attributi {#add-and-filter-attributes}

Seleziona l’icona Aggiungi (![Icona Aggiungi.](./images/user-defined-dashboards/add-icon.png)) accanto al nome di un attributo per aggiungere un attributo al widget. Il menu a discesa visualizzato consente di aggiungere un attributo come asse X, asse Y, colore o filtro per il widget. La [!UICONTROL Colore] L’attributo ti consente di differenziare i risultati dei segni degli assi X e Y in base al colore. Lo fa suddividendo i risultati in diversi colori in base alla loro composizione di un terzo attributo.

>[!TIP]
>
>Per capovolgere la disposizione degli assi X e Y, selezionate l&#39;icona freccia su e freccia giù (![Icona freccia Su e freccia Giù.](./images/user-defined-dashboards/switch-axis-icon.png)) per cambiare la loro disposizione.

![Il compositore di widget con il menu a discesa dell&#39;icona del componente aggiuntivo evidenziato.](./images/user-defined-dashboards/attributes-dropdown.png)

Per modificare il tipo di grafico o grafico del widget, seleziona la [!UICONTROL Indicatori] e scegli tra le opzioni disponibili. Le opzioni disponibili sono barre, punti, zecche, linee o area. Una volta selezionata, viene generata una visualizzazione in anteprima delle impostazioni correnti del widget.

![Il compositore di widget con il menu a discesa Marchi evidenziato.](./images/user-defined-dashboards/marks-dropdown.png)

Aggiungendo un attributo come filtro, puoi selezionare i valori da includere o escludere dal widget. Dopo aver aggiunto un filtro dall’elenco degli attributi, il [!UICONTROL Filtro] viene visualizzata una finestra di dialogo in cui è possibile selezionare o deselezionare i valori utilizzando la relativa casella di controllo.

![Finestra di dialogo del filtro per filtrare i valori dal widget.](./images/user-defined-dashboards/filter-dialog.png)

### Proprietà dei widget

Seleziona l’icona delle proprietà (![Icona delle proprietà.](./images/user-defined-dashboards/properties-icon.png)) nella barra a destra per aprire il pannello proprietà. In [!UICONTROL Proprietà] , immetti un nome per il widget nel [!UICONTROL Titolo del widget] campo di testo.

![Il pannello delle proprietà con l’icona delle proprietà e il campo del titolo del widget evidenziati.](./images/user-defined-dashboards/properties-panel.png)

Dal pannello delle proprietà del widget, puoi modificare diversi aspetti del widget. Hai il controllo completo per modificare la posizione della legenda del widget. Per spostare la legenda, seleziona la [!UICONTROL Posizionamento della legenda] e scegli la posizione desiderata dall’elenco delle opzioni disponibili. È inoltre possibile rinominare l’etichetta associata alla legenda e l’asse X o Y immettendo un nuovo nome nel [!UICONTROL Titolo legenda] campo di testo, oppure [!UICONTROL Etichetta asse] campo di testo rispettivamente.

#### Salva il widget {#save-widget}

Il salvataggio nel compositore widget consente di salvare il widget localmente nel dashboard. Se desideri salvare il tuo lavoro e riprendere in un secondo momento, seleziona **[!UICONTROL Salva]**. Un&#39;icona di spunta sotto il nome del widget indica che il widget è stato salvato. In alternativa, quando sei soddisfatto del widget, seleziona **[!UICONTROL Salva e chiudi]** per rendere il widget disponibile a tutti gli altri utenti con accesso al dashboard. Seleziona **[!UICONTROL Annulla]** per abbandonare il lavoro e tornare al dashboard personalizzato.

![Conferma del salvataggio di un nuovo widget.](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>Seleziona l’icona delle proprietà (![Icona delle proprietà.](./images/user-defined-dashboards/properties-icon.png)) accanto al nome del dashboard per visualizzare i dettagli relativi alla creazione. Potete modificare il nome del dashboard nella finestra di dialogo visualizzata.

I widget possono essere riorganizzati e ridimensionati in questa area di lavoro. Seleziona **[!UICONTROL Salva]** per mantenere il nome del dashboard e il layout configurato.

![Dashboard definito dall&#39;utente con widget personalizzato e pulsante Salva evidenziato.](./images/user-defined-dashboards/user-defined-dashboard.png)

Per garantire che ogni query per un dashboard di Adobe Real-time Customer Data Platform insights disponga di risorse sufficienti per essere eseguita in modo efficiente, l’API tiene traccia dell’utilizzo delle risorse assegnando spazi di concorrenza a ogni query. Il sistema può elaborare fino a quattro query simultanee e quindi quattro slot di query simultanee sono disponibili in un dato momento. Le query vengono inserite in una coda basata sugli slot di concorrenza, quindi attendono in coda finché non sono disponibili slot di concorrenza sufficienti.

## Passaggi successivi e risorse aggiuntive

Leggendo questo documento, potrai comprendere meglio come creare un dashboard personalizzato e come creare, modificare e aggiornare widget personalizzati per tale dashboard.

Per scoprire le metriche e le visualizzazioni preconfigurate disponibili per [profiles](./guides/profiles.md#standard-widgets), [segmenti](./guides/segments.md#standard-widgets)e [destinazioni](./guides/destinations.md#standard-widgets) dashboard, consultare l’elenco dei widget standard nella relativa documentazione.

Per comprendere meglio le dashboard definite dall’utente in Experience Platform, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
