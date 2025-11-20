---
keywords: Experience Platform;home;argomenti popolari;ui;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;schema Registry;schema;schema;schemi;schemi;creare;tipo di dati;tipi di dati;
solution: Experience Platform
title: Creare e modificare i tipi di dati tramite l’interfaccia utente
type: Tutorial
description: Scopri come creare e modificare i tipi di dati nell’interfaccia utente di Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 6%

---

# Creare e modificare i tipi di dati tramite l’interfaccia utente {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="Filtro per tipo di dati personalizzati o standard"
>abstract="L’elenco dei tipi di dati disponibili viene prefiltrato in base alla modalità di creazione. Selezionare il pulsante di opzione per scegliere tra le opzioni Standard e Personalizzato. L’opzione Standard mostra le entità create da Adobe, mentre l’opzione Personalizzato mostra le entità create all’interno dell’organizzazione. Per ulteriori informazioni sulla creazione e la modifica dei tipi di dati, consulta la documentazione."

In Experience Data Model (XDM), i tipi di dati sono campi riutilizzabili che contengono più sottocampi. Sebbene siano simili ai gruppi di campi dello schema in quanto consentono l’utilizzo coerente di una struttura a più campi, i tipi di dati sono più flessibili in quanto possono essere inclusi ovunque nella struttura dello schema, mentre i gruppi di campi possono essere aggiunti solo al livello principale.

Adobe Experience Platform fornisce molti tipi di dati standard che possono essere utilizzati per coprire un’ampia varietà di casi d’uso comuni di gestione delle esperienze. Tuttavia, puoi anche definire tipi di dati personalizzati per soddisfare esigenze aziendali specifiche.

>[!NOTE]
>
>Se un campo è definito come tipo di dati specifico, non è possibile creare lo stesso campo con un tipo di dati diverso in un altro schema. Questo vincolo si applica a tutto il tenant dell’organizzazione.

Questo tutorial illustra i passaggi necessari per creare e modificare i tipi di dati personalizzati nell’interfaccia utente di Experience Platform.

## Prerequisiti {#prerequisites}

Questa guida richiede una buona conoscenza del sistema XDM. Consulta la [panoramica di XDM](../../home.md) per un&#39;introduzione al ruolo di XDM nell&#39;ecosistema Experience Platform e le [nozioni di base sulla composizione dello schema](../../schema/composition.md) per informazioni sul modo in cui i tipi di dati contribuiscono agli schemi XDM.

Sebbene non sia necessario per questa guida, è consigliabile seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità di [!DNL Schema Editor].

## Apri [!DNL Schema Editor] per un tipo di dati {#data-type}

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Schemas]** nel menu di navigazione a sinistra per aprire l&#39;area di lavoro [!UICONTROL Schemas], quindi seleziona la scheda **[!UICONTROL Data types]**. Viene visualizzato un elenco dei tipi di dati disponibili. L’elenco dei tipi di dati viene filtrato automaticamente in base alla modalità di creazione. L’impostazione predefinita visualizza i tipi di dati definiti da Adobe. Puoi anche filtrare l’elenco per visualizzare quelli creati dall’organizzazione.

![Area di lavoro [!UICONTROL Schemas] con [!UICONTROL Schemas] nel menu di navigazione a sinistra e [!UICONTROL Data types] evidenziata.](../../images/ui/resources/data-types/data-types-tab.png)

Da qui sono disponibili le seguenti opzioni:

