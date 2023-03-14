---
title: Dashboard definiti dall'utente
description: Scopri come creare e gestire dashboard personalizzate che consentono di creare, aggiungere e modificare widget personalizzati per visualizzare le metriche chiave.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Dashboard definiti dall&#39;utente

Le dashboard di Adobe Experience Platform consentono di velocizzare le informazioni e personalizzare la visualizzazione tramite la funzione delle dashboard definite dall’utente. Questa funzione ti consente di creare e gestire dashboard personalizzate in cui creare, aggiungere e modificare widget personalizzati per visualizzare metriche chiave rilevanti per la tua organizzazione.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Creare dashboard personalizzati

Per creare un dashboard personalizzato, passa innanzitutto all’inventario del dashboard. Seleziona **[!UICONTROL Dashboard]** dalla barra di navigazione a sinistra dell’interfaccia utente di Platform, seguita da **[!UICONTROL Crea dashboard]**.

![Inventario delle dashboard con le dashboard nella barra di navigazione a sinistra ed evidenziata l’opzione &quot;Crea dashboard&quot;.](./images/user-defined-dashboards/create-dashboard.png)

Prima di aggiungere un dashboard personalizzato, l’inventario dei dashboard è vuoto e viene visualizzato il messaggio &quot;Nessun dashboard trovato&quot;. messaggio. Una volta creati, tutti i dashboard definiti dall’utente sono elencati nell’inventario dei dashboard.

Il [!UICONTROL Crea dashboard] viene visualizzata. Immettete un nome descrittivo per la raccolta di widget che intendete creare e selezionate **[!UICONTROL Salva]**.

![Finestra di dialogo Crea dashboard.](./images/user-defined-dashboards/create-dashboard-dialog.png)

La nuova dashboard vuota creata viene visualizzata con il nome scelto nell&#39;angolo superiore sinistro della visualizzazione.

## Creare un widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Numero massimo di widget"
>abstract="I dashboard definiti dall&#39;utente supportano fino a dieci widget. Dopo aver aggiunto dieci widget alla dashboard, il [!UICONTROL Aggiungi nuovo widget] è disattivata e appare grigia."

Dalla nuova vista del dashboard, seleziona **[!UICONTROL Aggiungi nuovo widget]** per avviare il processo di creazione del widget.

>[!IMPORTANT]
>
>I dashboard definiti dall&#39;utente supportano fino a dieci widget. Dopo aver aggiunto dieci widget alla dashboard, il [!UICONTROL Aggiungi nuovo widget] è disattivata e appare grigia.

![Il nuovo dashboard vuoto con Aggiungi nuovo widget evidenziato.](./images/user-defined-dashboards/add-new-widget.png)

### Compositore widget

Viene visualizzata l&#39;area di lavoro del compositore widget. Quindi, seleziona **[!UICONTROL Seleziona dati]** per scegliere il modello dati da cui aggiungere attributi ai widget.

![Area di lavoro del compositore widget.](./images/user-defined-dashboards/widget-composer.png)

Il [!UICONTROL Seleziona dati] viene visualizzata. Seleziona un modello dati dalla colonna a sinistra per visualizzare un elenco di anteprima di tutte le tabelle disponibili.

>[!NOTE]
>
>Le dashboard definite dall’utente attualmente supportano solo il modello dati del profilo. Saranno supportate altre opzioni.

![La finestra di dialogo Seleziona dati.](./images/user-defined-dashboards/select-data-dialog.png)

L’elenco di anteprima fornisce dettagli sulle tabelle contenute nel modello dati. La tabella seguente fornisce le descrizioni dei campi colonna e dei relativi valori potenziali.

| Campo colonna | Descrizione |
|---|---|
| [!UICONTROL Titolo] | Nome della tabella. |
| [!UICONTROL Tipo di tabella] | Tipo di tabella. I tipi potenziali includono: `fact`, `dimension`, e `none`. |
| [!UICONTROL Ricerche] | Numero di tabelle unite alla tabella selezionata. |

Seleziona **[!UICONTROL Successivo]** per confermare la scelta del modello dati. Nella vista successiva viene visualizzato un elenco delle tabelle disponibili nella barra a sinistra. Seleziona una tabella per visualizzare una suddivisione completa dei dati contenuti nella tabella selezionata.

