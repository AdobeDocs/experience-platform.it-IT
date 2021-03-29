---
keywords: destinazioni;destinazione;pagina dettagli destinazioni;pagina dettagli destinazioni
title: Visualizza dettagli destinazione
description: 'La pagina dei dettagli di una singola destinazione fornisce una panoramica dei dettagli della destinazione. I dettagli della destinazione includono il nome della destinazione, l’ID, i segmenti mappati alla destinazione e i controlli per modificare l’attivazione e per abilitare e disabilitare il flusso di dati. '
seo-description: 'La pagina dei dettagli di una singola destinazione fornisce una panoramica dei dettagli della destinazione. I dettagli della destinazione includono il nome della destinazione, l’ID, i segmenti mappati alla destinazione e i controlli per modificare l’attivazione e per abilitare e disabilitare il flusso di dati. '
translation-type: tm+mt
source-git-commit: 4f5e7dfee17b2dde371efb82cf52d91c08696f39
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---


# Visualizza dettagli destinazione

## Panoramica {#overview}

Nell’interfaccia utente di Adobe Experience Platform puoi visualizzare e monitorare gli attributi e le attività delle destinazioni. Questi dettagli includono il nome e l’ID della destinazione, i controlli per attivare o disattivare le destinazioni e altro ancora. I dettagli per le destinazioni batch includono anche metriche per i record di profilo attivati e una cronologia delle esecuzioni dei flussi di dati.

>[!NOTE]
>
>La pagina dei dettagli delle destinazioni fa parte dell’area di lavoro [!UICONTROL Destinations] nell’interfaccia utente di Platform. Per ulteriori informazioni, consulta la [[!UICONTROL Destinations] panoramica dell&#39;area di lavoro](./destinations-workspace.md) .

Nell’area di lavoro **[!UICONTROL Destinations]** all’interno dell’interfaccia utente di Platform, passa alla scheda **[!UICONTROL Browse]** e seleziona il nome di una destinazione da visualizzare.

![](../assets/ui/details-page/select-destination.png)

Viene visualizzata la pagina dei dettagli della destinazione, con i relativi controlli disponibili. Se visualizzi i dettagli di una destinazione batch, viene visualizzata anche una dashboard di monitoraggio.

![](../assets/ui/details-page/details.png)

Inoltre, nella scheda Sfoglia è possibile scegliere di eliminare il flusso di dati selezionato selezionando l&#39;icona ![cestino](../assets/ui/details-page/trash-icon.png). Tutti i segmenti attivati nelle destinazioni verranno demappati prima che il flusso di dati venga eliminato.

![](../assets/ui/details-page/delete-flow.png)

## Barra a destra

La barra a destra visualizza le informazioni di base sulla destinazione.

![](../assets/ui/details-page/right-rail.png)

La tabella seguente illustra i controlli e i dettagli forniti dalla barra a destra:

| Elemento a destra | Descrizione |
| --- | --- |
| [!UICONTROL Activate] | Seleziona questo controllo per modificare i segmenti mappati alla destinazione. Per ulteriori informazioni, consulta la guida sull’ [attivazione dei segmenti su una destinazione](./activate-destinations.md) . |
| [!UICONTROL Delete] | Consente di eliminare questo flusso di dati e di rimuovere la mappatura dei segmenti precedentemente attivati, se presenti. |
| [!UICONTROL Destination name] | È possibile modificare questo campo per aggiornare il nome della destinazione. |
| [!UICONTROL Description] | È possibile modificare questo campo per aggiornare o aggiungere una descrizione facoltativa alla destinazione. |
| [!UICONTROL Destination] | Rappresenta la piattaforma di destinazione a cui vengono inviati i tipi di pubblico. Per ulteriori informazioni, consulta il [catalogo delle destinazioni](../catalog/overview.md) . |
| [!UICONTROL Status] | Indica se la destinazione è abilitata o disabilitata. |
| [!UICONTROL Marketing actions] | Indica le azioni di marketing (casi d’uso) applicabili a questa destinazione a scopo di governance dei dati. |
| [!UICONTROL Category] | Indica il tipo di destinazione. Per ulteriori informazioni, consulta il [catalogo delle destinazioni](../catalog/overview.md) . |
| [!UICONTROL Connection type] | Indica il modulo in base al quale i tipi di pubblico vengono inviati alla destinazione. I valori possibili includono &quot;[!UICONTROL Cookie]&quot; e &quot;[!UICONTROL Profile-based]&quot;. |
| [!UICONTROL Frequency] | Indica la frequenza con cui i tipi di pubblico vengono inviati alla destinazione. I valori possibili includono &quot;[!UICONTROL Streaming]&quot; e &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identity] | Rappresenta lo spazio dei nomi di identità accettato dalla destinazione, ad esempio `GAID`, `IDFA` o `email`. Per ulteriori informazioni sugli spazi dei nomi di identità accettati, consulta la [panoramica dello spazio dei nomi di identità](../../identity-service/namespaces.md). |
| [!UICONTROL Created by] | Indica l&#39;utente che ha creato la destinazione. |
| [!UICONTROL Created] | Indica la data/ora UTC al momento della creazione della destinazione. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Enabled]/[!UICONTROL Disabled] toggle

Puoi utilizzare l’interruttore **[!UICONTROL Enabled]/[!UICONTROL Disabled]** per avviare e mettere in pausa tutte le esportazioni di dati verso la destinazione.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs]

La scheda [!UICONTROL Dataflow runs] fornisce dati metrici sul flusso di dati da eseguire su destinazioni batch. Viene visualizzato un elenco di singole esecuzioni e delle relative metriche specifiche, insieme ai seguenti totali per i record di profilo:

* **[!UICONTROL Profile records activated]**: Numero totale di record di profilo creati o aggiornati per l’attivazione.
* **[!UICONTROL Profile records skipped]**: Numero totale di record di profilo saltati per l’attivazione in base alle uscite di profilo o agli attributi mancanti.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>Le esecuzioni dei flussi di dati vengono generate in base alla frequenza di pianificazione del flusso di dati di destinazione. Viene eseguita un&#39;esecuzione separata del flusso di dati per ogni criterio di unione applicato a un segmento.

Per visualizzare i dettagli di una particolare esecuzione di un flusso di dati, selezionare l’ora di inizio dell’esecuzione dall’elenco. La pagina dei dettagli di un&#39;esecuzione del flusso di dati contiene informazioni aggiuntive, come la dimensione dei dati elaborati e un elenco degli eventuali errori che si sono verificati con i dettagli relativi alla diagnostica degli errori.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Activation data] {#activation-data}

La scheda [!UICONTROL Activation data] visualizza un elenco di segmenti mappati sulla destinazione, con le relative date di inizio e di fine (se applicabili). Per visualizzare i dettagli di un particolare segmento, selezionane il nome dall’elenco.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;esplorazione della pagina dei dettagli di un segmento, consulta la [Panoramica dell&#39;interfaccia utente di segmentazione](../../segmentation/ui/overview.md#segment-details).

## Passaggi successivi

Questo documento illustra le funzionalità della pagina dei dettagli della destinazione. Per ulteriori informazioni sulla gestione delle destinazioni nell&#39;interfaccia utente, consulta la panoramica nell&#39; area di lavoro [[!UICONTROL Destinations]](./destinations-workspace.md).