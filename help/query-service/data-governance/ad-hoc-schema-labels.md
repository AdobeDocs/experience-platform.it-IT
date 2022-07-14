---
title: Supporto per il controllo degli accessi basato su attributi per gli schemi ad hoc
description: Una guida per limitare l’accesso ai campi dati negli schemi ad hoc generati tramite Adobe Experience Platform Query Service.
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: d955473fb9123a6fc2384cde4073c713b921f582
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 1%

---

# Supporto del controllo degli accessi basato su attributi per schemi ad hoc

I dati inseriti in Adobe Experience Platform sono incapsulati dagli schemi Experience Data Model (XDM) e possono essere soggetti a restrizioni d’uso definite dalla tua organizzazione o da normative legali.

Eseguendo una query CTAS tramite Query Service quando non viene specificato alcuno schema, viene generato automaticamente uno schema ad hoc. Spesso è necessario limitare l’uso di determinati campi, o set di dati, di schemi ad hoc per controllare l’accesso sia a dati personali sensibili che a informazioni personali identificabili. Adobe Experience Platform facilita questo controllo degli accessi consentendo di etichettare i campi dello schema tramite l’interfaccia utente di Platform utilizzando la funzionalità di controllo degli accessi basata sugli attributi.

Le etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta della modalità di gestione dei dati. Tuttavia, è consigliabile etichettare i dati non appena vengono acquisiti in Platform, o non appena questi diventano disponibili per l’utilizzo in Platform.

L’etichettatura basata su schema è un componente importante del controllo degli accessi basato su attributi per gestire meglio l’accesso concesso a utenti o gruppi di utenti. Adobe Experience Platform consente di limitare l’accesso a qualsiasi campo di uno schema ad hoc creando e applicando etichette.

