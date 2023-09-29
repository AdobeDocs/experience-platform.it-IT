---
keywords: Experience Platform;home;argomenti popolari;ui;interfaccia utente;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;data model;esplorare;classe;gruppo di campi;tipo di dati;schema;
solution: Experience Platform
title: Esplorare le risorse dello schema nell’interfaccia utente
description: Scopri come esplorare schemi, classi, gruppi di campi di schema e tipi di dati esistenti nell’interfaccia utente di Experienci Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: f08aa017b7f971a54197b95023e9331832ecb7f1
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---

# Esplorare le risorse dello schema nell’interfaccia utente

In Adobe Experience Platform, tutte le risorse dello schema Experience Data Model (XDM) sono memorizzate nel [!DNL Schema Library], incluse le risorse standard fornite da Adobe e le risorse personalizzate definite dall’organizzazione. Nell’interfaccia utente di Experienci Platform, puoi visualizzare la struttura e i campi di qualsiasi schema, classe, gruppo di campi o tipo di dati esistente in [!DNL Schema Library]. Questa funzione è particolarmente utile durante la pianificazione e la preparazione per l’acquisizione dei dati, in quanto l’interfaccia utente fornisce informazioni sui tipi di dati previsti e sui casi di utilizzo di ciascun campo fornito da queste risorse XDM.

Questo tutorial illustra i passaggi necessari per esplorare schemi, classi, gruppi di campi e tipi di dati esistenti nell’interfaccia utente di Experienci Platform.

## Cercare una risorsa schema {#lookup}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nel menu di navigazione a sinistra. Il [!UICONTROL Schemi] workspace fornisce un **[!UICONTROL Sfoglia]** per esplorare tutti gli schemi dell’organizzazione, insieme a schede dedicate aggiuntive per l’esplorazione **[!UICONTROL Classi]**, **[!UICONTROL Gruppi di campi]**, e **[!UICONTROL Tipi di dati]** rispettivamente.

![](../images/ui/explore/tabs.png)

Icona del filtro (![Immagine icona filtro](../images/ui/explore/icon.png)) mostra i controlli nella barra a sinistra per limitare i risultati elencati. I controlli visualizzati variano a seconda del tipo di risorsa elencata.

Ad esempio, per filtrare l’elenco in modo da mostrare solo i tipi di dati standard forniti dall’Adobe, seleziona **[!UICONTROL Tipo di dati]** e **[!UICONTROL Adobe]** sotto **[!UICONTROL Tipo]** e **[!UICONTROL Proprietario]** sezioni, rispettivamente.

Il **[!UICONTROL Incluso nel profilo]** consente di filtrare i risultati in modo da visualizzare solo le risorse utilizzate negli schemi che sono stati abilitati per l’utilizzo in [Profilo cliente in tempo reale](../../profile/home.md). Il **[!UICONTROL Mostra schemi ad hoc]** attiva/disattiva filtra l’elenco degli schemi creati con campi con namespace utilizzabili solo da un singolo set di dati.

![Il [!UICONTROL Schemi] workspace [!UICONTROL Sfoglia] con il pannello filtri evidenziato.](../images/ui/explore/filter.png)

Quando si elencano le risorse in **[!UICONTROL Classi]**, **[!UICONTROL Gruppi di campi]**, o **[!UICONTROL Tipi di dati]** schede, è possibile selezionare **[!UICONTROL Adobe]** per visualizzare solo le risorse standard o **[!UICONTROL Cliente]** per visualizzare solo le risorse create dall’organizzazione.

![](../images/ui/explore/filter-data-type.png)

Puoi anche utilizzare la barra di ricerca per limitare ulteriormente i risultati.

![](../images/ui/explore/search.png)

Le risorse visualizzate nei risultati della ricerca vengono ordinate prima in base alle corrispondenze titolo, quindi in base alle corrispondenze descrizione. A sua volta, più le parole corrispondono in una di queste categorie, più la risorsa viene visualizzata nell’elenco.

Una volta trovata la risorsa da esplorare, selezionane il nome dall’elenco per visualizzarne la struttura nell’area di lavoro.

## Esplorare una risorsa XDM nell’area di lavoro {#explore}

Dopo aver selezionato una risorsa, la sua struttura si apre nell’area di lavoro.

![](../images/ui/explore/canvas.png)

Tutti i campi di tipo oggetto contenenti sottoproprietà vengono compressi per impostazione predefinita quando vengono visualizzati per la prima volta nell’area di lavoro. Per visualizzare le sottoproprietà di qualsiasi campo, seleziona l’icona accanto al nome.

