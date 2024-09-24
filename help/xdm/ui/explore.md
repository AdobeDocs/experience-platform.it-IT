---
keywords: Experience Platform;home;argomenti popolari;ui;interfaccia utente;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;data model;esplorare;classe;gruppo di campi;tipo di dati;schema;
solution: Experience Platform
title: Esplorare le risorse dello schema nell’interfaccia utente
description: Scopri come esplorare schemi, classi, gruppi di campi di schema e tipi di dati esistenti nell’interfaccia utente di Experience Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 5f9fdc9eff4d8bba049c03058d24e80e9b89e953
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 0%

---

# Esplorare le risorse dello schema nell’interfaccia utente

In Adobe Experience Platform, tutte le risorse dello schema Experience Data Model (XDM) sono memorizzate in [!DNL Schema Library], incluse le risorse standard fornite da Adobe e le risorse personalizzate definite dall&#39;organizzazione. Nell&#39;interfaccia utente di Experience Platform è possibile visualizzare la struttura e i campi di qualsiasi schema, classe, gruppo di campi o tipo di dati esistente in [!DNL Schema Library]. Questa funzione è particolarmente utile durante la pianificazione e la preparazione per l’acquisizione dei dati, in quanto l’interfaccia utente fornisce informazioni sui tipi di dati previsti e sui casi di utilizzo di ciascun campo fornito da queste risorse XDM.

Questo tutorial illustra i passaggi necessari per esplorare schemi, classi, gruppi di campi e tipi di dati esistenti nell’interfaccia utente di Experience Platform.

## Cercare una risorsa schema {#lookup}

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nell&#39;area di navigazione a sinistra. L&#39;area di lavoro [!UICONTROL Schemi] fornisce una scheda **[!UICONTROL Sfoglia]** per esplorare tutti gli schemi dell&#39;organizzazione, insieme a schede dedicate aggiuntive per esplorare rispettivamente **[!UICONTROL Classi]**, **[!UICONTROL Gruppi di campi]**, **[!UICONTROL Tipi di dati]** e **[!UICONTROL Relazioni]**.

![Area di lavoro Schemi con diverse schede evidenziate.](../images/ui/explore/tabs.png)

L&#39;icona del filtro (![Immagine icona filtro](/help/images/icons/filter.png)) rivela i controlli nella barra a sinistra per limitare i risultati elencati. I filtri delle risorse sono disponibili per schemi e relazioni rispettivamente nelle schede **[!UICONTROL Sfoglia]** e **[!UICONTROL Relazioni]**.

Nella scheda [!UICONTROL Sfoglia] dell&#39;area di lavoro [!UICONTROL Schemi], puoi filtrare l&#39;inventario degli schemi. Utilizza l&#39;opzione **[!UICONTROL Incluso nel profilo]** per visualizzare solo gli schemi abilitati per l&#39;utilizzo in [Profilo cliente in tempo reale](../../profile/home.md). Utilizza l&#39;interruttore **[!UICONTROL Mostra schemi ad hoc]** per filtrare l&#39;elenco di schemi creati con campi con spazio dei nomi utilizzabili solo da un singolo set di dati.

