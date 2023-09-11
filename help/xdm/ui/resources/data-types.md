---
keywords: Experience Platform;home;argomenti popolari;ui;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;schema Registry;schema;schema;schemi;schemi;creare;tipo di dati;tipi di dati;
solution: Experience Platform
title: Creare e modificare i tipi di dati tramite l’interfaccia utente
type: Tutorial
description: Scopri come creare e modificare i tipi di dati nell’interfaccia utente di Experienci Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 51ef116ad125b0d699bf4808e3d26d3b00b743e2
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---

# Creare e modificare i tipi di dati tramite l’interfaccia utente {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="Filtro per tipo di dati standard o personalizzato"
>abstract="L’elenco dei tipi di dati disponibili viene pre-filtrato in base a come sono stati creati. Selezionare il pulsante di opzione per scegliere tra le opzioni Standard e Personalizzato. L&#39;opzione Standard mostra le entità create da Adobe, mentre l&#39;opzione Personalizzato mostra le entità create all&#39;interno dell&#39;organizzazione. Per ulteriori informazioni sulla creazione e la modifica dei tipi di dati, consulta la documentazione."

In Experience Data Model (XDM), i tipi di dati sono campi riutilizzabili che contengono più sottocampi. Sebbene siano simili ai gruppi di campi dello schema in quanto consentono l’utilizzo coerente di una struttura a più campi, i tipi di dati sono più flessibili in quanto possono essere inclusi ovunque nella struttura dello schema, mentre i gruppi di campi possono essere aggiunti solo al livello principale.

Adobe Experience Platform fornisce molti tipi di dati standard che possono essere utilizzati per coprire un’ampia varietà di casi d’uso comuni di gestione delle esperienze. Tuttavia, puoi anche definire tipi di dati personalizzati per soddisfare esigenze aziendali specifiche.

Questo tutorial illustra i passaggi necessari per creare e modificare tipi di dati personalizzati nell’interfaccia utente di Platform.

## Prerequisiti

Questa guida richiede una buona conoscenza del sistema XDM. Consulta la sezione [Panoramica di XDM](../../home.md) per un’introduzione al ruolo di XDM nell’ecosistema Experience Platform e [nozioni di base sulla composizione dello schema](../../schema/composition.md) come i tipi di dati contribuiscono agli schemi XDM.

