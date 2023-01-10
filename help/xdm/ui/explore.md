---
keywords: Experience Platform;home;argomenti popolari;interfaccia utente;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;esplorare;classe;gruppo di campi;tipo di dati;schema;
solution: Experience Platform
title: Esplorare le risorse dello schema nell’interfaccia utente
description: Scopri come esplorare gli schemi, le classi, i gruppi di campi dello schema e i tipi di dati esistenti nell’interfaccia utente di Experience Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# Esplorare le risorse dello schema nell’interfaccia utente

In Adobe Experience Platform, tutte le risorse dello schema Experience Data Model (XDM) sono memorizzate in [!DNL Schema Library], incluse le risorse standard fornite da risorse Adobi e personalizzate definite dall’organizzazione. Nell’interfaccia utente di Experience Platform, è possibile visualizzare la struttura e i campi di qualsiasi schema, classe, gruppo di campi o tipo di dati esistente nella [!DNL Schema Library]. Questa funzione è particolarmente utile nella pianificazione e preparazione dell’acquisizione dei dati, in quanto l’interfaccia utente fornisce informazioni sui tipi di dati previsti e sui casi d’uso di ciascun campo fornito da queste risorse XDM.

Questa esercitazione descrive i passaggi necessari per esplorare gli schemi, le classi, i gruppi di campi e i tipi di dati esistenti nell’interfaccia utente di Experience Platform.

## Cercare una risorsa schema {#lookup}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nella navigazione a sinistra. La [!UICONTROL Schemi] l&#39;area di lavoro fornisce **[!UICONTROL Sfoglia]** scheda per esplorare tutti gli schemi dell’organizzazione, insieme a schede dedicate aggiuntive per l’esplorazione **[!UICONTROL Classi]**, **[!UICONTROL Gruppi di campi]** e **[!UICONTROL Tipi di dati]** rispettivamente.

![](../images/ui/explore/tabs.png)

Icona del filtro (![Icona filtro](../images/ui/explore/icon.png)) mostra i controlli nella barra a sinistra per limitare i risultati elencati. I controlli visualizzati variano a seconda del tipo di risorsa elencata.

Ad esempio, per filtrare l’elenco in modo da visualizzare solo i tipi di dati standard forniti dall’Adobe, selezionare **[!UICONTROL Tipo di dati]** e **[!UICONTROL Adobe]** in **[!UICONTROL Tipo]** e **[!UICONTROL Proprietario]** sezioni, rispettivamente.

La **[!UICONTROL Incluso nel profilo]** consente di filtrare i risultati per visualizzare solo le risorse utilizzate negli schemi abilitati per l’utilizzo in [Profilo cliente in tempo reale](../../profile/home.md).

![](../images/ui/explore/filter.png)

Quando inserisci risorse in **[!UICONTROL Classi]**, **[!UICONTROL Gruppi di campi]** oppure **[!UICONTROL Tipi di dati]** schede, puoi selezionare **[!UICONTROL Adobe]** mostrare solo risorse standard o **[!UICONTROL Cliente]** per mostrare solo le risorse create dall’organizzazione.

![](../images/ui/explore/filter-data-type.png)

È inoltre possibile utilizzare la barra di ricerca per limitare ulteriormente i risultati.

![](../images/ui/explore/search.png)

Le risorse visualizzate nei risultati della ricerca vengono ordinate prima per corrispondenza del titolo e poi per corrispondenza della descrizione. A sua volta, più parole corrispondono in una di queste categorie, più la risorsa viene visualizzata nell’elenco.

Dopo aver trovato la risorsa da esplorare, selezionane il nome dall’elenco per visualizzarne la struttura nell’area di lavoro.

## Esplorare una risorsa XDM nell’area di lavoro {#explore}

Dopo aver selezionato una risorsa, la relativa struttura si apre nell’area di lavoro.

![](../images/ui/explore/canvas.png)

Tutti i campi di tipo oggetto contenenti proprietà secondarie vengono compressi per impostazione predefinita quando vengono visualizzati per la prima volta nell’area di lavoro. Per visualizzare le proprietà secondarie di un campo, seleziona l’icona accanto al nome corrispondente.

![](../images/ui/explore/field-expand.png)

### Campi generati dal sistema {#system-fields}

