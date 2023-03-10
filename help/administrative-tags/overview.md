---
keywords: Experience Platform;home;argomenti popolari;tag unificati;tag;
title: Panoramica dei tag unificati (Beta)
description: Questo documento fornisce informazioni sui tag unificati in Adobe Experience Platform
source-git-commit: 6f9787909b8155d2bf032b4a42483f2cb4d44eb4
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# Panoramica dei tag unificati (Beta)

>[!IMPORTANT]
>
>I tag unificati sono in versione beta. Per lasciare un feedback, fai clic sul pulsante nella parte superiore della pagina di amministrazione dei tag.

I tag sono una funzionalità di Adobe Experience Platform che consente agli amministratori di gestire le tassonomie dei metadati al fine di classificare gli oggetti business per semplificare l’individuazione e la classificazione. I tag sono metadati che possono essere considerati parole chiave da associare a un segmento, un set di dati, un percorso o altri oggetti per consentire alle ricerche di trovare l’oggetto e gli oggetti correlati. I tag sono classificati in due tipi: categorizzati e non categorizzati.

Per fornire più contesto e definire lo scopo di un tag, le categorie organizzano i tag in set utili. Un amministratore definisce i tag categorizzati disponibili per gli utenti da aggiungere agli oggetti. I nuovi tag che non contengono categorie possono essere creati anche in linea nei flussi di lavoro in cui vengono applicati i tag. Questi tag verranno visualizzati nella sezione senza categoria dell’inventario dei tag. I tag possono essere applicati sia dagli amministratori che dagli utenti, indipendentemente da chi li ha creati. Tutti i tipi di tag sono disponibili per la selezione quando si assegna un oggetto, si esegue una ricerca o si applica un filtro.

## Terminologia dei tag

L’assegnazione tag include i seguenti componenti:

| Terminologia | Definizione |
| --- | --- |
| Archiviato | Uno stato per un tag che mantiene le associazioni correnti con gli oggetti ma impedisce l&#39;applicazione del tag ad altri oggetti.  I tag archiviati sono nascosti dal selettore di tag. |
| Oggetto | Elemento di Experience Cloud a cui è possibile applicare un tag.  Esempi: Segmento, Percorso, Set di dati. |
| Tag | I tag sono metadati e possono essere considerati come parole chiave che possono essere associate a un segmento, a un set di dati, a un percorso o ad altri oggetti per consentire alle ricerche di trovare l’oggetto e gli oggetti correlati. |
| Categoria tag | Categorie di tag raggruppa i tag in set significativi per fornire maggiore contesto o descrivere lo scopo del tag.  Gli amministratori gestiscono le categorie e i tag all’interno delle categorie. |
| Tag non categorizzato | Nuovo tag creato in linea in cui vengono applicati i tag. Possono essere creati e applicati da qualsiasi utente, ma non sono associati a una categoria.  Gli amministratori possono spostare questi tag in una categoria per allinearli ad altri tag simili. |

## Inventario dei tag

La gestione delle categorie e dei tag tramite l’inventario dei tag è disponibile nell’area di navigazione di Experience Platform e Journey Optimizer. Le modifiche apportate ai tag nell&#39;inventario vengono applicate a tutti gli oggetti che supportano i tag. Tutti gli utenti possono accedere e sfogliare l’inventario dei tag, ma la gestione dei tag è limitata agli amministratori di sistema e di prodotto.

L’inventario dei tag dispone di tre livelli gerarchici che consentono agli utenti di gestire categorie di tag, tag all’interno di una categoria e singoli tag. Durante la gestione di un singolo tag, gli utenti possono visualizzare e spostarsi su qualsiasi oggetto in cui tale tag è attualmente applicato.

### Categorie di tag

Le categorie raggruppano i tag in set significativi per fornire maggiore contesto o descrivere lo scopo del tag. Su qualsiasi tag con una categoria, il nome della categoria seguito da due punti precede il nome del tag.

Quando si utilizzano le categorie di tag, sono possibili le seguenti azioni:

* [Crea categoria tag](./ui/tags-categories.md#create-tag-category)
* [Modifica categoria tag](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Elimina categoria tag](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Gestione dei tag all’interno di una categoria

>[!NOTE]
>
>Per gestire i tag, ad Experience Cloud, è necessario essere un amministratore di sistema o un amministratore di prodotto per Adobe Experience Platform per la tua organizzazione, che dispone di una sottoscrizione a Experience Cloud.

All’interno di una categoria (o del gruppo predefinito &quot;Non categorizzato&quot;), puoi creare e gestire i tag. Durante la gestione dei tag sono possibili le seguenti azioni:

* [Creare un tag](./ui/managing-tags.md#create-a-tag-create-tag)
* [Modificare un tag](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Spostare un tag tra categorie](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Archiviare un tag](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Ripristinare un tag archiviato](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Eliminare un tag](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Visualizza oggetti con tag](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
