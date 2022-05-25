---
title: Cerca ordini di lavoro di igiene dati
description: Scopri come visualizzare e gestire gli ordini di lavoro esistenti in materia di igiene dei dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---

# Sfoglia gli ordini di lavoro per l&#39;igiene dei dati

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="ID ordine di lavoro"
>abstract="Quando una richiesta di igiene dati viene inviata al sistema, viene creato un ordine di lavoro per eseguire l&#39;attività richiesta. In altre parole, un ordine di lavoro rappresenta un processo specifico di igiene dei dati, che include il suo stato attuale e altri dettagli correlati. A ogni ordine di lavoro viene assegnato automaticamente il proprio ID univoco al momento della creazione. Per ulteriori informazioni, consulta la guida all’interfaccia utente per l’igiene dei dati ."

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato Adobe Shield per il settore sanitario.

Quando una richiesta di igiene dati viene inviata al sistema, viene creato un ordine di lavoro per eseguire l&#39;attività richiesta. Un ordine di lavoro rappresenta un processo specifico di igiene dei dati (ad esempio l&#39;eliminazione dei dati dei consumatori), che include il suo stato attuale e altri dettagli correlati.

Questa guida illustra come visualizzare e gestire gli ordini di lavoro esistenti nell’interfaccia utente di Adobe Experience Platform.

## Elencare e filtrare gli ordini di lavoro esistenti

Quando accedi per la prima volta al **[!UICONTROL Igiene dei dati]** nell’interfaccia utente viene visualizzato un elenco degli ordini di lavoro esistenti con i relativi dettagli di base.

![Immagine che mostra [!UICONTROL Igiene dei dati] Area di lavoro nell’interfaccia utente di Platform](../images/ui/browse/work-order-list.png)

L&#39;elenco mostra solo gli ordini di lavoro per una categoria alla volta. Seleziona **[!UICONTROL Consumatore]** visualizzare un elenco delle attività di eliminazione dei consumatori e **[!UICONTROL Set di dati]** per visualizzare un elenco delle pianificazioni TTL (time-to-live) per i set di dati.

![Immagine che mostra [!UICONTROL Set di dati] scheda](../images/ui/browse/dataset-tab.png)

Seleziona l’icona funnel (![Immagine dell’icona funnel](../images/ui/browse/funnel-icon.png)) per visualizzare un elenco di filtri per gli ordini di lavoro visualizzati.

![Immagine dei filtri dell&#39;ordine di lavoro visualizzati](../images/ui/browse/filters.png)

A seconda della scheda che stai visualizzando, sono disponibili diversi filtri:

| Filtro | Categoria | Descrizione |
| --- | --- | --- |
| [!UICONTROL Stato] | [!UICONTROL Consumatore] &amp; [!UICONTROL Set di dati] | Filtrare in base allo stato corrente dell&#39;ordine di lavoro. |
| [!UICONTROL Data di creazione] | [!UICONTROL Consumatore] | Filtra in base alla data in cui è stata effettuata la richiesta di eliminazione del consumatore. |
| [!UICONTROL Data di creazione] | [!UICONTROL Set di dati] | Filtra in base alla data in cui è stata effettuata la richiesta di eliminazione del consumatore. |
| [!UICONTROL Data di eliminazione] | [!UICONTROL Set di dati] | Filtra in base alla data di eliminazione pianificata dal TTL. |
| [!UICONTROL Data di aggiornamento] | [!UICONTROL Set di dati] | Filtra in base alla data dell’ultimo aggiornamento del TTL del set di dati. Le creazioni e le scadenza TTL vengono conteggiate come aggiornamenti. |

{style=&quot;table-layout:auto&quot;}

## Visualizza i dettagli di un ordine di lavorazione

Selezionare l&#39;ID di un ordine di lavoro elencato per visualizzarne i dettagli.

![Immagine che mostra un ID ordine di lavoro selezionato](../images/ui/browse/select-work-order.png)

A seconda del tipo di ordine di lavoro selezionato, vengono fornite informazioni e controlli diversi. Questi sono trattati nelle sezioni seguenti.

### Dettagli di cancellazione del consumatore

<!-- (Not available for initial release)
>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."
-->

I dettagli di una richiesta di cancellazione del consumatore sono di sola lettura e presentano gli attributi di base, come lo stato corrente e il tempo trascorso dalla richiesta.

![Immagine che mostra la pagina dei dettagli di un ordine di lavoro di eliminazione del consumatore](../images/ui/browse/consumer-delete-details.png)

### Dettagli TTL set di dati

La pagina dei dettagli di un set di dati TTL fornisce informazioni sui suoi attributi di base, inclusa la data di scadenza pianificata nei giorni rimanenti prima dell’eliminazione. Nella barra a destra è possibile utilizzare i controlli per modificare o annullare il TTL.

![Immagine che mostra la pagina dei dettagli di un ordine di lavoro TTL di un set di dati](../images/ui/browse/ttl-details.png)

## Passaggi successivi

Questa guida illustra come visualizzare e gestire gli ordini di lavoro esistenti in materia di igiene dei dati nell’interfaccia utente di Platform. Per informazioni sulla creazione di ordini di lavoro personalizzati, consulta la seguente documentazione:

* [Eliminare un consumatore](./delete-consumer.md)
* [Pianificare un TTL di set di dati](./ttl.md)