![](../images/ui/explore/field-expand.png)

### Campi generati dal sistema {#system-fields}

Alcuni nomi di campo sono preceduti da un trattino basso, ad esempio `_repo` e `_id`. Questi rappresentano segnaposto per i campi che il sistema genera e assegna automaticamente quando i dati vengono acquisiti.

Di conseguenza, la maggior parte di questi campi deve essere esclusa dalla struttura dei dati al momento dell’acquisizione in Platform. L&#39;eccezione principale a questa regola è la [`_{TENANT_ID}` campo](../api/getting-started.md#know-your-tenant_id), in cui tutti i campi XDM creati nell’organizzazione devono essere denominati.

### Tipi di dati {#data-types}

Per ogni campo visualizzato nell’area di lavoro, accanto al nome viene visualizzato il tipo di dati corrispondente, che indica subito il tipo di dati previsto dal campo per l’acquisizione.

![](../images/ui/explore/data-types.png)

Qualsiasi tipo di dati aggiunto con parentesi quadre (`[]`) rappresenta un array di quel particolare tipo di dati. Ad esempio, un tipo di dati **[!UICONTROL Stringa]\[]** indica che il campo richiede una matrice di valori stringa. Tipo di dati di **[!UICONTROL Voce di pagamento]\[]** indica un array di oggetti conformi al [!UICONTROL Voce di pagamento] tipo di dati.

Se un campo array è basato su un tipo di oggetto, è possibile selezionarne l&#39;icona nell&#39;area di lavoro per visualizzare gli attributi previsti per ogni elemento array.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Proprietà campo] {#field-properties}

Quando selezioni il nome di qualsiasi campo nell’area di lavoro, la barra a destra si aggiorna per mostrare i dettagli di quel campo in **[!UICONTROL Proprietà campo]**. Può includere una descrizione del caso d’uso previsto del campo, valori predefiniti, modelli, formati, se il campo è obbligatorio o meno e altro ancora.

![](../images/ui/explore/field-properties.png)

Se il campo che stai esaminando è un campo enum, nella barra a destra verranno visualizzati anche i valori accettabili che il campo si aspetta di ricevere.

![](../images/ui/explore/enum-field.png)

### Campi di identità {#identity}

Durante l’analisi degli schemi che contengono campi di identità, questi campi sono elencati nella barra a sinistra sotto la classe o il gruppo di campi che li fornisce allo schema. Seleziona il nome del campo di identità nella barra a sinistra per visualizzare il campo nell’area di lavoro, indipendentemente dalla profondità di nidificazione.

I campi di identità sono evidenziati nell’area di lavoro con l’icona di un’impronta digitale (![Immagine icona impronta digitale](../images/ui/explore/identity-symbol.png)). Se selezioni il nome del campo di identità, puoi visualizzare informazioni aggiuntive come [spazio dei nomi delle identità](../../identity-service/namespaces.md) e se il campo rappresenta o meno l’identità primaria dello schema.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Consulta la guida su [definizione dei campi di identità](./fields/identity.md) per ulteriori informazioni sui campi di identità e sulla loro relazione con i servizi Platform a valle.

### Campi di relazione {#relationship}

Se stai esaminando uno schema che contiene un campo di relazione, il campo verrà elencato nella barra a sinistra in **[!UICONTROL Relazioni]**. Seleziona il nome del campo relazione nella barra a sinistra per visualizzare il campo nell’area di lavoro, indipendentemente dalla profondità di nidificazione.

I campi di relazione vengono inoltre evidenziati in modo univoco nell’area di lavoro, mostrando il nome dello schema di riferimento a cui è collegato il campo. Se selezioni il nome del campo relazione, puoi visualizzare lo spazio dei nomi delle identità dell’identità principale dello schema di riferimento nella barra a destra.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Guarda il tutorial su [creazione di una relazione nell’interfaccia utente](../tutorials/relationship-ui.md) per ulteriori informazioni sull’utilizzo delle relazioni negli schemi XDM.

## Passaggi successivi

Questo documento illustra come esplorare le risorse XDM esistenti nell’interfaccia utente di Experienci Platform. Per ulteriori informazioni sulle diverse funzioni del [!UICONTROL Schemi] workspace e [!DNL Schema Editor], vedere [[!UICONTROL Schemi] panoramica di workspace](./overview.md).
