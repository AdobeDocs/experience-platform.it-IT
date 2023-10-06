---
title: Sfoglia ordini di lavoro del ciclo di vita dei dati
description: Scopri come visualizzare e gestire gli ordini di lavoro del ciclo di vita dei dati esistenti nell’interfaccia utente di Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 14%

---

# Sfoglia ordini di lavoro del ciclo di vita dei dati {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="ID degli ordini di lavoro"
>abstract="Quando una richiesta del ciclo di vita dei dati viene inviata al sistema, viene creato un ordine di lavoro per eseguire l&#39;attività richiesta. In altre parole, un ordine di lavoro rappresenta un processo specifico del ciclo di vita dei dati, che include lo stato corrente e altri dettagli correlati. Al momento della creazione di ogni ordine di lavoro, gli viene assegnato automaticamente un ID univoco."
>text="See the data lifecycle UI guide to learn more."

Quando una richiesta del ciclo di vita dei dati viene inviata al sistema, viene creato un ordine di lavoro per eseguire l&#39;attività richiesta. Un ordine di lavoro rappresenta un processo specifico del ciclo di vita dei dati, ad esempio una scadenza pianificata del set di dati, che include lo stato corrente e altri dettagli correlati.

Questa guida illustra come visualizzare e gestire gli ordini di lavoro esistenti nell’interfaccia utente di Adobe Experience Platform.

## Elenca e filtra gli ordini di lavoro esistenti

La prima volta che accedi a **[!UICONTROL Ciclo di vita dei dati]** nell’interfaccia utente di, viene visualizzato un elenco degli ordini di lavoro esistenti con i relativi dettagli di base.

![Immagine che mostra [!UICONTROL Ciclo di vita dei dati] Workspace nell’interfaccia utente di Platform](../images/ui/browse/work-order-list.png)

Nell&#39;elenco vengono visualizzati solo gli ordini di lavorazione per una categoria alla volta. Seleziona **[!UICONTROL Consumatore]** per visualizzare un elenco di attività di eliminazione record e **[!UICONTROL Set di dati]** per visualizzare un elenco delle scadenze pianificate dei set di dati.

![Immagine che mostra [!UICONTROL Set di dati] scheda](../images/ui/browse/dataset-tab.png)

Seleziona l’icona funnel (![Immagine dell’icona funnel](../images/ui/browse/funnel-icon.png)) per visualizzare un elenco di filtri per gli ordini di lavoro visualizzati.

![Immagine dei filtri ordine di lavoro visualizzati](../images/ui/browse/filters.png)

A seconda del tipo di ordine di lavoro visualizzato, sono disponibili opzioni di filtro diverse.

### Filtri per eliminazioni record

I seguenti filtri si applicano alle richieste di cancellazione dei record:

| Filtro | Descrizione |
| --- | --- |
| [!UICONTROL Stato] | Filtra in base allo stato corrente dell&#39;ordine di lavorazione:<ul><li>**[!UICONTROL Completato]**: processo completato.</li><li>**[!UICONTROL Non riuscito]**: il processo ha rilevato un errore e non è stato completato.</li><li>**[!UICONTROL Elaborazione]**: la richiesta è iniziata ed è in fase di elaborazione.</li></ul> |
| [!UICONTROL Data di creazione] | Filtra in base al momento in cui è stato effettuato l’ordine di lavoro. |
| [!UICONTROL Data aggiornamento] | Filtra in base al momento dell&#39;ultimo aggiornamento dell&#39;ordine di lavoro. Le creazioni vengono conteggiate come aggiornamenti. |

### Filtri per le scadenze dei set di dati

I seguenti filtri si applicano alle richieste di scadenza dei set di dati:

