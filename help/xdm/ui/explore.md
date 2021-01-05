---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;explore;class;mixin;data type;schema;
solution: Experience Platform
title: Esplora risorse XDM nell'interfaccia utente
description: Scopri come esplorare gli schemi, le classi, i mixin e i tipi di dati esistenti nell'interfaccia utente del Experience Platform .
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: e5c5fea783aa4088d225f771905fa8b2098613cf
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---


# Esplora risorse XDM nell&#39;interfaccia utente

In Adobe Experience Platform, tutte le risorse di Experience Data Model (XDM) sono memorizzate in [!DNL Schema Library], incluse le risorse standard fornite da risorse  Adobe e personalizzate definite dall&#39;organizzazione. Nell&#39;interfaccia utente del Experience Platform , è possibile visualizzare la struttura e i campi di qualsiasi schema, classe, mixin o tipo di dati esistente in [!DNL Schema Library]. Questa funzione è particolarmente utile per la pianificazione e la preparazione dell&#39;inserimento dei dati, in quanto l&#39;interfaccia utente fornisce informazioni sui tipi di dati previsti e sui casi di utilizzo di ciascun campo fornito da queste risorse XDM.

Questa esercitazione illustra i passaggi necessari per esplorare gli schemi, le classi, i mixin e i tipi di dati esistenti nell&#39;interfaccia utente del Experience Platform .

## Cercare una risorsa XDM {#lookup}

Nell&#39;interfaccia utente della piattaforma, selezionate **[!UICONTROL Schemas]** nel menu di navigazione a sinistra. L&#39;area di lavoro [!UICONTROL Schemas] include una scheda **[!UICONTROL Browse]** per esplorare tutte le risorse XDM esistenti nell&#39;organizzazione, insieme a schede dedicate aggiuntive per l&#39;esplorazione specifica di **[!UICONTROL Classes]**, **[!UICONTROL Mixins]** e **[!UICONTROL Data types]**.

![](../images/ui/explore/tabs.png)

Nella scheda [!UICONTROL Browse] è possibile utilizzare l&#39;icona del filtro (![Immagine icona filtro](../images/ui/explore/icon.png)) per visualizzare i controlli nella barra a sinistra per limitare i risultati elencati.

Ad esempio, per filtrare l&#39;elenco in modo da visualizzare solo i tipi di dati standard forniti dal  Adobe, selezionare **[!UICONTROL Datatype]** e **[!UICONTROL Adobe]** rispettivamente nelle sezioni **[!UICONTROL Type]** e **[!UICONTROL Owner]**.

L&#39;interruttore **[!UICONTROL Included in Profile]** consente di filtrare i risultati per visualizzare solo le risorse utilizzate negli schemi che sono stati abilitati per l&#39;utilizzo in [Profilo cliente in tempo reale](../../profile/home.md).

![](../images/ui/explore/filter.png)

È inoltre possibile utilizzare la barra di ricerca per limitare i risultati alle risorse i cui nomi corrispondono alla query di ricerca.

![](../images/ui/explore/search.png)

Dopo aver trovato la risorsa da esplorare, selezionatene il nome dall’elenco per visualizzarne la struttura nell’area di lavoro.

## Esplora una risorsa XDM nell&#39;area di lavoro {#explore}

Dopo aver selezionato una risorsa, la sua struttura viene aperta nel quadro.

![](../images/ui/explore/canvas.png)

Per impostazione predefinita, tutti i campi di tipo oggetto contenenti proprietà secondarie vengono compressi quando vengono visualizzati per la prima volta nel quadro. Per visualizzare le proprietà secondarie di un campo, selezionare l&#39;icona accanto al nome.

![](../images/ui/explore/field-expand.png)

### Campi generati dal sistema {#system-fields}

Alcuni nomi di campo sono preceduti da un carattere di sottolineatura, ad esempio `_repo` e `_id`. Questi rappresentano segnaposto per i campi che il sistema genererà e assegnerà automaticamente durante l&#39;assimilazione dei dati.