Alcuni nomi di campo sono preceduti da un carattere di sottolineatura, ad esempio `_repo` e `_id`. Questi rappresentano segnaposto per i campi che il sistema genererà e assegnerà automaticamente durante l’acquisizione dei dati.

Di conseguenza, la maggior parte di questi campi deve essere esclusa dalla struttura dei dati durante l’acquisizione in Platform. L&#39;eccezione principale a questa regola è la [`_{TENANT_ID}` field](../api/getting-started.md#know-your-tenant_id), in cui tutti i campi XDM creati nell’organizzazione devono essere spazi dei nomi.

### Tipi di dati {#data-types}

Per ciascun campo mostrato nell’area di lavoro, accanto al nome viene visualizzato il tipo di dati corrispondente, che indica immediatamente il tipo di dati che il campo prevede di acquisire.

![](../images/ui/explore/data-types.png)

Qualsiasi tipo di dati aggiunto con parentesi quadre (`[]`) rappresenta un array di quel particolare tipo di dati. Ad esempio, un tipo di dati di **[!UICONTROL Stringa]\[]** indica che il campo richiede una matrice di valori stringa. Tipo di dati **[!UICONTROL Elemento di pagamento]\[]** indica un array di oggetti conformi al [!UICONTROL Elemento di pagamento] tipo di dati.

Se un campo array è basato su un tipo di oggetto, è possibile selezionarne l’icona nell’area di lavoro per visualizzare gli attributi previsti per ogni elemento array.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Proprietà campo] {#field-properties}

Quando selezioni il nome di un campo nell’area di lavoro, la barra a destra si aggiorna e mostra i dettagli di quel campo in **[!UICONTROL Proprietà campo]**. È possibile includere una descrizione del caso di utilizzo previsto del campo, i valori predefiniti, i pattern, i formati, indipendentemente dal fatto che il campo sia obbligatorio o meno e altro ancora.

![](../images/ui/explore/field-properties.png)

Se il campo che stai analizzando è un campo enum, nella barra a destra vengono visualizzati anche i valori accettabili che il campo prevede di ricevere.

![](../images/ui/explore/enum-field.png)

### Campi di identità {#identity}

Quando si esaminano gli schemi che contengono campi di identità, questi campi sono elencati nella barra a sinistra sotto la classe o il gruppo di campi che li fornisce allo schema. Seleziona il nome del campo di identità nella barra a sinistra per visualizzare il campo nell’area di lavoro, indipendentemente dalla sua profondità di nidificazione.

I campi di identità sono evidenziati nell’area di lavoro con l’icona dell’impronta digitale (![Immagine icona impronta digitale](../images/ui/explore/identity-symbol.png)). Se selezioni il nome del campo di identità, puoi visualizzare informazioni aggiuntive, ad esempio [spazio dei nomi identità](../../identity-service/namespaces.md) e se il campo è o meno l&#39;identità principale dello schema.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Consulta la guida su [definizione dei campi di identità](./fields/identity.md) per ulteriori informazioni sui campi di identità e sul loro rapporto con i servizi della piattaforma a valle.

### Campi di relazione {#relationship}

Se stai analizzando uno schema contenente un campo di relazione, il campo verrà elencato nella barra a sinistra sotto **[!UICONTROL Relazioni]**. Seleziona il nome del campo di relazione nella barra a sinistra per visualizzare il campo nell’area di lavoro, indipendentemente da quanto è nidificato.

I campi di relazione vengono inoltre evidenziati in modo univoco nell’area di lavoro, mostrando il nome dello schema di destinazione a cui fa riferimento il campo. Se selezioni il nome del campo relazione, puoi visualizzare lo spazio dei nomi identità dell’identità principale dello schema di destinazione nella barra a destra.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Guarda l’esercitazione su [creazione di una relazione nell’interfaccia utente](../tutorials/relationship-ui.md) per ulteriori informazioni sull’utilizzo delle relazioni negli schemi XDM.

## Passaggi successivi

Questo documento illustra come esplorare le risorse XDM esistenti nell’interfaccia utente di Experience Platform. Per ulteriori informazioni sulle diverse funzioni di [!UICONTROL Schemi] area di lavoro e [!DNL Schema Editor], vedi [[!UICONTROL Schemi] panoramica dell&#39;area di lavoro](./overview.md).