- [Crea un nuovo tipo di dati](#create)
- [Filtrare i tipi di dati](#filter)
- [Seleziona un tipo di dati esistente da modificare](#edit)

### Crea un nuovo tipo di dati {#create}

Dalla sezione **[!UICONTROL Data types]**, seleziona **[!UICONTROL Create data type]**.

![Scheda [!UICONTROL Schemas] dell&#39;area di lavoro [!UICONTROL Data types] con [!UICONTROL Create data type] evidenziato.](../../images/ui/resources/data-types/create.png)

Viene visualizzato [!DNL Schema Editor], che mostra la struttura corrente del nuovo tipo di dati nell&#39;area di lavoro. Sul lato destro dell’editor, puoi fornire un nome visualizzato e una descrizione facoltativa per il tipo di dati. Assicurati di fornire un nome univoco e conciso per il tipo di dati, in quanto questo sarà il modo in cui verrà identificato quando lo aggiungi a uno schema.

Questo tutorial crea un tipo di dati che descrive una proprietà del ristorante, per cui al tipo di dati viene assegnato il nome visualizzato &quot;Restaurant&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

Da qui puoi passare alla [sezione successiva](#add-fields) per iniziare ad aggiungere campi al nuovo tipo di dati.

### Filtrare i tipi di dati {#filter}

L’elenco dei tipi di dati disponibili viene prefiltrato in base alla modalità di creazione. Selezionare il pulsante di opzione per scegliere tra le opzioni [!UICONTROL Standard] e [!UICONTROL Custom]. L&#39;opzione [!UICONTROL Standard] mostra le entità create da Adobe e l&#39;opzione [!UICONTROL Custom] mostra le entità create all&#39;interno dell&#39;organizzazione.

![Scheda [!UICONTROL Data types] dell&#39;area di lavoro [!UICONTROL Schemas] con [!UICONTROL Standard] e [!UICONTROL Custom] evidenziati.](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### Modificare un tipo di dati esistente {#edit}

>[!NOTE]
>
>Una volta utilizzato un tipo di dati esistente in uno schema abilitato per l’utilizzo in Real-Time Customer Profile, è possibile apportare successivamente solo modifiche non distruttive a tale tipo di dati. Per ulteriori informazioni, consulta le [regole dell&#39;evoluzione dello schema](../../schema/composition.md#evolution).

È possibile modificare solo i tipi di dati personalizzati definiti dall’organizzazione. Seleziona **[!UICONTROL Custom]** per visualizzare solo i tipi di dati personalizzati di proprietà della tua organizzazione.

Seleziona dall’elenco il tipo di dati da modificare per aprire la barra a destra, con i dettagli del tipo di dati. Dal pannello dei dettagli puoi anche scaricare un file di esempio, copiare la struttura JSON o aggiungere il tipo di dati a un pacchetto.

Selezionare il nome del tipo di dati nella barra a destra per aprirne la struttura in [!DNL Schema Editor].

![Scheda [!UICONTROL Data types] dell&#39;area di lavoro [!UICONTROL Schemas], con tipo di dati [!UICONTROL Custom] e tipo di dati [!UICONTROL Name] evidenziati.](../../images/ui/resources/data-types/edit.png)

## Aggiungere campi al tipo di dati {#add-fields}

Per iniziare ad aggiungere campi al tipo di dati, seleziona l’icona **più (+)** accanto al campo a livello di radice nell’area di lavoro. Sotto viene visualizzato un nuovo campo e la barra a destra si aggiorna per visualizzare i controlli per il nuovo campo.

![](../../images/ui/resources/data-types/new-field.png)

Utilizza i controlli nella barra a destra per configurare i dettagli del nuovo campo. Consulta la guida su [definizione dei campi nell&#39;interfaccia utente](../fields/overview.md#define) per i passaggi specifici su come configurare e aggiungere il campo al tipo di dati.

Il tipo di dati Ristorante richiede un campo stringa per rappresentare il nome del ristorante. [!UICONTROL Field name] è impostato come &quot;name&quot; e [!UICONTROL Type] è impostato come &quot;[!UICONTROL String]&quot;. Selezionare **[!UICONTROL Apply]** per applicare le modifiche al campo.

![](../../images/ui/resources/data-types/name-field.png)

Continua ad aggiungere altri campi al tipo di dati in base alle esigenze. Il tipo di dati Ristorante di esempio ora dispone di campi aggiuntivi per marchio, capacità di posti a sedere e spazio del pavimento.

![](../../images/ui/resources/data-types/more-fields.png)

Oltre ai campi di base, puoi anche nidificare tipi di dati aggiuntivi all’interno del tipo di dati personalizzato. Ad esempio, il tipo di dati Ristorante richiede un campo che rappresenti l’indirizzo fisico della proprietà. In questo scenario, è possibile aggiungere un nuovo campo &quot;address&quot; a cui viene assegnato il tipo di dati standard &quot;[!UICONTROL Postal address]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Questo dimostra quanto possano essere flessibili i tipi di dati in termini di descrizione dei dati: i tipi di dati possono utilizzare campi che sono anche tipi di dati, che a loro volta possono contenere ulteriori tipi di dati e così via. Questo consente di astrarre e riutilizzare pattern di dati comuni in tutti gli schemi XDM, semplificando la rappresentazione di strutture di dati complesse.

Dopo aver aggiunto i campi al tipo di dati, selezionare **[!UICONTROL Save]** per salvare le modifiche e aggiungere il tipo di dati a [!DNL Schema Library].

## Aggiungere il tipo di dati a uno schema {#add-data-type}

Dopo aver creato un tipo di dati, puoi iniziare a utilizzarlo negli schemi. Poiché gli schemi XDM sono composti da una classe e da zero o più gruppi di campi, i campi forniti da un tipo di dati non possono essere aggiunti direttamente a uno schema. Devono invece essere inclusi in una classe o in un gruppo di campi.

Iniziare seguendo i passaggi necessari per [aggiungere un campo a una classe](./classes.md#add-fields) o [aggiungere un campo a un gruppo di campi](./field-groups.md#add-fields). In alternativa, è possibile avviare [l&#39;aggiunta di un campo direttamente a uno schema](./schemas.md#add-individual-fields) e scegliere la classe padre o il gruppo di campi da tale schema. Quando scegli **[!UICONTROL Type]** per il nuovo campo, seleziona il nome del tipo di dati dal menu a discesa.

## Convertire un oggetto multicampo in un tipo di dati {#convert}

Quando si crea un campo di tipo oggetto con più sottocampi in [!DNL Schema Editor], è possibile convertire tale campo in un tipo di dati in modo da poter utilizzare la stessa struttura di campi in una classe o in un gruppo di campi diverso.

Per convertire un campo di tipo oggetto in un tipo di dati, selezionare il campo nell&#39;area di lavoro. Prima di convertire il campo, verificare che **[!UICONTROL Display name]** sia descrittivo dei dati che l&#39;oggetto conterrà, in quanto diventerà il nome del tipo di dati. Quando sei pronto a convertire il campo, seleziona **[!UICONTROL Convert to new data type]** nella barra a destra.

![](../../images/ui/resources/data-types/convert-object.png)

Il tipo di dati del campo viene aggiornato da &quot;[!UICONTROL Object]&quot; al nuovo tipo di dati. Questa struttura può essere riutilizzata in altre classi e gruppi di campi selezionando questo tipo di dati dal menu a discesa **[!UICONTROL Type]** durante la definizione di un nuovo campo.

![](../../images/ui/resources/data-types/converted.png)

## Passaggi successivi {#next-steps}

Questa guida illustra come creare e modificare i tipi di dati utilizzando l’interfaccia utente di Experience Platform. Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemas]](../overview.md).

Per informazioni su come gestire i tipi di dati utilizzando l&#39;API [!DNL Schema Registry], vedere la [guida dell&#39;endpoint dei tipi di dati](../../api/data-types.md).