Questo documento fornisce un tutorial per gestire l’accesso ai dati sensibili applicando etichette ai campi di dati di schemi ad hoc generati tramite Query Service.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Sistema Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [[!DNL Schema Editor]](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html): Scopri come creare e gestire schemi e altre risorse nell’interfaccia utente di Platform.
* [[!DNL Data Governance]](../../data-governance/home.md): Scopri come [!DNL Data Governance] consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati.
* [Controllo dell&#39;accesso basato su attributi](../../access-control/abac/overview.md): Il controllo dell&#39;accesso basato su attributi è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l&#39;accesso a oggetti e/o funzionalità specifici in base agli attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un&#39;etichetta aggiunta a un campo di schema ad hoc o regolare. Un amministratore definisce i criteri di accesso che includono gli attributi per gestire le autorizzazioni di accesso degli utenti.

## Creare uno schema ad hoc

Una volta eseguita la query e generato il risultato, viene generato automaticamente uno schema ad hoc che viene aggiunto all’inventario dello schema.

Per aggiungere un’etichetta dati, passa a [!UICONTROL Schemi] scheda Sfoglia del dashboard selezionando [!UICONTROL Schemi] nella barra a sinistra dell’interfaccia utente di Platform. Viene visualizzato l’inventario dello schema.

>[!NOTE]
>
>Gli schemi ad hoc non vengono visualizzati per impostazione predefinita nell’inventario degli schemi.

## Scopri schemi ad hoc nell’inventario degli schemi dell’interfaccia utente di Platform {#discover-ad-hoc-schemas}

Per abilitare la visualizzazione di schemi ad hoc nell’interfaccia utente di Platform, seleziona l’icona del filtro (![Icona filtro.](../images/data-governance/filter.png)) a sinistra del campo di ricerca, quindi seleziona **[!UICONTROL Mostra schemi adhoc] nella barra a sinistra visualizzata.

![Le opzioni del filtro del dashboard dello schema a sinistra della barra con l’opzione &quot;Mostra schema ad hoc&quot; abilitata.](../images/data-governance/adhoc-schema-toggle.png)

Seleziona il nome dello schema ad hoc creato di recente dall’elenco disponibile. Viene visualizzata una visualizzazione della struttura dello schema ad hoc.

![Esempio di diagramma della struttura dello schema ad hoc.](../images/data-governance/adhoc-schema-structure-diagram.png)

## Modifica delle etichette di governance

Per modificare le etichette dati per lo schema ad hoc, seleziona la [!UICONTROL Etichette] scheda . L’area di lavoro delle etichette consente di applicare, creare e modificare le etichette ai campi dello schema ad hoc e di controllare le autorizzazioni di accesso tramite l’interfaccia utente. Tutti i campi all’interno dello schema ad hoc sono rappresentati qui.

## Modificare le etichette per lo schema o il campo

Per modificare le etichette per l&#39;intero schema, seleziona l&#39;icona a forma di matita (![](../images/data-governance/edit-icon.png)) sul lato del nome dello schema sotto il [!UICONTROL Etichette] scheda .

![L’icona a forma di matita evidenziata viene visualizzata nell’area di lavoro degli schemi.](../images/data-governance/edit-entire-schema-labels.png)

Per applicare un’etichetta a un campo esistente, selezionare uno o più campi dall’elenco seguito da [!UICONTROL Modifica delle etichette di governance] nella barra laterale destra.

![Le etichette vengono visualizzate nell’area di lavoro degli schemi con l’opzione &quot;Modifica etichette di governance&quot; evidenziata nella barra laterale dei diritti.](../images/data-governance/edit-governance-labels.png)

## Modifica del puntatore delle etichette

La [!UICONTROL Modificare le etichette] appare il puntatore. Da questa visualizzazione è possibile creare o modificare etichette di governance esistenti tramite l’interfaccia utente.

![L’opzione Modifica etichette è attiva.](../images/data-governance/edit-labels-popover.png)

Consulta la documentazione per informazioni su come [creare o modificare le etichette per lo schema o il campo selezionato](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/labels.html#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>La creazione di una nuova etichetta o la modifica di un’etichetta esistente richiede le autorizzazioni di amministratore per la tua organizzazione. Se non disponi di privilegi di amministratore, contatta l’amministratore di sistema per organizzare l’accesso.

Le etichette possono essere create anche utilizzando l&#39;area di lavoro delle autorizzazioni. Consulta la sezione [guida alla creazione di etichette nell’area di lavoro delle autorizzazioni](../../access-control/abac/ui/labels.md) per istruzioni.

Una volta applicato il livello appropriato di controllo dell’accesso basato su attributi, il seguente comportamento del sistema si applica a qualsiasi query eseguita tramite Query Service quando un utente tenta di accedere a dati non accessibili:

1. Se un utente non ha accesso a uno dei campi di uno schema, non sarà in grado di leggere o scrivere sul campo con restrizioni. Ciò vale per i seguenti scenari comuni:

   * Quando un utente tenta di eseguire una query con una sola colonna con restrizioni, il sistema genera un errore che la colonna non esiste.
   * Quando un utente tenta di eseguire una query con più colonne che includono una colonna con restrizioni, il sistema restituisce l&#39;output solo per tutte le colonne senza restrizioni.

1. Se un utente richiede l’accesso a un campo calcolato, deve avere accesso a tutti i campi utilizzati nella composizione, altrimenti il sistema negherà l’accesso al campo calcolato.

Se un&#39;identità o un&#39;identità primaria è impostata su uno schema ad hoc, il sistema rispetta automaticamente tutte le richieste di igiene dei dati associate e pulisce i dati contenuti in tali set di dati legati alla colonna identity.

## Passaggi successivi

Dopo aver letto questo documento hai una migliore comprensione su come aggiungere etichette di utilizzo dei dati a schemi ad hoc creati tramite query CTAS del servizio query. Se non lo hai già fatto, i seguenti documenti sono utili per migliorare la comprensione della governance dei dati in Query Service:

* [Identità dello schema ad hoc](./ad-hoc-schema-identities.md)
* [Governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it)