Il [!UICONTROL Anteprima] il pannello contiene schede per [!UICONTROL Record di esempio] e [!UICONTROL Attributi]. Il [!UICONTROL Record di esempio] fornisce un sottoinsieme dei record della tabella selezionata in una vista a tabella. Il [!UICONTROL Attributi] fornisce il nome attributo, il tipo di dati e la tabella di origine per ogni attributo associato alla tabella selezionata.

Seleziona una tabella dall’elenco disponibile nella barra a sinistra per fornire i dati per il widget e seleziona **[!UICONTROL Seleziona]** per tornare al compositore widget.

![La finestra di dialogo Seleziona dati con seleziona evidenziato.](./images/user-defined-dashboards/select-a-table.png)

Il compositore widget ora è compilato con i dati della tabella scelta.

Il modello dati e la tabella attualmente selezionata vengono visualizzati nella parte superiore della barra a sinistra e gli attributi disponibili per creare il widget sono elencati nella colonna degli attributi.

![Un widget popolato con dati all&#39;interno del compositore widget.](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>Puoi modificare il modello di dati scelto selezionando l’icona a forma di matita (![Icona della matita.](./images/user-defined-dashboards/edit-icon.png)) nella barra a sinistra.

Seleziona l’icona Aggiungi (./images/user-defined-dashboards/add-icon.png) accanto al nome di un attributo per aggiungere un attributo all&#39;asse X o Y.

![Il compositore widget con l&#39;icona Aggiungi evidenziata a discesa per aggiungere attributi a un asse widget.](./images/user-defined-dashboards/attributes-dropdown.png)

Quindi, seleziona il tipo di grafico o grafico dall’ [!UICONTROL Indicatori] per generare una visualizzazione di anteprima delle impostazioni correnti del widget. In [!UICONTROL Proprietà] nella parte destra dello schermo, immetti un nome per il widget nella [!UICONTROL Titolo widget] campo di testo.

![Il compositore widget con il menu a discesa Contrassegni e il campo di testo del titolo del widget evidenziato.](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

Quando si è soddisfatti del widget, selezionare **[!UICONTROL Salva]**. Un&#39;icona di spunta sotto il nome del widget indica che il widget è stato salvato.

>[!NOTE]
>
>Se si salva nel compositore widget, il widget viene salvato localmente nel dashboard. Se esci dall’editor del dashboard senza salvare il dashboard, il widget non viene salvato nel dashboard.

![Conferma del salvataggio del nuovo widget.](./images/user-defined-dashboards/save-confirmation.png)

Seleziona **[!UICONTROL Annulla]** per tornare alla dashboard personalizzata.

![Il compositore di widget con un widget di esempio creato.](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>Seleziona l’icona dell’impostazione accanto al nome del dashboard per visualizzare i dettagli sulla sua creazione. Puoi modificare il nome del dashboard nella finestra di dialogo visualizzata.

I widget possono essere ridisposti e ridimensionati mentre si trovano in questa area di lavoro. Seleziona **[!UICONTROL Salva]** per mantenere il nome del dashboard e il layout configurato.

![Dashboard definita dall&#39;utente con widget personalizzato ed evidenziato il pulsante Salva.](./images/user-defined-dashboards/user-defined-dashboard.png)

Per garantire che ogni query per un dashboard di approfondimenti di Adobe Real-time Customer Data Platform disponga di risorse sufficienti per essere eseguita in modo efficiente, l’API tiene traccia dell’utilizzo delle risorse assegnando slot di concorrenza a ogni query. Il sistema può elaborare fino a quattro query simultanee, pertanto sono disponibili quattro slot di query simultanee in un dato momento. Le query vengono inserite in una coda in base agli slot di concorrenza, quindi attendi nella coda fino a quando non sono disponibili abbastanza slot di concorrenza.

## Passaggi successivi e risorse aggiuntive

La lettura di questo documento consente di comprendere meglio come creare un dashboard personalizzato e come creare, modificare e aggiornare i widget personalizzati per tale dashboard.

Per scoprire le metriche e le visualizzazioni preconfigurate disponibili per [profili](./guides/profiles.md#standard-widgets), [segmenti](./guides/segments.md#standard-widgets), e [destinazioni](./guides/destinations.md#standard-widgets) dashboard, consulta l’elenco dei widget standard nella rispettiva documentazione.

Per comprendere meglio le dashboard definite dall’utente in questo Experience Platform, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
