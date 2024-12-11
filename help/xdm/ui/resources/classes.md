---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;data model;ui;workspace;class;classes;
solution: Experience Platform
title: Creare e modificare le classi nell’interfaccia utente
description: Scopri come creare e modificare le classi nell’interfaccia utente di Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 02b709c01347c1d03f870132dff437b97f239a9c
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 5%

---

# Creare e modificare le classi nell’interfaccia utente {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Filtro di classe personalizzato o standard"
>abstract="L’elenco delle classi disponibili viene prefiltrato in base alla modalità di creazione. Selezionare il pulsante di opzione per scegliere tra le opzioni Standard e Personalizzato. L’opzione Standard mostra le entità create da Adobe e include sia le classi Profilo individuale XDM che Evento esperienza XDM. L’opzione Personalizzato consente di visualizzare le entità create all’interno dell’organizzazione. Per ulteriori informazioni sulla creazione e la modifica delle classi, consulta la documentazione."

In Adobe Experience Platform, la classe di uno schema definisce gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Inoltre, le classi descrivono il minor numero di proprietà comuni che tutti gli schemi basati su tale classe dovrebbero includere e forniscono un modo per unire più set di dati compatibili.

Adobe fornisce diverse classi standard (&quot;core&quot;) di Experience Data Model (XDM), tra cui [XDM Individual Profile](../../classes/individual-profile.md) e [XDM ExperienceEvent](../../classes/experienceevent.md). Oltre a queste classi principali, puoi anche creare classi personalizzate per descrivere casi d’uso più specifici per la tua organizzazione.

Questo documento fornisce una panoramica su come creare, modificare e gestire le classi personalizzate nell’interfaccia utente di Experience Platform.

## Prerequisiti {#prerequisites}

Questa guida richiede una buona conoscenza del sistema XDM. Per un&#39;introduzione al ruolo di XDM all&#39;interno dell&#39;ecosistema Experience Platform e alle [nozioni di base sulla composizione dello schema](../../schema/composition.md), consulta la [panoramica di XDM](../../home.md) per scoprire come le classi contribuiscono agli schemi XDM.

Sebbene non sia necessario per questa guida, è consigliabile seguire anche l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità dell&#39;Editor di schema.

## Introduzione {#getting-started}

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nell&#39;area di navigazione a sinistra per aprire l&#39;area di lavoro [!UICONTROL Schemi], quindi seleziona la scheda **[!UICONTROL Classi]**. Viene visualizzato un elenco delle classi disponibili.