| Filtro | Descrizione |
| --- | --- |
| [!UICONTROL Stato] | Filtra in base allo stato corrente dell&#39;ordine di lavorazione:<ul><li>**[!UICONTROL Completato]**: processo completato.</li><li>**[!UICONTROL In sospeso]**: il processo è stato creato ma non è ancora stato eseguito. A [richiesta di scadenza del set di dati](./dataset-expiration.md) assume questo stato prima della data di eliminazione pianificata. Una volta arrivata la data di eliminazione, lo stato si aggiorna a [!UICONTROL In esecuzione] a meno che il processo non venga annullato in precedenza.</li><li>**[!UICONTROL In esecuzione]**: la richiesta di scadenza del set di dati è iniziata e è attualmente in elaborazione.</li><li>**[!UICONTROL Annullato]**: il processo è stato annullato come parte di una richiesta manuale dell’utente.</li></ul> |
| [!UICONTROL Data di creazione] | Filtra in base al momento in cui è stato effettuato l’ordine di lavoro. |
| [!UICONTROL Data di scadenza] | Filtra le richieste di scadenza dei set di dati in base alla data di eliminazione pianificata per il set di dati in questione. |
| [!UICONTROL Data aggiornamento] | Filtra in base al momento dell&#39;ultimo aggiornamento dell&#39;ordine di lavoro. Le creazioni e le scadenze vengono conteggiate come aggiornamenti. |

{style="table-layout:auto"}

## Visualizzare i dettagli di un ordine di lavoro {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Stato per servizio"
>abstract="Le richieste del ciclo di vita dei dati vengono elaborate in modo indipendente da più servizi Experienci Platform. Questa sezione riassume lo stato di elaborazione attuale della richiesta per ciascun servizio. Per ulteriori informazioni, consulta la guida Data Lifecycle UI."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Numero di identità"
>abstract="Numero di identità per i cui record è stato richiesto l’aggiornamento o l’eliminazione nell’ambito di questo ordine di lavoro. Le identità incluse nel conteggio potrebbero non esistere necessariamente nei set di dati interessati. Per ulteriori informazioni, consulta la guida Data Lifecycle UI."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Risposta per eliminazione dei record"
>abstract="Quando un processo di eliminazione di record riceve una risposta dal sistema, questi messaggi vengono visualizzati nella sezione **[!UICONTROL Risultato]**. Se si verifica un problema durante l’elaborazione di un ordine di lavoro, tutti i messaggi di errore pertinenti vengono visualizzati in questa sezione per aiutarti a risolvere il problema. Per ulteriori informazioni, consulta la guida Data Lifecycle UI."

Selezionare l&#39;ID di un ordine di lavoro elencato per visualizzarne i dettagli.

![Immagine che mostra un ID ordine di lavoro selezionato](../images/ui/browse/select-work-order.png)

A seconda del tipo di ordine di lavoro selezionato, vengono fornite informazioni e controlli diversi. Questi sono trattati nelle sezioni seguenti.

### Dettagli eliminazione record {#record-delete}

I dettagli di una richiesta di cancellazione del record includono lo stato corrente e il tempo trascorso dall&#39;invio della richiesta. Ogni richiesta include anche un **[!UICONTROL Stato per servizio]** sezione che fornisce dettagli sullo stato di ciascun servizio a valle coinvolto nell’eliminazione. Nella barra a destra è possibile utilizzare i controlli per aggiornare il nome e la descrizione dell&#39;ordine di lavoro.

![Immagine che mostra la pagina dei dettagli di un ordine di lavoro di eliminazione record](../images/ui/browse/record-delete-details.png)

### Dettagli scadenza set di dati {#dataset-expiration}

La pagina dei dettagli per la scadenza di un set di dati fornisce informazioni sui relativi attributi di base, inclusa la data di scadenza pianificata nei giorni rimanenti prima che si verifichi l’eliminazione. Nella barra a destra, puoi utilizzare i controlli per modificare o annullare la scadenza.

![Immagine che mostra la pagina dei dettagli per un ordine di lavoro di scadenza del set di dati](../images/ui/browse/ttl-details.png)

## Passaggi successivi

Questa guida illustra come visualizzare e gestire gli ordini di lavoro esistenti relativi al ciclo di vita dei dati nell’interfaccia utente di Platform. Per informazioni sulla creazione di ordini di lavoro personalizzati, consultare la seguente documentazione:

* [Gestire le scadenze dei set di dati](./dataset-expiration.md)
* [Gestisci eliminazioni record](./record-delete.md)
