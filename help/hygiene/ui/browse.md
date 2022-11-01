---
title: Cerca ordini di lavoro di igiene dati
description: Scopri come visualizzare e gestire gli ordini di lavoro esistenti in materia di igiene dei dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 6453ec6c98d90566449edaa0804ada260ae12bf6
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 1%

---

# Sfoglia gli ordini di lavoro per l&#39;igiene dei dati {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="ID ordine di lavoro"
>abstract="Quando una richiesta di igiene dati viene inviata al sistema, viene creato un ordine di lavoro per eseguire l&#39;attività richiesta. In altre parole, un ordine di lavoro rappresenta un processo specifico di igiene dei dati, che include il suo stato attuale e altri dettagli correlati. A ogni ordine di lavoro viene assegnato automaticamente il proprio ID univoco al momento della creazione."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato **Scudo sanitario Adobe** o **Adobe Privacy e sicurezza scudo**.

Quando una richiesta di igiene dati viene inviata al sistema, viene creato un ordine di lavoro per eseguire l&#39;attività richiesta. Un ordine di lavoro rappresenta un processo specifico di igiene dei dati, ad esempio una scadenza pianificata del set di dati, che include il suo stato corrente e altri dettagli correlati.

Questa guida illustra come visualizzare e gestire gli ordini di lavoro esistenti nell’interfaccia utente di Adobe Experience Platform.

## Elencare e filtrare gli ordini di lavoro esistenti

Quando accedi per la prima volta al **[!UICONTROL Igiene dei dati]** nell’interfaccia utente viene visualizzato un elenco degli ordini di lavoro esistenti con i relativi dettagli di base.

![Immagine che mostra [!UICONTROL Igiene dei dati] Area di lavoro nell’interfaccia utente di Platform](../images/ui/browse/work-order-list.png)

L&#39;elenco mostra solo gli ordini di lavoro per una categoria alla volta. Seleziona **[!UICONTROL Consumatore]** per visualizzare un elenco delle attività di eliminazione dei consumatori e **[!UICONTROL Set di dati]** per visualizzare un elenco delle scadenze pianificate dei set di dati.

![Immagine che mostra [!UICONTROL Set di dati] scheda](../images/ui/browse/dataset-tab.png)

Seleziona l’icona funnel (![Immagine dell’icona funnel](../images/ui/browse/funnel-icon.png)) per visualizzare un elenco di filtri per gli ordini di lavoro visualizzati.

