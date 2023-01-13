---
title: Eliminazioni nel servizio Identity
description: Questo documento fornisce una panoramica dei vari meccanismi che è possibile utilizzare per eliminare i dati di identità in Experience Platform e per fornire chiarezza su come i grafici di identità possono essere interessati.
source-git-commit: da1ce4560d28d43db47318883f9656cebb2eb487
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# Eliminazioni nel servizio Identity

Il servizio Adobe Experience Platform Identity genera grafici di identità mediante un collegamento deterministico delle identità tra dispositivi e sistemi per una singola persona. I collegamenti ai grafici di identità sono stabiliti quando due o più identità contrassegnate vengono ricevute all’interno della stessa riga di dati.

I grafici di identità sono sfruttati da Profilo cliente in tempo reale per creare una visualizzazione completa e singolare degli attributi e dei comportamenti dei clienti, consentendo di fornire esperienze digitali personali e di impatto in tempo reale, a persone e non a dispositivi.

Questo documento fornisce una panoramica dei vari meccanismi che è possibile utilizzare per eliminare i dati di identità in Experience Platform e per fornire chiarezza su come i grafici di identità possono essere interessati.

## Introduzione

Il documento seguente fa riferimento alle seguenti caratteristiche dell&#39;Experience Platform:

* [Servizio identità](home.md): Ottieni una visione migliore dei singoli clienti e del loro comportamento attraverso il collegamento delle identità tra dispositivi e sistemi.
   * [Grafico di identità](./ui/identity-graph-viewer.md): Un grafico delle identità è una mappa delle relazioni tra identità diverse per un particolare cliente, che fornisce una rappresentazione visiva di come il cliente interagisce con il tuo marchio su diversi canali.
   * [Namespace Identity](namespaces.md): Gli spazi dei nomi di identità sono un componente del servizio Identity che funge da indicatori del contesto a cui si riferisce un’identità. Ad esempio, distinguono un valore di &quot;name<span>@email.com&quot; come indirizzo e-mail o &quot;443522&quot; come ID CRM numerico.
* [Servizio catalogo](../catalog/home.md): Esplora la derivazione dei dati, i metadati, le descrizioni dei file, le directory e i set di dati all’interno del data lake.
* [Igiene dei dati](../hygiene/home.md): Gestisci i dati dei consumatori memorizzati pianificando scadenze automatizzate dei set di dati o eliminando singoli record da un set di dati o da tutti i set di dati.
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Gestisci le richieste dei clienti per l&#39;accesso, la rinuncia o l&#39;eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [Profilo cliente in tempo reale](../profile/home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.

## Eliminazioni di singole identità

Le richieste di eliminazione di identità singole consentono di eliminare un’identità all’interno di un grafico, causando la rimozione di collegamenti associati a una singola identità utente associata a uno spazio dei nomi identità. Puoi utilizzare i meccanismi forniti da [Privacy Service](../privacy-service/home.md) per casi d’uso quali richieste di cancellazione dei dati da parte dei clienti e conformità alle normative sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD).

Le sezioni seguenti descrivono i meccanismi che è possibile utilizzare per le richieste di eliminazione di singole identità in Experience Platform.

### Eliminazione di una singola identità in Privacy Service

Privacy Service tratta le richieste dei clienti di accedere, rinunciare alla vendita o cancellare i propri dati personali come delineato dalle normative sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD) e il California Consumer Privacy Act (CCPA). Con Privacy Service è possibile inviare richieste di lavoro utilizzando l’API o l’interfaccia utente di . Quando Experience Platform riceve una richiesta di cancellazione da Privacy Service, Platform invia una conferma ad Privacy Service che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l’eliminazione. L’eliminazione della singola identità si basa sul namespace e/o sul valore ID fornito. Inoltre, l’eliminazione avviene per tutte le sandbox associate a una determinata organizzazione. Per ulteriori informazioni, consulta la guida su [elaborazione della richiesta di accesso a dati personali nel servizio Identity](privacy.md).

La tabella seguente fornisce una suddivisione dell’eliminazione di una singola identità in Privacy Service :

| Eliminazione di una singola identità | Privacy Service |
| --- | --- |
| Casi di utilizzo accettati | Solo richieste di privacy dei dati (RGPD, CCPA). |
| Latenza stimata | Giorni a settimane |
| Servizi interessati | L’eliminazione di una singola identità in Privacy Service consente di selezionare se i dati verranno eliminati dal servizio Identity, dal profilo cliente in tempo reale o dal data lake. |
| Pattern di eliminazione | Elimina un’identità dal servizio Identity. |

{style=&quot;table-layout:auto&quot;}

## Eliminazione del set di dati

Le sezioni seguenti descrivono i meccanismi che possono essere utilizzati per eliminare i set di dati e i collegamenti di identità associati in Experience Platform.