Sebbene non sia necessario per questa guida, si consiglia di seguire l’esercitazione anche su [composizione di uno schema nell’interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità del [!DNL Schema Editor].

## Apri [!DNL Schema Editor] per un tipo di dati {#data-type}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nel menu di navigazione a sinistra per aprire [!UICONTROL Schemi] , quindi seleziona la **[!UICONTROL Tipi di dati]** scheda. Viene visualizzato un elenco dei tipi di dati disponibili, inclusi quelli definiti da Adobe e quelli creati dall’organizzazione.

![](../../images/ui/resources/data-types/data-types-tab.png)

Da qui puoi scegliere tra due opzioni:

- [Crea un nuovo tipo di dati](#create)
- [Seleziona un tipo di dati esistente da modificare](#edit)

### Crea un nuovo tipo di dati {#create}

Dalla sezione **[!UICONTROL Tipi di dati]** , seleziona **[!UICONTROL Crea tipo di dati]**.

![](../../images/ui/resources/data-types/create.png)

Il [!DNL Schema Editor] viene visualizzata la struttura corrente del nuovo tipo di dati nell&#39;area di lavoro. Sul lato destro dell’editor, puoi fornire un nome visualizzato e una descrizione facoltativa per il tipo di dati. Assicurati di fornire un nome univoco e conciso per il tipo di dati, in quanto questo sarà il modo in cui verrà identificato quando lo aggiungi a uno schema.

Questo tutorial crea un tipo di dati che descrive una proprietà del ristorante, per cui al tipo di dati viene assegnato il nome visualizzato &quot;Restaurant&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

Da qui, puoi passare alla sezione [sezione successiva](#add-fields) per iniziare ad aggiungere campi al nuovo tipo di dati.

### Modificare un tipo di dati esistente {#edit}

>[!NOTE]
>
>Una volta utilizzato un tipo di dati esistente in uno schema abilitato per l’utilizzo in Real-Time Customer Profile, è possibile apportare successivamente solo modifiche non distruttive a tale tipo di dati. Consulta la [regole di evoluzione dello schema](../../schema/composition.md#evolution) per ulteriori informazioni.

È possibile modificare solo i tipi di dati personalizzati definiti dall’organizzazione. Per limitare l’elenco visualizzato, seleziona l’icona del filtro (![Icona filtro](../../images/ui/resources/data-types/filter.png)) per visualizzare i controlli per il filtraggio in base a [!UICONTROL Proprietario]. Seleziona **[!UICONTROL Cliente]** per mostrare solo i tipi di dati personalizzati di proprietà della tua organizzazione.

Seleziona dall’elenco il tipo di dati da modificare per aprire la barra a destra, con i dettagli del tipo di dati. Seleziona il nome del tipo di dati nella barra a destra per aprirne la struttura in [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Aggiungere campi al tipo di dati {#add-fields}

Per iniziare ad aggiungere campi al tipo di dati, seleziona la **più (+)** accanto al campo a livello di radice nell’area di lavoro. Sotto viene visualizzato un nuovo campo e la barra a destra si aggiorna per visualizzare i controlli per il nuovo campo.

![](../../images/ui/resources/data-types/new-field.png)

Utilizza i controlli nella barra a destra per configurare i dettagli del nuovo campo. Consulta la guida su [definizione dei campi nell’interfaccia utente](../fields/overview.md#define) per passaggi specifici su come configurare e aggiungere il campo al tipo di dati.

Il tipo di dati Ristorante richiede un campo stringa per rappresentare il nome del ristorante. In quanto tale, il [!UICONTROL Nome campo] è impostato come &quot;name&quot; e [!UICONTROL Tipo] è impostato come &quot;[!UICONTROL Stringa]&quot;. Seleziona **[!UICONTROL Applica]** per applicare le modifiche al campo.

![](../../images/ui/resources/data-types/name-field.png)

Continua ad aggiungere altri campi al tipo di dati in base alle esigenze. Il tipo di dati Ristorante di esempio ora dispone di campi aggiuntivi per marchio, capacità di posti a sedere e spazio del pavimento.

![](../../images/ui/resources/data-types/more-fields.png)

Oltre ai campi di base, puoi anche nidificare tipi di dati aggiuntivi all’interno del tipo di dati personalizzato. Ad esempio, il tipo di dati Ristorante richiede un campo che rappresenti l’indirizzo fisico della proprietà. In questo scenario, puoi aggiungere un nuovo campo &quot;address&quot; a cui viene assegnato il tipo di dati standard &quot;[!UICONTROL Indirizzo postale]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Questo dimostra quanto possano essere flessibili i tipi di dati in termini di descrizione dei dati: i tipi di dati possono utilizzare campi che sono anche tipi di dati, che a loro volta possono contenere ulteriori tipi di dati e così via. Questo consente di astrarre e riutilizzare pattern di dati comuni in tutti gli schemi XDM, semplificando la rappresentazione di strutture di dati complesse.

Dopo aver aggiunto i campi al tipo di dati, seleziona **[!UICONTROL Salva]** per salvare le modifiche e aggiungere il tipo di dati al [!DNL Schema Library].

## Aggiungere il tipo di dati a uno schema

Dopo aver creato un tipo di dati, puoi iniziare a utilizzarlo negli schemi. Poiché gli schemi XDM sono composti da una classe e da zero o più gruppi di campi, i campi forniti da un tipo di dati non possono essere aggiunti direttamente a uno schema. Devono invece essere inclusi in una classe o in un gruppo di campi.

Per iniziare, segui i passaggi relativi a [aggiunta di un campo a una classe](./classes.md#add-fields) o [aggiunta di un campo a un gruppo di campi](./field-groups.md#add-fields). In alternativa, è possibile iniziare [aggiunta diretta di un campo a uno schema](./schemas.md#add-individual-fields) e scegliere la classe padre o il gruppo di campi. Quando scegli il **[!UICONTROL Tipo]** per il nuovo campo, seleziona il nome del tipo di dati dal menu a discesa.

## Convertire un oggetto multicampo in un tipo di dati {#convert}

Quando si crea un campo di tipo oggetto con più sottocampi nel [!DNL Schema Editor], è possibile convertire tale campo in un tipo di dati in modo da poter utilizzare la stessa struttura di campi in una classe o in un gruppo di campi diverso.

Per convertire un campo di tipo oggetto in un tipo di dati, selezionare il campo nell&#39;area di lavoro. Prima di convertire il campo, assicurati che il **[!UICONTROL Nome visualizzato]** è descrittivo dei dati che l’oggetto conterrà, in quanto diventerà il nome del tipo di dati. Quando sei pronto per convertire il campo, seleziona **[!UICONTROL Converti in nuovo tipo di dati]** nella barra a destra.

![](../../images/ui/resources/data-types/convert-object.png)

Il quadro aggiorna il tipo di dati del campo da &quot;[!UICONTROL Oggetto]&quot; al nuovo tipo di dati. Questa struttura può ora essere riutilizzata in altre classi e gruppi di campi selezionando questo tipo di dati dall&#39; **[!UICONTROL Tipo]** quando si definisce un nuovo campo.

![](../../images/ui/resources/data-types/converted.png)

## Passaggi successivi

Questa guida illustra come creare e modificare i tipi di dati utilizzando l’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità di [!UICONTROL Schemi] Workspace, consulta la sezione [[!UICONTROL Schemi] panoramica di workspace](../overview.md).

Per scoprire come gestire i tipi di dati utilizzando [!DNL Schema Registry] API, consulta [guida dell’endpoint &quot;data types&quot;](../../api/data-types.md).
