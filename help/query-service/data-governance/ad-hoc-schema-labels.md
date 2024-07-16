---
title: Supporto del controllo degli accessi basato su attributi per schemi ad hoc
description: Guida per limitare l’accesso ai campi dati negli schemi ad hoc generati tramite Adobe Experience Platform Query Service.
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 2%

---

# Supporto del controllo degli accessi basato su attributi per schemi ad hoc

Tutti i dati introdotti in Adobe Experience Platform sono incapsulati da schemi Experience Data Model (XDM) e possono essere soggetti a restrizioni di utilizzo definite dall’organizzazione o da normative legali.

Se non viene specificato alcuno schema, viene generato automaticamente uno schema ad hoc eseguendo una query CTAS tramite Query Service. Spesso è necessario limitare l’utilizzo di determinati campi o set di dati di schemi ad hoc per controllare l’accesso sia ai dati personali sensibili che alle informazioni personali. Adobe Experience Platform facilita questo controllo di accesso consentendoti di etichettare i campi dello schema tramite l’interfaccia utente di Platform utilizzando la funzionalità di controllo di accesso basato su attributi.

Le etichette possono essere applicate in qualsiasi momento, offrendo flessibilità nella scelta di come gestire i dati. Tuttavia, è consigliabile etichettare i dati non appena vengono acquisiti in Platform o non appena i dati diventano disponibili per l’utilizzo in Platform.

L’etichettatura basata su schema è un componente importante del controllo dell’accesso basato su attributi per gestire meglio l’accesso concesso a utenti o gruppi di utenti. Adobe Experience Platform consente di limitare l’accesso a qualsiasi campo di uno schema ad hoc tramite la creazione e l’applicazione di etichette.

