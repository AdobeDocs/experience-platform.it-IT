---
keywords: Experience Platform;home;argomenti popolari;tag amministrativi;tag;
title: Panoramica sui tag amministrativi
description: Questo documento fornisce informazioni sui tag amministrativi in Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 7f0572af2d582353a0dde12bdb6692f342463312
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---

# Panoramica sui tag

I tag sono una funzionalità di Adobe Experience Platform che consente agli amministratori di gestire le tassonomie dei metadati al fine di classificare gli oggetti aziendali per semplificarne l’individuazione e la categorizzazione. I tag sono metadati che possono essere paragonati a parole chiave che possono essere collegate a un segmento, a un set di dati, a un percorso o ad altri oggetti per consentire le ricerche in grado di trovare l’oggetto e gli oggetti correlati. I tag sono classificati in due tipi: categorizzato e non categorizzato.

Per fornire più contesto e definire lo scopo di un tag, le categorie organizzano i tag in set utili. Un amministratore definisce i tag suddivisi in categorie che gli utenti possono aggiungere agli oggetti. I nuovi tag che non contengono categorie possono essere creati anche in linea nei flussi di lavoro in cui vengono applicati i tag. Questi tag verranno visualizzati nella sezione non categorizzata dell’inventario tag. I tag possono essere applicati sia dagli amministratori che dagli utenti, indipendentemente da chi li ha creati. È possibile selezionare tutti i tipi di tag quando si assegna a un oggetto, si esegue una ricerca o un filtro.

## Terminologia dei tag

L’assegnazione tag include i seguenti componenti:

| Terminologia | Definizione |
| --- | --- |
| Archiviato | Stato di un tag che mantiene le associazioni correnti con gli oggetti ma limita l’applicazione del tag ad altri oggetti.  I tag archiviati sono nascosti nel selettore tag. |
| Oggetto | Un Experience Cloud di elemento a cui può essere applicato un tag.  Esempi: Segmento, Percorso, set di dati. |
| Tag | I tag sono metadati e possono essere pensati come parole chiave che possono essere collegate a un segmento, a un set di dati, a un percorso o ad altri oggetti per consentire le ricerche per trovare quell’oggetto e gli oggetti correlati. |
| Categoria tag | Assegnare tag alle categorie in set significativi per fornire un contesto più ampio o descrivere lo scopo del tag.  Gli amministratori gestiscono le categorie di tag e i tag all’interno delle categorie. |
| Tag non categorizzato | Un nuovo tag creato in linea in cui vengono applicati i tag. Questi tag possono essere creati e applicati da qualsiasi utente, ma non sono associati a una categoria.  Gli amministratori possono spostare questi tag in una categoria per allinearli ad altri tag simili. |

## Inventario dei tag

La gestione dei tag e delle categorie tramite l’inventario dei tag è disponibile nella navigazione Experience Platform e Journey Optimizer. Le modifiche ai tag nell’inventario si riflettono in tutti gli oggetti che supportano i tag. Tutti gli utenti possono accedere e sfogliare l’inventario dei tag, ma la gestione dei tag è limitata agli amministratori di sistema e di prodotto.

L’inventario dei tag presenta tre livelli di gerarchia che consentono agli utenti di gestire categorie di tag, tag all’interno di una categoria e singoli tag. Quando gestisci un singolo tag, gli utenti possono visualizzare e navigare verso qualsiasi oggetto a cui è attualmente applicato il tag.

### Categorie di tag

Categorie raggruppa i tag in set significativi per fornire un contesto più ampio o descrivere lo scopo del tag. Su qualsiasi tag con una categoria, il nome della categoria seguito da due punti precede il nome del tag.

Quando si utilizzano le categorie di tag, è possibile effettuare le seguenti operazioni:

* [Creare una categoria di tag](./ui/tags-categories.md#create-tag-category)
* [Modifica categoria tag](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Elimina categoria tag](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Gestione dei tag in una categoria

>[!NOTE]
>
>Per gestire i tag, ad Experience Cloud, devi essere un amministratore di sistema o un amministratore di prodotto per Adobe Experience Platform per la tua organizzazione, che dispone di una sottoscrizione ad Experience Cloud.

All’interno di una categoria (o del gruppo &quot;Non categorizzato&quot; predefinito), puoi creare e gestire i tag. Durante la gestione dei tag è possibile effettuare le seguenti operazioni:

* [Creare un tag](./ui/managing-tags.md#create-a-tag-create-tag)
* [Modificare un tag](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Spostare un tag tra categorie](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Archiviare un tag](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Ripristinare un tag archiviato](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Eliminare un tag](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Visualizzare gli oggetti con tag](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
