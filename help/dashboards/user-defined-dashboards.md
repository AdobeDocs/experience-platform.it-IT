---
title: Dashboard definiti dall'utente
description: Scopri come creare e gestire dashboard personalizzati per creare, aggiungere e modificare widget personalizzati per visualizzare le metriche chiave.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: 2c96bfd2c1b541d30a72fcf2bac414ee06607456
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---

# Dashboard definiti dall&#39;utente

Le dashboard di Adobe Experience Platform consentono di accelerare le informazioni e personalizzare la visualizzazione tramite la funzione dashboard definita dall’utente. Questa funzione ti consente di creare e gestire dashboard personalizzati per creare, aggiungere e modificare widget personalizzati per visualizzare le metriche chiave pertinenti per la tua organizzazione.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Creare dashboard personalizzati

Per creare un dashboard personalizzato, prima di tutto, accedi all’inventario del dashboard. Seleziona **[!UICONTROL Dashboard]** dalla navigazione a sinistra dell’interfaccia utente di Platform, seguita da **[!UICONTROL Crea dashboard]**.

![Inventario del dashboard con dashboard nella navigazione a sinistra e &quot;Crea dashboard&quot; evidenziato.](./images/user-defined-dashboards/create-dashboard.png)

Prima di aggiungere una dashboard personalizzata, l’inventario delle dashboard è vuoto e visualizza un messaggio &quot;Nessun dashboard trovato&quot;. messaggio. Una volta create, tutte le dashboard definite dall’utente sono elencate nell’inventario del dashboard.

La [!UICONTROL Crea dashboard] viene visualizzata la finestra di dialogo . Inserisci un nome descrittivo e descrittivo per la raccolta di widget che intendi creare e seleziona **[!UICONTROL Salva]**.

![Finestra di dialogo Crea dashboard.](./images/user-defined-dashboards/create-dashboard-dialog.png)

Il dashboard vuoto appena creato viene visualizzato con il nome scelto nell’angolo in alto a sinistra della visualizzazione.

## Creare un widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Numero massimo di widget"
>abstract="Le dashboard definite dall&#39;utente supportano fino a dieci widget. Dopo aver aggiunto dieci widget al dashboard, [!UICONTROL Aggiungi nuovo widget] è disabilitata e appare grigia."

Dalla nuova vista dashboard, seleziona **[!UICONTROL Aggiungi nuovo widget]** per avviare il processo di creazione del widget.

>[!IMPORTANT]
>
>Le dashboard definite dall&#39;utente supportano fino a dieci widget. Dopo aver aggiunto dieci widget al dashboard, [!UICONTROL Aggiungi nuovo widget] è disabilitata e appare grigia.

![Il nuovo dashboard vuoto con Aggiungi nuovo widget evidenziato.](./images/user-defined-dashboards/add-new-widget.png)

### Compositore esperienza visivo

Viene visualizzata l&#39;area di lavoro del compositore widget. Quindi, seleziona **[!UICONTROL Seleziona dati]** per scegliere il modello dati da cui aggiungere gli attributi ai widget.

![Area di lavoro del compositore widget.](./images/user-defined-dashboards/widget-composer.png)

La [!UICONTROL Seleziona dati] viene visualizzata la finestra di dialogo . Selezionare un modello dati dalla colonna a sinistra per visualizzare un elenco di anteprima di tutte le tabelle disponibili.

>[!NOTE]
>
>Le dashboard definite dall&#39;utente supportano attualmente solo il modello dati di profilo. Saranno supportate più opzioni.

![Finestra di dialogo Seleziona dati .](./images/user-defined-dashboards/select-data-dialog.png)

L’elenco di anteprima fornisce dettagli sulle tabelle contenute nel modello dati. La tabella seguente fornisce una descrizione dei campi colonna e dei relativi valori potenziali.

| Campo colonna | Descrizione |
|---|---|
| [!UICONTROL Titolo] | Nome della tabella. |
| [!UICONTROL Tipo di tabella] | Tipo di tabella. I tipi potenziali includono: `fact`, `dimension`e `none`. |
| [!UICONTROL Ricerche] | Numero di tabelle unite alla tabella selezionata. |