![Scheda [!UICONTROL Sfoglia] dell&#39;area di lavoro [!UICONTROL Schemi] con il pannello Filtri evidenziato.](../images/ui/explore/filters.png)

Nella scheda [!UICONTROL Relazione] dell&#39;area di lavoro [!UICONTROL Schemi] è possibile filtrare l&#39;elenco delle relazioni in base a quattro criteri. I filtri includono [!UICONTROL schema Source], [!UICONTROL schema di destinazione], [!UICONTROL classe Source] e la [!UICONTROL classe Destination]. La tabella seguente fornisce una descrizione dei filtri.

| Filtro | Descrizione |
|-----------------------------------|------------|
| [!UICONTROL Schema Source] | Per visualizzare tutte le relazioni in cui lo schema selezionato è il punto iniziale o &quot;sorgente&quot;, selezionare uno schema dal menu a discesa [!UICONTROL Schema Source]. |
| [!UICONTROL Schema di destinazione] | Per visualizzare tutte le relazioni in cui lo schema selezionato è la destinazione o &quot;destinazione&quot;, selezionare uno schema dal menu a discesa [!UICONTROL Schema di destinazione]. |
| [!UICONTROL Classe Source] | Per filtrare le relazioni in base alla classe dello schema di avvio, selezionare una classe dal menu a discesa [!UICONTROL Classe Source]. |
| [!UICONTROL Classe di destinazione] | Per visualizzare le relazioni che terminano con gli schemi di una classe specifica, selezionare una classe dal menu a discesa [!UICONTROL Classe di destinazione]. |

{style="table-layout:auto"}

![Scheda Relazioni con la sezione dei filtri evidenziata.](../images/ui/explore/relationships-filter.png)

Puoi anche utilizzare la barra di ricerca per limitare ulteriormente i risultati.

![Scheda Sfoglia dell&#39;area di lavoro Schemi con il campo di ricerca evidenziato.](../images/ui/explore/search.png)

Le risorse visualizzate nei risultati della ricerca vengono ordinate prima in base alle corrispondenze titolo, quindi in base alle corrispondenze descrizione. A sua volta, più le parole corrispondono in una di queste categorie, più la risorsa viene visualizzata nell’elenco.

Una volta trovata la risorsa da esplorare, selezionane il nome dall’elenco per visualizzarne la struttura nell’area di lavoro.

## Esplorare una risorsa XDM nell’area di lavoro {#explore}

Dopo aver selezionato una risorsa, la sua struttura si apre nell’area di lavoro.

![Area di lavoro del tipo di dati che visualizza il tipo di dati di Commerce.](../images/ui/explore/canvas.png)

Tutti i campi di tipo oggetto contenenti sottoproprietà vengono compressi per impostazione predefinita quando vengono visualizzati per la prima volta nell’area di lavoro. Per visualizzare le sottoproprietà di qualsiasi campo, seleziona l’icona accanto al nome.

![Area di lavoro del tipo di dati con campi espansi e sottoproprietà evidenziate.](../images/ui/explore/field-expand.png)

### Indicatore di classe e gruppo di campi standard {#standard-class-and-field-group-indicator}

Nell&#39;Editor schema, le classi e i gruppi di campi standard (generati da Adobi) sono indicati con l&#39;icona lucchetto (![Un&#39;icona lucchetto.](/help/images/icons/lock-closed.png). Il lucchetto viene visualizzato nella barra a sinistra accanto al nome della classe o del gruppo di campi, nonché accanto a qualsiasi campo nel diagramma dello schema che fa parte di una risorsa generata dal sistema.

![Editor schema con l&#39;icona lucchetto evidenziata](../images/ui/explore/schema-editor-padlock-icon.png)

Consulta la documentazione [Aggiungere campi personalizzati ai gruppi di campi standard](./resources/schemas.md). Impossibile modificare una classe standard.

### Campi generati dal sistema {#system-fields}

Alcuni nomi di campo sono preceduti da un trattino basso, ad esempio `_repo` e `_id`. Questi rappresentano segnaposto per i campi che il sistema genera e assegna automaticamente quando i dati vengono acquisiti.

Di conseguenza, la maggior parte di questi campi deve essere esclusa dalla struttura dei dati al momento dell’acquisizione in Platform. L&#39;eccezione principale a questa regola è il campo [`_{TENANT_ID}`](../api/getting-started.md#know-your-tenant_id), in cui tutti i campi XDM creati nell&#39;organizzazione devono essere namespace.

### Tipi di dati {#data-types}

Per ogni campo visualizzato nell’area di lavoro, accanto al nome viene visualizzato il tipo di dati corrispondente, che indica subito il tipo di dati previsto dal campo per l’acquisizione.

![Il tipo di dati Indirizzo postale visualizzato nell&#39;area di lavoro con i tipi di dati associati evidenziati.](../images/ui/explore/data-types.png)

Qualsiasi tipo di dati aggiunto con parentesi quadre (`[]`) rappresenta una matrice di quel particolare tipo di dati. Ad esempio, un tipo di dati **[!UICONTROL String]\[]** indica che il campo richiede una matrice di valori stringa. Un tipo di dati **[!UICONTROL Elemento pagamento]\[]** indica un array di oggetti conformi al tipo di dati [!UICONTROL Elemento pagamento].

Se un campo array è basato su un tipo di oggetto, è possibile selezionarne l&#39;icona nell&#39;area di lavoro per visualizzare gli attributi previsti per ogni elemento array.

![Oggetto nell&#39;area di lavoro con campo di matrice evidenziato e attributi previsti per ogni elemento di matrice visualizzato.](../images/ui/explore/array-type.png)

### [!UICONTROL Proprietà campo] {#field-properties}

Quando selezioni il nome di un campo nell&#39;area di lavoro, la barra a destra si aggiorna per mostrare i dettagli di quel campo in **[!UICONTROL Proprietà campo]**. Può includere una descrizione del caso d’uso previsto del campo, valori predefiniti, modelli, formati, se il campo è obbligatorio o meno e altro ancora.

![Campo selezionato dal tipo di dati Commerce con le proprietà del campo evidenziate.](../images/ui/explore/field-properties.png)

Se il campo che stai esaminando è un campo enum, nella barra a destra verranno visualizzati anche i valori accettabili che il campo si aspetta di ricevere.

![Editor schema con un campo selezionato e valori enum e nomi visualizzati evidenziati nella barra delle proprietà del campo.](../images/ui/explore/enum-field.png)

### Campi di identità {#identity}

Durante l’analisi degli schemi che contengono campi di identità, questi campi sono elencati nella barra a sinistra sotto la classe o il gruppo di campi che li fornisce allo schema. Seleziona il nome del campo di identità nella barra a sinistra per visualizzare il campo nell’area di lavoro, indipendentemente dalla profondità di nidificazione.

I campi di identità sono evidenziati nell&#39;area di lavoro con un&#39;icona di impronta digitale (![Immagine icona impronta digitale](/help/images/icons/identity-service.png)). Se si seleziona il nome del campo di identità, è possibile visualizzare ulteriori informazioni, ad esempio lo spazio dei nomi [identità](../../identity-service/features/namespaces.md) e se il campo rappresenta o meno l&#39;identità primaria dello schema.

![Editor schema con l&#39;identità dello schema evidenziata nella barra a sinistra, il campo evidenziato nel diagramma schema e lo spazio dei nomi dell&#39;identità evidenziato nelle proprietà del campo.](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Per ulteriori informazioni sui campi di identità e sulla loro relazione con i servizi Platform a valle, consulta la guida su [definizione dei campi di identità](./fields/identity.md).

### Campi di relazione {#relationship}

Se stai esaminando uno schema che contiene un campo di relazione, il campo verrà elencato nella barra a sinistra in **[!UICONTROL Relazioni]**. Seleziona il nome del campo relazione nella barra a sinistra per visualizzare il campo nell’area di lavoro, indipendentemente dalla profondità di nidificazione. I campi di relazione vengono inoltre evidenziati in modo univoco nell’area di lavoro, mostrando il nome dello schema di riferimento a cui è collegato il campo. Per le organizzazioni con funzionalità B2B, in questi casi è possibile scrivere nomi di relazione personalizzati che verranno visualizzati nell’area di lavoro.

![Editor schema con il campo relazione e la relazione Modifica evidenziati.](../images/ui/explore/relationship-field.png)

Per visualizzare lo spazio dei nomi dell&#39;identità primaria dello schema di riferimento, selezionare il campo relazione, quindi **[!UICONTROL Modifica relazione]** nella barra laterale [!UICONTROL Proprietà campo]. I parametri per la relazione vengono visualizzati nella finestra di dialogo [!UICONTROL Modifica relazione] visualizzata.

![Viene visualizzata la finestra di dialogo Modifica relazione con i parametri di relazione.](../images/ui/explore/edit-relationship-dialog.png)

Per ulteriori informazioni sull&#39;utilizzo delle relazioni negli schemi XDM, consulta il tutorial su [creazione di una relazione nell&#39;interfaccia utente](../tutorials/relationship-ui.md).

## Passaggi successivi

Questo documento illustra come esplorare le risorse XDM esistenti nell’interfaccia utente di Experience Platform. Per ulteriori informazioni sulle diverse funzionalità dell&#39;area di lavoro [!UICONTROL Schemi] e [!DNL Schema Editor], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemi]](./overview.md).
