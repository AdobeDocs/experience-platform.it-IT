---
title: Eliminazioni nel servizio Identity
description: Questo documento fornisce una panoramica dei vari meccanismi che puoi utilizzare per eliminare i dati di identità in Experience Platform e per fornire chiarezza su come i grafici di identità possono essere interessati.
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 1%

---

# Eliminazioni nel servizio Identity

Il servizio Adobe Experience Platform Identity genera grafici delle identità collegando in modo deterministico le identità tra dispositivi e sistemi per una singola persona. I collegamenti del grafico delle identità sono stabiliti quando due o più identità contrassegnate vengono ricevute all’interno della stessa riga di dati.

I grafici delle identità vengono utilizzati da Real-Time Customer Profile per creare una visualizzazione completa e unica degli attributi e dei comportamenti dei clienti, consentendo di fornire esperienze digitali personali e di impatto in tempo reale, alle persone e non ai dispositivi.

Questo documento fornisce una panoramica dei vari meccanismi che puoi utilizzare per eliminare i dati di identità in Experience Platform e per fornire chiarezza su come i grafici di identità possono essere interessati.

## Introduzione

Il documento seguente fa riferimento alle seguenti caratteristiche di Experience Platform:

* [Servizio identità](home.md): ottieni una visione migliore dei singoli clienti e del loro comportamento collegando le identità tra dispositivi e sistemi.
   * [Grafico delle identità](./ui/identity-graph-viewer.md): un grafo di identità è una mappa delle relazioni tra identità diverse per un particolare cliente, che ti fornisce una rappresentazione visiva di come il cliente interagisce con il tuo marchio su canali diversi.
   * [Spazi dei nomi delle identità](namespaces.md): gli spazi dei nomi di identità sono un componente di Identity Service che fungono da indicatori del contesto a cui si riferisce un’identità. Ad esempio, distinguono un valore di &quot;name<span>@email.com&quot; come indirizzo e-mail o &quot;443522&quot; come ID CRM numerico.
* [Servizio catalogo](../catalog/home.md): esplora la derivazione dei dati, i metadati, le descrizioni dei file, le directory e i set di dati all’interno del data lake.
* [Igiene dei dati](../hygiene/home.md): gestisci i dati consumer memorizzati pianificando scadenze automatizzate dei set di dati o eliminando singoli record da un set di dati o da tutti i set di dati.
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md): gestisci le richieste dei clienti di accedere ai propri dati personali nelle applicazioni Adobe Experience Cloud, rinunciarvi o eliminarli.
* [Profilo cliente in tempo reale](../profile/home.md): fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.

## Eliminazioni di identità singole

Le singole richieste di eliminazione delle identità consentono di eliminare un’identità all’interno di un grafico, con conseguente rimozione dei collegamenti associati a una singola identità utente associata a uno spazio dei nomi dell’identità. Puoi utilizzare i meccanismi forniti da [Privacy Service](../privacy-service/home.md) per casi d’uso come richieste dei clienti per l’eliminazione dei dati e la conformità alle normative sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD).

Le sezioni seguenti descrivono i meccanismi utilizzabili per le singole richieste di eliminazione delle identità in Experience Platform.

### Eliminazione di una singola identità in Privacy Service

Privacy Service elabora le richieste dei clienti di accedere ai propri dati personali, rinunciarvi o eliminarli, in base a quanto stabilito dalle normative sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD) e il California Consumer Privacy Act (CCPA). Con Privacy Service, puoi inviare richieste di processi utilizzando l’API o l’interfaccia utente. Quando Experience Platform riceve una richiesta di eliminazione da Privacy Service, Platform invia una conferma a Privacy Service che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l’eliminazione. L’eliminazione della singola identità si basa sullo spazio dei nomi e/o sul valore ID fornito. Inoltre, l’eliminazione avviene per tutte le sandbox associate a una determinata organizzazione. Per ulteriori informazioni, consulta la guida su [elaborazione delle richieste di accesso a dati personali in Identity Service](privacy.md).

La tabella seguente fornisce una suddivisione dell’eliminazione di una singola identità in Privacy Service:

| Eliminazione di una singola identità | Privacy Service |
| --- | --- |
| Casi d’uso accettati | Solo richieste relative alla privacy dei dati (RGPD, CCPA). |
| Latenza stimata | Da giorni a settimane |
| Servizi interessati | L’eliminazione di una singola identità in Privacy Service consente di scegliere se eliminare i dati da Identity Service, Real-Time Customer Profile o data lake. |
| Pattern di eliminazione | Eliminare un’identità da Identity Service. |

{style="table-layout:auto"}

## Eliminazione set di dati

Le sezioni seguenti descrivono i meccanismi che possono essere utilizzati per eliminare i set di dati e i collegamenti di identità associati in Experience Platform.