Seleziona **[!UICONTROL Successivo]** per confermare la scelta del modello dati. Nella vista successiva viene visualizzato un elenco delle tabelle disponibili nella barra a sinistra. Selezionare una tabella per visualizzare un raggruppamento completo dei dati contenuti nella tabella selezionata.

La [!UICONTROL Anteprima] il pannello contiene schede per [!UICONTROL Record di esempio] e [!UICONTROL Attributi]. La [!UICONTROL Record di esempio] In una vista tabulata, la scheda fornisce un sottoinsieme dei record della tabella selezionata. La [!UICONTROL Attributi] scheda fornisce il nome dell’attributo, il tipo di dati e la tabella di origine per ogni attributo associato alla tabella selezionata.

Seleziona una tabella dall’elenco disponibile nella barra a sinistra per fornire i dati del widget e seleziona **[!UICONTROL Seleziona]** per tornare al compositore widget.

![Finestra di dialogo Seleziona dati con selezione evidenziata.](./images/user-defined-dashboards/select-a-table.png)

Il compositore di widget ora viene compilato con i dati della tabella selezionata.

Il modello dati e la tabella attualmente selezionata vengono visualizzati nella parte superiore della barra a sinistra e gli attributi disponibili per la creazione del widget sono elencati nella colonna attributi.

![Un widget popolato con dati all&#39;interno del compositore di widget.](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>Per modificare il modello dati selezionato, seleziona l’icona a forma di matita (![Icona a forma di matita.](./images/user-defined-dashboards/edit-icon.png)) nella barra a sinistra.

Seleziona l’icona Aggiungi (./images/user-defined-dashboards/add-icon.png) accanto al nome di un attributo per aggiungere un attributo all&#39;asse X o Y.

![Il compositore di widget con il menu a discesa Aggiungi icona evidenziato per aggiungere attributi a un asse di widget.](./images/user-defined-dashboards/attributes-dropdown.png)

Quindi, seleziona il tipo di grafico o grafico dal [!UICONTROL Indicatori] menu a discesa per generare una visualizzazione di anteprima delle impostazioni correnti del widget. In [!UICONTROL Proprietà] nella barra a destra dello schermo, immetti un nome per il widget nel [!UICONTROL Titolo del widget] campo di testo.

![Il compositore di widget con il campo di testo del titolo del widget e del menu a discesa Marchi evidenziati.](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

Quando sei soddisfatto del widget seleziona **[!UICONTROL Salva]**. Un&#39;icona di spunta sotto il nome del widget indica che il widget è stato salvato.

>[!NOTE]
>
>Il salvataggio nel compositore widget consente di salvare il widget localmente nel dashboard. Se esci dall’editor del dashboard senza salvare il dashboard, il widget non verrà salvato nel dashboard.

![Conferma del salvataggio di un nuovo widget.](./images/user-defined-dashboards/save-confirmation.png)

Seleziona **[!UICONTROL Annulla]** per tornare al dashboard personalizzato.

![Il compositore di widget con un widget di esempio creato.](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>Seleziona l’icona di impostazione accanto al nome del dashboard per visualizzare i dettagli relativi alla creazione. Potete modificare il nome del dashboard nella finestra di dialogo visualizzata.

I widget possono essere riorganizzati e ridimensionati in questa area di lavoro. Seleziona **[!UICONTROL Salva]** per mantenere il nome del dashboard e il layout configurato.

![Dashboard definito dall&#39;utente con widget personalizzato e pulsante Salva evidenziato.](./images/user-defined-dashboards/user-defined-dashboard.png)

## Passaggi successivi

Leggendo questo documento è possibile comprendere meglio come creare un dashboard personalizzato e come creare, modificare e aggiornare widget personalizzati per tale dashboard.

Per scoprire le metriche e le visualizzazioni preconfigurate disponibili per [profiles](./guides/profiles.md#standard-widgets), [segmenti](./guides/segments.md#standard-widgets)e [destinazioni](./guides/destinations.md#standard-widgets) dashboard, consultare l’elenco dei widget standard nella relativa documentazione.