![Immagine dei filtri dell&#39;ordine di lavoro visualizzati](../images/ui/browse/filters.png)

A seconda del tipo di ordine di lavoro visualizzato, sono disponibili diverse opzioni di filtro.

### Filtri per le cancellazioni dei consumatori

I seguenti filtri si applicano alle richieste di cancellazione del consumatore:

| Filtro | Descrizione |
| --- | --- |
| [!UICONTROL Stato] | Filtra in base allo stato corrente dell&#39;ordine di lavoro:<ul><li>**[!UICONTROL Completato]**: Il processo è stato completato.</li><li>**[!UICONTROL Non riuscito]**: Errore del processo. Impossibile completare il processo.</li><li>**[!UICONTROL Elaborazione]**: La richiesta è stata avviata ed è in corso l’elaborazione.</li></ul> |
| [!UICONTROL Data di creazione] | Filtra in base al momento in cui è stato effettuato l’ordine di lavoro. |
| [!UICONTROL Data di aggiornamento] | Filtra in base alla data dell’ultimo aggiornamento dell’ordine di lavoro. Le creazioni vengono conteggiate come aggiornamenti. |

### Filtri per le scadenze dei set di dati

I seguenti filtri si applicano alle richieste di scadenza dei set di dati:

| Filtro | Descrizione |
| --- | --- |
| [!UICONTROL Stato] | Filtra in base allo stato corrente dell&#39;ordine di lavoro:<ul><li>**[!UICONTROL Completato]**: Il processo è stato completato.</li><li>**[!UICONTROL In sospeso]**: Il processo è stato creato ma non è ancora stato eseguito. A [richiesta di scadenza del set di dati](./dataset-expiration.md) assume questo stato prima della data di eliminazione pianificata. Una volta che la data di eliminazione arriva, lo stato si aggiorna a [!UICONTROL In esecuzione] a meno che il lavoro non venga annullato in anticipo.</li><li>**[!UICONTROL In esecuzione]**: La richiesta di scadenza del set di dati è iniziata ed è in corso di elaborazione.</li><li>**[!UICONTROL Annullato]**: Il processo è stato annullato come parte di una richiesta utente manuale.</li></ul> |
| [!UICONTROL Data di creazione] | Filtra in base al momento in cui è stato effettuato l’ordine di lavoro. |
| [!UICONTROL Data di scadenza] | Filtra le richieste di scadenza dei set di dati in base alla data di eliminazione pianificata per il set di dati in questione. |
| [!UICONTROL Data di aggiornamento] | Filtra in base alla data dell’ultimo aggiornamento dell’ordine di lavoro. Le creazioni e le scadenze vengono conteggiate come aggiornamenti. |

{style=&quot;table-layout:auto&quot;}

## Visualizza i dettagli di un ordine di lavorazione {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Stato per servizio"
>abstract="Le richieste di igiene dei dati vengono elaborate in modo indipendente da più servizi di Experience Platform. In questa sezione viene illustrato lo stato di elaborazione corrente della richiesta per ciascun servizio. Per ulteriori informazioni, consulta la guida all’interfaccia utente per l’igiene dei dati ."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Numero di identità"
>abstract="Numero di identità richieste per l&#39;eliminazione nell&#39;ambito di questo ordine di lavoro. Le identità incluse nel conteggio potrebbero non esistere necessariamente nei set di dati interessati. Per ulteriori informazioni, consulta la guida all’interfaccia utente per l’igiene dei dati ."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Risposta di cancellazione del consumatore"
>abstract="Quando un processo di eliminazione del consumatore riceve una risposta dal sistema, questi messaggi vengono visualizzati sotto il **[!UICONTROL Risultato]** sezione . Se si verifica un problema durante l&#39;elaborazione di un ordine di lavoro, tutti i messaggi di errore pertinenti verranno visualizzati in questa sezione per aiutarti a risolvere il problema. Per ulteriori informazioni, consulta la guida all’interfaccia utente per l’igiene dei dati ."

Selezionare l&#39;ID di un ordine di lavoro elencato per visualizzarne i dettagli.

![Immagine che mostra un ID ordine di lavoro selezionato](../images/ui/browse/select-work-order.png)

A seconda del tipo di ordine di lavoro selezionato, vengono fornite informazioni e controlli diversi. Questi sono trattati nelle sezioni seguenti.

### Dettagli di cancellazione del consumatore {#consumer-delete}

I dettagli di una richiesta di cancellazione del consumatore includono lo stato attuale e il tempo trascorso dalla richiesta. Ogni richiesta include anche **[!UICONTROL Stato per servizio]** sezione che fornisce informazioni sullo stato individuale di ciascun servizio a valle coinvolto nella cancellazione. Nella barra a destra è possibile utilizzare i controlli per aggiornare il nome e la descrizione dell&#39;ordine di lavoro.

![Immagine che mostra la pagina dei dettagli di un ordine di lavoro di eliminazione del consumatore](../images/ui/browse/consumer-delete-details.png)

### Dettagli di scadenza del set di dati {#dataset-expiration}

La pagina dei dettagli per la scadenza di un set di dati fornisce informazioni sui suoi attributi di base, inclusa la data di scadenza pianificata nei giorni rimanenti prima dell’eliminazione. Nella barra a destra, puoi utilizzare i controlli per modificare o annullare la scadenza.

![Immagine che mostra la pagina dei dettagli di un ordine di lavoro di scadenza di un set di dati](../images/ui/browse/ttl-details.png)

## Passaggi successivi

Questa guida illustra come visualizzare e gestire gli ordini di lavoro esistenti in materia di igiene dei dati nell’interfaccia utente di Platform. Per informazioni sulla creazione di ordini di lavoro personalizzati, consulta la seguente documentazione:

* [Gestire le scadenze dei set di dati](./dataset-expiration.md)
* [Gestire le cancellazioni dei consumatori](./delete-consumer.md)