### Eliminazione del set di dati in Catalog Service

Puoi utilizzare Catalog Service per inviare richieste di eliminazione di set di dati. Per ulteriori informazioni su come eliminare i set di dati con Catalog Service, consulta la guida su [eliminazione di oggetti tramite l’API Catalog Service](../catalog/api/delete-object.md). In alternativa, puoi utilizzare l’interfaccia utente di Platform per inviare richieste di eliminazione di set di dati. Per ulteriori informazioni, leggere [guida utente sui set di dati](../catalog/datasets/user-guide.md#delete-a-dataset).

### Scadenze del set di dati nell’igiene dei dati

Il [[!UICONTROL Igiene dei dati] workspace](../hygiene/ui/overview.md) nell’interfaccia utente di Adobe Experience Platform consente di pianificare le scadenze per i set di dati. Quando un set di dati raggiunge la data di scadenza, il data lake, Identity Service e Real-Time Customer Profile iniziano processi separati per rimuovere i contenuti del set di dati dai rispettivi servizi. Per ulteriori informazioni, consulta la guida su [gestione delle scadenze dei set di dati utilizzando [!UICONTROL Igiene dei dati] workspace](../hygiene/ui/dataset-expiration.md).

La tabella seguente fornisce una suddivisione delle differenze tra l’eliminazione dei set di dati in Catalog Service e l’igiene dei dati:

| Eliminazione set di dati | Servizio catalogo | Igiene dei dati |
| --- | --- | --- |
| Casi d’uso accettati | Elimina i set di dati completi e le informazioni sull’identità associate in Platform. | Gestione dei dati memorizzati in Experience Platform. |
| Latenza stimata | Days | Days |
| Servizi interessati | L’eliminazione del set di dati tramite Catalog Service elimina i dati da Identity Service, Real-Time Customer Profile e data lake. | L’eliminazione del set di dati tramite igiene dei dati elimina i dati da Identity Service, Real-Time Customer Profile e data lake. |
| Pattern di eliminazione | Elimina le identità collegate da Identity Service stabilite da un particolare set di dati. | Elimina le identità collegate da Identity Service stabilito da un particolare set di dati, in base alla pianificazione di scadenza. |

{style="table-layout:auto"}

## Diversi stati dei grafici di identità dopo l’eliminazione

Tutte le eliminazioni del grafo delle identità determinano la rimozione dei collegamenti tra due o più identità, come specificato dalla richiesta di eliminazione. Per le richieste di eliminazione dei set di dati, tutti i collegamenti di identità stabiliti dal set di dati specificato vengono rimossi e possono o meno rimuovere le identità dai grafici. Per richieste di eliminazione di identità singole, i collegamenti di identità vengono rimossi per l’identità specificata e, di conseguenza, il valore di identità stesso viene rimosso da tutti i grafici di identità. Le identità senza un singolo collegamento a un’altra identità non vengono memorizzate in Identity Service.

Di seguito è riportato uno schema dei potenziali impatti che le eliminazioni possono avere sullo stato dei grafici di identità.

| Stato del grafico delle identità | Descrizione |
| --- | --- |
| Aggiornamento parziale | Un aggiornamento parziale di un grafico si verifica quando almeno due identità rimangono collegate all’interno di un grafico dopo la corretta elaborazione di una richiesta di eliminazione. Dopo l’eliminazione, i collegamenti di identità rimanenti possono rimanere collegati l’uno all’altro, oppure possono essere suddivisi in due o più grafici separati a seconda delle identità eliminate. |
| Rimozione completa | Un grafo deve avere almeno due identità collegate per esistere. Pertanto, se una richiesta di eliminazione comporta la rimozione di tutti i collegamenti esistenti all’interno di un grafico, il grafico verrà rimosso completamente. |
| Nessuna modifica | Un grafico non sarà interessato se una particolare richiesta di eliminazione contiene un’identità o un set di dati non associato ad alcun membro del grafico. Inoltre, un grafico non viene aggiornato anche se la richiesta di eliminazione rimuove un collegamento tra un set di dati o una combinazione di identità e set di dati, dato che il collegamento è stato stabilito da un altro collegamento non eliminato. Ciò significa che se un collegamento esiste in due set di dati diversi, il grafico non verrà aggiornato perché viene rimosso solo uno dei set di dati. |

{style="table-layout:auto"}

## Passaggi successivi

In questo documento sono stati descritti i vari meccanismi che è possibile utilizzare per eliminare identità e set di dati in Experience Platform. Questo documento illustra inoltre come le eliminazioni di identità e set di dati possono influire sui grafici di identità. Per ulteriori informazioni sul servizio Identity, consulta [Panoramica del servizio Identity](home.md).

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->