Di conseguenza, la maggior parte di questi campi dovrebbe essere esclusa dalla struttura dei dati durante l&#39;assimilazione in Piattaforma. L&#39;eccezione principale a questa regola è il campo [`_{TENANT_ID}`](../api/getting-started.md#know-your-tenant_id), in cui tutti i campi XDM creati nell&#39;organizzazione devono essere denominati.

### Tipi di dati {#data-types}

Per ciascun campo mostrato nel quadro, il tipo di dati corrispondente è visualizzato accanto al nome corrispondente, indicando immediatamente il tipo di dati che il campo prevede di inserire.

![](../images/ui/explore/data-types.png)

Qualsiasi tipo di dati aggiunto con parentesi quadre (`[]`) rappresenta un array di quel particolare tipo di dati. Ad esempio, un tipo di dati di **[!UICONTROL String]\[]** indica che il campo prevede una matrice di valori stringa. Un tipo di dati di **[!UICONTROL Payment Item]\[]** indica un array di oggetti conformi al tipo di dati [!UICONTROL Payment Item].

Se un campo array è basato su un tipo di oggetto, è possibile selezionare la relativa icona nell&#39;area di lavoro per mostrare gli attributi previsti per ciascun elemento dell&#39;array.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

Quando si seleziona il nome di un campo nell&#39;area di lavoro, la barra laterale destra si aggiorna per visualizzare i dettagli relativi a tale campo in **[!UICONTROL Field properties]**. Questo può includere una descrizione del caso di utilizzo previsto del campo, valori predefiniti, pattern, formati, indipendentemente dal fatto che il campo sia o meno obbligatorio e altro ancora.

![](../images/ui/explore/field-properties.png)

Se il campo che si sta esaminando è un campo enum, nella barra a destra vengono visualizzati anche i valori accettabili che il campo prevede di ricevere.

![](../images/ui/explore/enum-field.png)

### Campi identità {#identity}

Quando si esaminano gli schemi che contengono campi di identità, questi campi sono elencati nella barra a sinistra sotto la classe o il mixin che li fornisce allo schema. Selezionate il nome del campo di identità nella barra a sinistra per visualizzare il campo nell’area di lavoro, indipendentemente dalla profondità della sua nidificazione.

I campi di identità sono evidenziati nel quadro con l&#39;icona dell&#39;impronta digitale (![Immagine icona dell&#39;impronta digitale](../images/ui/explore/identity-symbol.png)). Se si seleziona il nome del campo di identità, è possibile visualizzare informazioni aggiuntive, ad esempio [identity namespace](../../identity-service/namespaces.md) e se il campo è o meno l&#39;identità principale dello schema.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Per ulteriori informazioni sui campi di identità e sulla loro relazione con i servizi della piattaforma a valle, consulta la guida sulla [definizione dei campi di identità](./fields/identity.md).

### Campi di relazione {#relationship}

Se si sta esaminando uno schema che contiene un campo di relazione, il campo verrà elencato nella barra a sinistra sotto **[!UICONTROL Relationships]**. Selezionate il nome del campo della relazione nella barra a sinistra per visualizzare il campo nel quadro, indipendentemente dal livello di nidificazione.

I campi delle relazioni sono inoltre evidenziati in modo univoco nel quadro, mostrando il nome dello schema di destinazione a cui fa riferimento il campo. Se si seleziona il nome del campo relazione, è possibile visualizzare lo spazio nomi identità dell&#39;identità primaria dello schema di destinazione nella barra a destra.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;utilizzo delle relazioni negli schemi XDM, vedere l&#39;esercitazione su [creazione di una relazione nell&#39;interfaccia utente](../tutorials/create-schema-ui.md).

## Passaggi successivi

Questo documento illustra come esplorare le risorse XDM esistenti nell&#39;interfaccia utente del Experience Platform . Per ulteriori informazioni sulle diverse funzioni dell&#39;area di lavoro [!UICONTROL Schemas] e [!DNL Schema Editor], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemas]](./overview.md).