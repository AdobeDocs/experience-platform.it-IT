---
keywords: Experience Platform; home; argomenti popolari; tag unificati; tag;
title: Panoramica sui tag unificati (Beta)
description: Questo documento fornisce informazioni sui tag unificati in Adobe Experience Platform
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '607'
ht-degree: 100%

---

# Panoramica sui tag unificati (Beta)

>[!IMPORTANT]
>
>I tag unificati sono nella versione beta. Per lasciare un feedback, fai clic sul pulsante nella parte superiore della pagina di Amministrazione dei tag.

I tag sono una funzionalità di Adobe Experience Platform che consente agli amministratori di gestire le tassonomie dei metadati al fine di classificare gli oggetti aziendali per semplificare l’individuazione e la classificazione. I tag sono metadati che possono essere considerati come parole chiave che possono essere associate a un segmento, a un set di dati, a un percorso o ad altri oggetti per consentire alle ricerche di trovare l’oggetto e gli oggetti correlati. I tag sono classificati in due tipi: categorizzati e non categorizzati.

Per fornire più contesto e definire lo scopo di un tag, le categorie organizzano i tag in set utili. Un amministratore definisce i tag categorizzati disponibili che gli utenti possono aggiungere agli oggetti. I nuovi tag che non contengono categorie possono essere creati anche in linea nei flussi di lavoro in cui vengono applicati. Questi tag verranno mostrati nella sezione non categorizzati della libreria di tag. I tag possono essere applicati sia dagli amministratori che dagli utenti, indipendentemente da chi li ha creati. Tutti i tipi di tag possono essere selezionati quando vengono assegnati a un oggetto, a una ricerca oppure a un filtro.

## Terminologia dei tag

L’assegnazione tag include i seguenti componenti:

| Terminologia | Definizione |
| --- | --- |
| Archiviato | Uno stato per un tag che mantiene le associazioni correnti con gli oggetti ma impedisce l’applicazione del tag ad altri oggetti.  I tag archiviati sono nascosti dal selettore di tag. |
| Oggetto | Un elemento di Experience Cloud a cui è possibile applicare un tag.  Esempi: segmento, percorso, set di dati. |
| Tag | I tag sono metadati che possono essere considerati come parole chiave che possono essere associate a un segmento, a un set di dati, a un percorso o ad altri oggetti per consentire alle ricerche di trovare l’oggetto e gli oggetti correlati. |
| Categoria di tag | Le categorie raggruppano i tag in set significativi per fornire maggiore contesto o descrivere lo scopo del tag.  Gli amministratori gestiscono le categorie e i tag all’interno delle categorie. |
| Tag non categorizzato | Un nuovo tag creato in linea in cui vengono applicati i tag. Questi tag possono essere creati e applicati da qualsiasi utente, ma non sono associati a una categoria.  Gli amministratori possono spostare questi tag in una categoria per allinearli ad altri tag simili. |

## Libreria di tag

La categoria e la gestione dei tag tramite la libreria di tag è disponibile nell’area di navigazione di Experience Platform e Journey Optimizer. Le modifiche apportate ai tag nella libreria vengono applicate a tutti gli oggetti che supportano i tag. Tutti gli utenti possono accedere e sfogliare l’la libreria di tag, ma la gestione dei tag è limitata agli amministratori di sistema e di prodotto.

La libreria di tag dispone di tre livelli gerarchici che consentono agli utenti di gestire le categorie di tag, i tag all’interno di una categoria e i singoli tag. Durante la gestione di un singolo tag, gli utenti possono visualizzare e passare a qualsiasi oggetto in cui tale tag è attualmente applicato.

### Categorie di tag

Le categorie raggruppano i tag in set significativi per fornire maggiore contesto o descrivere lo scopo del tag. In qualsiasi tag con una categoria, il nome della categoria seguito da due punti precede il nome del tag.

Quando si utilizzano le categorie di tag, è possibile eseguire le seguenti azioni:

* [Creare la categoria di tag](./ui/tags-categories.md#create-tag-category)
* [Modificare la categoria di tag](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Eliminare la categoria di tag](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Gestione dei tag all’interno di una categoria

>[!NOTE]
>
>Per gestire i tag in Experience Cloud, è necessario avere il ruolo di amministratore di sistema o di prodotto di Adobe Experience Platform per la tua organizzazione e disporre di un abbonamento a Experience Cloud.

Puoi creare e gestire i tag all’interno di una categoria (o del gruppo predefinito “Non categorizzati”). Durante la gestione dei tag, è possibile eseguire le seguenti azioni:

* [Creare un tag](./ui/managing-tags.md#create-a-tag-create-tag)
* [Modificare un tag](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Spostare un tag tra le categorie](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Archiviare un tag](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Ripristinare un tag archiviato](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Eliminare un tag](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Visualizzare oggetti con tag](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