### Eliminazione del set di dati nel servizio catalogo

Puoi usare il servizio Catalogo per inviare richieste di eliminazione dei set di dati. Per ulteriori informazioni su come eliminare i set di dati con Servizio catalogo, consulta la guida su [eliminazione di oggetti tramite l’API del servizio catalogo](../catalog/api/delete-object.md). In alternativa, puoi utilizzare l’interfaccia utente di Platform per inviare richieste di eliminazione dei set di dati. Per ulteriori informazioni, consulta la sezione [guida utente dei set di dati](../catalog/datasets/user-guide.md#delete-a-dataset).

### Scadenza del set di dati nell&#39;igiene dei dati

La [[!UICONTROL Igiene dei dati] workspace](../hygiene/ui/overview.md) nell’interfaccia utente di Adobe Experience Platform consente di pianificare le scadenze per i set di dati. Quando un set di dati raggiunge la data di scadenza, il data lake, il servizio Identity e il profilo cliente in tempo reale iniziano processi separati per rimuovere il contenuto del set di dati dai rispettivi servizi. Per ulteriori informazioni, consulta la guida su [gestione delle scadenze dei set di dati tramite [!UICONTROL Igiene dei dati] workspace](../hygiene/ui/dataset-expiration.md).

La tabella seguente fornisce una suddivisione delle differenze tra l’eliminazione dei set di dati in Servizio catalogo e igiene dei dati:

| Eliminazione del set di dati | Servizio catalogo | Igiene dei dati |
| --- | --- | --- |
| Casi di utilizzo accettati | Elimina set di dati completi e le relative informazioni di identità associate in Platform. | Gestione dei dati memorizzati in Experience Platform. |
| Latenza stimata | Days | Days |
| Servizi interessati | L’eliminazione del set di dati tramite il Servizio catalogo elimina i dati dal Servizio identità, dal Profilo cliente in tempo reale e dal data lake. | L’eliminazione del set di dati tramite l’igiene dei dati elimina i dati da Identity Service, Real-Time Customer Profile e Data Lake. |
| Pattern di eliminazione | Elimina le identità collegate dal servizio Identity stabilite da un particolare set di dati. | Elimina le identità collegate dal servizio Identity stabilite da un particolare set di dati, in base alla pianificazione della scadenza. |

{style=&quot;table-layout:auto&quot;}

## Diversi stati dei grafici di identità dopo la cancellazione

Tutte le eliminazioni del grafico di identità causano la rimozione dei collegamenti tra due o più identità, come specificato dalla richiesta di eliminazione. Per le richieste di eliminazione dei set di dati, tutti i collegamenti di identità stabiliti dal set di dati specificato vengono rimossi e possono rimuovere o meno le identità dai grafici. Per le richieste di eliminazione di identità singole i collegamenti di identità vengono rimossi per l&#39;identità specificata e di conseguenza il valore di identità stesso viene rimosso da tutti i grafici di identità. Le identità senza un singolo collegamento a un’altra identità non vengono memorizzate nel servizio Identity.

Di seguito è riportato un quadro dei potenziali impatti che le cancellazioni possono avere sullo stato dei grafici di identità.

| Stato del grafico di identità | Descrizione |
| --- | --- |
| Aggiornamento parziale | Un aggiornamento parziale di un grafico si verifica quando almeno due identità rimangono collegate all’interno di un grafico dopo la corretta elaborazione di una richiesta di eliminazione. Dopo l’eliminazione, i collegamenti di identità rimanenti possono rimanere collegati tra loro, oppure possono essere suddivisi in due o più grafici separati a seconda delle identità che sono state eliminate. |
| Rimozione completa | Per poter esistere, un grafico deve avere almeno due identità collegate. Pertanto, se una richiesta di cancellazione comporta la rimozione di tutti i collegamenti esistenti all’interno di un grafico, il grafico verrà rimosso completamente. |
| Nessuna modifica | Un grafico non sarà interessato se una particolare richiesta di eliminazione contiene un&#39;identità o un set di dati non associati ad alcun membro del grafico. Inoltre, un grafico non viene aggiornato anche se la richiesta di eliminazione rimuove un collegamento tra un set di dati o una combinazione di set di dati di identità, dato che il collegamento è stato stabilito da un altro collegamento che non è stato eliminato. Ciò significa che se un collegamento esiste in due set di dati diversi, il grafico non verrà aggiornato perché viene rimosso solo uno dei set di dati. |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi

Questo documento tratta i vari meccanismi che è possibile utilizzare per eliminare le identità e i set di dati in Experience Platform. Questo documento illustra anche come le eliminazioni di identità e set di dati possono influenzare i grafici di identità. Per ulteriori informazioni sul servizio Identity, consulta la sezione [Panoramica del servizio Identity](home.md).

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