Questo documento fornisce un tutorial per gestire l’accesso ai dati sensibili applicando etichette ai campi di dati di schemi ad hoc generati tramite Query Service.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [[!DNL Schema Editor]](../../xdm/ui/overview.md): scopri come creare e gestire schemi e altre risorse nell’interfaccia utente di Platform.
* [[!DNL Data Governance]](../../data-governance/home.md): scopri come [!DNL Data Governance] ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all&#39;utilizzo dei dati.
* [Controllo dell&#39;accesso basato su attributi](../../access-control/abac/overview.md): il controllo dell&#39;accesso basato su attributi è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l&#39;accesso a oggetti specifici e/o funzionalità basate su attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo schema ad hoc o normale. Un amministratore definisce i criteri di accesso che includono attributi per gestire le autorizzazioni di accesso degli utenti.

## Creare uno schema ad hoc

Una volta eseguita la query e generati i risultati, viene generato automaticamente uno schema ad hoc che viene aggiunto all’inventario degli schemi.

Per aggiungere un&#39;etichetta dati, passa alla scheda Sfoglia del dashboard [!UICONTROL Schemi] selezionando [!UICONTROL Schemi] nella barra a sinistra dell&#39;interfaccia utente di Platform. Viene visualizzato l’inventario degli schemi.

>[!NOTE]
>
>Gli schemi ad hoc non vengono visualizzati per impostazione predefinita nell’inventario degli schemi.

## Scopri gli schemi ad hoc nell’inventario degli schemi dell’interfaccia utente di Platform {#discover-ad-hoc-schemas}

Per abilitare la visualizzazione degli schemi ad hoc nell&#39;interfaccia utente di Platform, selezionare l&#39;icona del filtro (![Icona del filtro.](../images/data-governance/filter.png)) a sinistra del campo di ricerca, quindi seleziona **[!UICONTROL Mostra schemi ad hoc] nella barra a sinistra visualizzata.

![Nella barra a sinistra delle opzioni del filtro del dashboard Schema è abilitato l&#39;interruttore &#39;Mostra schema ad hoc&#39;.](../images/data-governance/adhoc-schema-toggle.png)

Seleziona il nome dello schema ad hoc creato di recente dall’elenco disponibile. Viene visualizzata una visualizzazione della struttura dello schema ad hoc.

![Esempio di diagramma ad hoc della struttura dello schema.](../images/data-governance/adhoc-schema-structure-diagram.png)

## Modificare le etichette di governance

Per modificare le etichette dati per lo schema ad hoc, seleziona la scheda [!UICONTROL Etichette]. L’area di lavoro etichette consente di applicare, creare e modificare le etichette nei campi dello schema ad hoc e di controllare le autorizzazioni di accesso tramite l’interfaccia utente. Tutti i campi all’interno dello schema ad hoc sono rappresentati qui.

## Modifica le etichette per lo schema o il campo

Per modificare le etichette per l&#39;intero schema, selezionare l&#39;icona della matita (![Un&#39;icona della matita.](../images/data-governance/edit-icon.png)) a lato del nome dello schema sotto la scheda [!UICONTROL Etichette].

![La visualizzazione delle etichette nell&#39;area di lavoro degli schemi con l&#39;icona della matita evidenziata.](../images/data-governance/edit-entire-schema-labels.png)

Per applicare un&#39;etichetta a un campo esistente, seleziona uno o più campi dall&#39;elenco seguito da [!UICONTROL Modifica etichette di governance] nella barra laterale a destra.

![La visualizzazione delle etichette nell&#39;area di lavoro degli schemi con l&#39;opzione &#39;Modifica etichette di governance&#39; evidenziata nella barra laterale a destra.](../images/data-governance/edit-governance-labels.png)

## Popover Modifica etichette

Viene visualizzato il popover [!UICONTROL Modifica etichette]. Da questa vista puoi creare o modificare le etichette di governance esistenti tramite l’interfaccia utente.

![Finestra a comparsa Modifica etichette.](../images/data-governance/edit-labels-popover.png)

Consulta la documentazione per istruzioni su come [creare o modificare le etichette per lo schema o il campo selezionato](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>La creazione di una nuova etichetta o la modifica di un’etichetta esistente richiede le autorizzazioni di amministratore per la tua organizzazione. Se non disponi dei privilegi di amministratore, contatta l’amministratore di sistema per organizzare l’accesso.

Le etichette possono essere create anche utilizzando l’area di lavoro delle autorizzazioni. Per istruzioni, consulta la [guida sulla creazione di etichette nell&#39;area di lavoro autorizzazioni](../../access-control/abac/ui/labels.md).

Una volta applicato il livello appropriato di controllo degli accessi basato su attributi, il seguente comportamento di sistema si applica a qualsiasi query eseguita tramite Query Service quando un utente tenta di accedere a dati non accessibili:

1. Se a un utente viene negato l’accesso a uno dei campi all’interno di uno schema, non potrà leggere o scrivere nel campo con restrizioni. Questo vale per i seguenti scenari comuni:

   * Quando un utente tenta di eseguire una query con una sola colonna con restrizioni, il sistema restituisce un errore per informare che la colonna non esiste.
   * Quando un utente tenta di eseguire una query con più colonne che includono una colonna con restrizioni, il sistema restituisce l’output solo per tutte le colonne senza restrizioni.

1. Se un utente richiede l’accesso a un campo calcolato, deve avere accesso a tutti i campi utilizzati nella composizione, altrimenti il sistema negherà l’accesso al campo calcolato.

Se un’identità o un’identità primaria è impostata su uno schema ad hoc, il sistema rispetta automaticamente tutte le richieste di igiene dei dati associate e pulisce i dati in tali set di dati associati alla colonna di identità.

## Passaggi successivi

Dopo aver letto questo documento hai una migliore comprensione di come aggiungere etichette di utilizzo dei dati a schemi ad hoc creati tramite query CTAS di Query Service. Se non lo hai già fatto, i seguenti documenti sono utili per comprendere meglio la governance dei dati in Query Service:

* [Identità di schemi ad hoc](./ad-hoc-schema-identities.md)
* [Governance dei dati](../../data-governance/home.md)