![Numero di classi all&#39;interno della scheda [!UICONTROL Classi] dell&#39;area di lavoro [!UICONTROL Schemi] [!UICONTROL Classi] e [!UICONTROL Schemi] evidenziati.](../../images/ui/resources/classes/available-classes.png)

## Filtra classi {#filter}

L’elenco delle classi viene filtrato automaticamente in base alla modalità di creazione. L&#39;impostazione predefinita visualizza le classi definite da Adobe. Puoi anche filtrare l’elenco per visualizzare quelli creati dall’organizzazione. Selezionare il pulsante di opzione per scegliere tra le opzioni [!UICONTROL Standard] e [!UICONTROL Personalizzato]. L&#39;opzione [!UICONTROL Standard] mostra le entità create da Adobe e l&#39;opzione [!UICONTROL Custom] mostra le entità create all&#39;interno dell&#39;organizzazione.

![Scheda [!UICONTROL Classi] dell&#39;area di lavoro [!UICONTROL Schemi] con [!UICONTROL Standard] e [!UICONTROL Personalizzato] evidenziati.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Utilizza le funzionalità di ricerca per filtrare o trovare una classe in base al suo nome. Per ulteriori informazioni, consulta la guida sull&#39;[esplorazione delle risorse XDM](../explore.md).

## Crea una nuova classe {#create}

Esistono due metodi per creare una classe nell&#39;interfaccia utente di Platform, tramite **[!UICONTROL Crea classe]** o **[!UICONTROL Crea schema]**.

### Crea classe

Seleziona **[!UICONTROL Crea classe]** dalla scheda [!UICONTROL Classi] nell&#39;area di lavoro [!UICONTROL Schemi].

![Scheda [!UICONTROL Classi] dell&#39;area di lavoro [!UICONTROL Schemi] con [!UICONTROL Crea classe] evidenziata](../../images/ui/resources/classes/create-class.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Crea classe]. Immetti un [!UICONTROL Nome visualizzato] e una [!UICONTROL Descrizione] per la classe e scegli il comportamento previsto della classe con i pulsanti di scelta. Le classi possono essere di tipo [!UICONTROL Record] o [!UICONTROL Serie temporali]. Seleziona **[!UICONTROL Crea]** per confermare le scelte e tornare alla scheda [!UICONTROL Classi].

![La finestra di dialogo [!UICONTROL Crea classe] con [!UICONTROL Crea] evidenziata.](../../images/ui/resources/classes/create-class-dialog.png)

La classe creata è disponibile ed elencata nella visualizzazione [!UICONTROL Classi].

![Scheda [!UICONTROL Classi] dell&#39;area di lavoro [!UICONTROL Schemi] con la classe creata di recente evidenziata.](../../images/ui/resources/classes/new-class-listing.png)

### Crea schema

In alternativa, puoi creare una classe creando manualmente uno schema. Seleziona **[!UICONTROL Crea schema]** dalla scheda [!UICONTROL Classi] nell&#39;area di lavoro [!UICONTROL Schemi].

![Scheda [!UICONTROL Classi] dell&#39;area di lavoro [!UICONTROL Schemi] con [!UICONTROL Crea schema] evidenziato](../../images/ui/resources/classes/create-schema.png)

Selezionare **[!UICONTROL Manuale]** nella finestra di dialogo [!UICONTROL Crea schema] visualizzata.

>[!NOTE]
>
>Se utilizzi il flusso di lavoro per la creazione di schemi assistiti da apprendimento automatico, puoi caricare un file e utilizzare gli algoritmi ML per generare uno schema consigliato. Nel flusso di lavoro di creazione dello schema non è necessario specificare la classe base per lo schema. Per informazioni su come ML può consigliare una struttura di schema basata su un file csv, consulta la [guida alla creazione di schemi assistiti da apprendimento automatico](../ml-assisted-schema-creation.md).

![Finestra di dialogo Crea schema con le opzioni del flusso di lavoro e seleziona evidenziato.](../../images/ui/resources/classes/manually-create-a-schema.png)

Viene visualizzato il flusso di lavoro per la creazione dello schema. Nella sezione [!UICONTROL Dettagli schema], seleziona **[!UICONTROL Altro]**. Viene visualizzato un elenco delle classi disponibili. Selezionare **[!UICONTROL Crea classe]**.

![Il flusso di lavoro [!UICONTROL Crea schema] con [!UICONTROL Altro] evidenziato nella sezione [!UICONTROL Dettagli schema].](../../images/ui/resources/classes/other-schema-details.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Crea classe]. Immetti un [!UICONTROL Nome visualizzato] e una [!UICONTROL Descrizione] per la classe e scegli il comportamento previsto della classe con i pulsanti di scelta. Le classi possono essere di tipo [!UICONTROL Record] o [!UICONTROL Serie temporali]. Seleziona **[!UICONTROL Crea]** per confermare le scelte e tornare alla scheda [!UICONTROL Classi].

![La finestra di dialogo [!UICONTROL Crea classe] con [!UICONTROL Crea] evidenziata.](../../images/ui/resources/classes/create-class-from-schema.png)

L&#39;elenco delle classi viene aggiornato nella sezione [!UICONTROL Dettagli schema] e la classe appena creata viene selezionata automaticamente. Seleziona **[!UICONTROL Avanti]** per continuare a creare lo schema.

![La sezione [!UICONTROL Dettagli schema] con la nuova classe selezionata ed evidenziata [!UICONTROL Successivo].](../../images/ui/resources/classes/select-new-class.png)

Dopo aver selezionato una classe, viene visualizzata la sezione [!UICONTROL Name and review]. In questa sezione, fornisci un nome e una descrizione per identificare lo schema. &#x200B;La struttura di base dello schema (fornita dalla classe) viene visualizzata nell’area di lavoro per rivedere e verificare la struttura di classe e schema selezionata.

Immetti un nome visualizzato dello schema [!UICONTROL descrittivo] nel campo di testo. Quindi, inserisci una descrizione adatta per identificare lo schema. Dopo aver rivisto la struttura dello schema e aver impostato correttamente le impostazioni, seleziona **[!UICONTROL Fine]** per creare lo schema.

![La sezione [!UICONTROL Name and review] del flusso di lavoro [!UICONTROL Create schema] con [!UICONTROL Schema display name], [!UICONTROL Description], e [!UICONTROL Finish] evidenziato.](../../images/ui/resources/classes/schema-details.png)

## Aggiungere campi a una classe {#add-fields}

Dopo aver aperto uno schema che utilizza una classe personalizzata nell’Editor schema, puoi iniziare ad aggiungere campi alla classe. Per aggiungere un nuovo campo, seleziona l&#39;icona **più (+)** accanto al nome dello schema.

>[!IMPORTANT]
>
>Quando crei uno schema che implementa una classe definita dall’organizzazione, ricorda che i gruppi di campi di schema sono disponibili per l’utilizzo solo con classi compatibili. Poiché la classe definita è nuova, nella finestra di dialogo **[!UICONTROL Aggiungi gruppo di campi]** non sono elencati gruppi di campi compatibili. Sarà invece necessario [creare nuovi gruppi di campi](./field-groups.md#create) da utilizzare con tale classe. La prossima volta che componi uno schema che implementa la nuova classe, i gruppi di campi definiti verranno elencati e saranno disponibili per l’uso.

![Editor di schema con il pulsante di aggiunta evidenziato.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Tenere presente che tutti i campi aggiunti a una classe verranno utilizzati in tutti gli schemi che utilizzano tale classe. Pertanto, è necessario considerare attentamente quali campi saranno utili in tutti i casi di utilizzo degli schemi. Se stai pensando di aggiungere un campo che potrebbe essere utilizzato solo in alcuni schemi di questa classe, puoi provare ad aggiungerlo a tali schemi [creando un gruppo di campi](./field-groups.md#create).

Nell&#39;area di lavoro viene visualizzato un segnaposto per **[!UICONTROL Campo senza titolo]** e la barra a destra si aggiorna per mostrare i controlli per configurare le proprietà del campo. In **[!UICONTROL Assegna a]**, seleziona **[!UICONTROL Classe]**.

![Campo senza titolo nell&#39;area di lavoro dell&#39;Editor schema con la proprietà di campo Assegna a [!UICONTROL Classe] selezionata ed evidenziata.](../../images/ui/resources/classes/assign-to-class.png)

Consulta la guida su [definizione dei campi nell&#39;interfaccia utente](../fields/overview.md#define) per i passaggi specifici su come configurare e aggiungere il campo alla classe. Continua ad aggiungere alla classe tutti i campi necessari. Al termine, selezionare **[!UICONTROL Salva]** per salvare sia lo schema che la classe.

![Lo schema appena creato nell&#39;area di lavoro dell&#39;Editor di schema, con [!UICONTROL Salva] evidenziato.](../../images/ui/resources/classes/save.png)

Se in precedenza sono stati creati schemi che utilizzano questa classe, i campi appena aggiunti verranno visualizzati automaticamente in tali schemi.

## Modificare una classe (#edit-a-class)

>[!NOTE]
>
>Solo le classi personalizzate definite dall&#39;organizzazione possono essere completamente modificate e personalizzate. Per le classi principali definite da Adobe, è possibile modificare solo i nomi visualizzati dei relativi campi nel contesto dei singoli schemi. Per ulteriori informazioni, consulta la sezione sulla [modifica dei nomi visualizzati per i campi dello schema](./schemas.md#display-names).
>
>Dopo aver salvato e utilizzato una classe personalizzata nell’acquisizione dei dati, è possibile apportarvi solo modifiche aggiuntive. Per ulteriori informazioni, consulta le [regole dell&#39;evoluzione dello schema](../../schema/composition.md#evolution).

È possibile modificare una classe tramite il flusso di lavoro dello schema modificando uno schema esistente che estende la classe o creando manualmente uno schema. Non è possibile modificare direttamente una classe. Dall&#39;interno della scheda [!UICONTROL Sfoglia] nell&#39;area di lavoro [!UICONTROL Schemi], selezionare una classe esistente o **[!UICONTROL Crea uno schema]**.

![Editor di schema con una classe esistente e [!UICONTROL Creazione di uno schema] evidenziati.](../../images/ui/resources/classes/edit-class-options.png)

Se scegli di creare un nuovo schema, consulta la sezione sulla [creazione di uno schema](#create-schema) per i dettagli. Al termine della creazione dello schema o dopo aver selezionato uno schema esistente, verrà visualizzato l&#39;Editor di schema. Per aggiornare un campo di classe esistente, seleziona il campo dalla struttura dello schema. Le informazioni del campo vengono visualizzate nella barra a destra. Assicurati che [!UICONTROL Assegna a]
l&#39;opzione **[!UICONTROL Classe]** è selezionata o gli aggiornamenti non influiranno sulla classe.

![L&#39;Editor di schema con un campo selezionato ed evidenziato e la barra a destra esposta, evidenziando [!UICONTROL Assegna a].](../../images/ui/resources/classes/edit-existing-field.png)

Apporta le modifiche desiderate al campo, scorri verso il basso nella barra a destra per selezionare **[!UICONTROL Applica]** per salvare le modifiche.

>[!IMPORTANT]
>
> Eventuali aggiornamenti apportati ai campi verranno applicati a tutti gli schemi che utilizzano tale classe, seguendo le [regole di evoluzione dello schema](../../schema/composition.md#evolution).

![Editor schema con un campo selezionato e la barra a destra esposta, evidenziando [!UICONTROL Applica].](../../images/ui/resources/classes/save-changes.png)

Per aggiungere nuovi campi, seguire la [guida per aggiungere campi a una classe](#add-fields-to-a-class). Al termine, selezionare **[!UICONTROL Salva]** per salvare sia lo schema che la classe.

![Editor schema con [!UICONTROL Salva] evidenziato.](../../images/ui/resources/classes/save-schema.png)

## Modificare la classe di uno schema {#schema}

È possibile modificare la classe dello schema in qualsiasi momento durante il processo di creazione iniziale prima che sia stato salvato. Tuttavia, questo deve essere fatto con cautela, in quanto i gruppi di campi sono compatibili solo con determinate classi. La modifica della classe ripristina l’area di lavoro e tutti i campi aggiunti.
Per ulteriori informazioni, consulta la guida su [creazione e modifica di schemi](./schemas.md#change-class).

## Passaggi successivi {#next-steps}

Questo documento illustra come creare e modificare le classi utilizzando l’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemi], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemi]](../overview.md).

Per informazioni su come gestire le classi utilizzando l&#39;API Schema Registry, vedere la [guida dell&#39;endpoint delle classi](../../api/classes.md).
