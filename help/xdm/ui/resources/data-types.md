---
keywords: Experience Platform;home;argomenti popolari;interfaccia utente;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;registro schema;registro schema;schema;schema;schemi;schemi;schemi;creare;tipo di dati;tipi di dati;
solution: Experience Platform
title: Creare e modificare i tipi di dati tramite l’interfaccia utente
topic-legacy: tutorial
type: Tutorial
description: Scopri come creare e modificare i tipi di dati nell’interfaccia utente di Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# Creare e modificare i tipi di dati tramite l’interfaccia utente

In Experience Data Model (XDM), i tipi di dati vengono utilizzati come campi di tipo riferimento in classi o mixin allo stesso modo dei campi letterali di base; la differenza chiave è che i tipi di dati possono definire più campi secondari. Sebbene siano simili ai mixin in quanto consentono un uso coerente di una struttura a più campi, i tipi di dati sono più flessibili perché possono essere inclusi in qualsiasi punto della struttura dello schema, mentre i mixin possono essere aggiunti solo a livello principale.

Adobe Experience Platform fornisce molti tipi di dati standard che possono essere utilizzati per coprire un’ampia varietà di casi d’uso comuni per la gestione dell’esperienza. Tuttavia, puoi anche definire tipi di dati personalizzati per soddisfare le tue esigenze aziendali specifiche.

Questa esercitazione descrive i passaggi per la creazione e la modifica di tipi di dati personalizzati nell’interfaccia utente di Platform.

## Prerequisiti

Questa guida richiede una buona comprensione del sistema XDM. Per un&#39;introduzione al ruolo di XDM all&#39;interno dell&#39;ecosistema Experience Platform, fai riferimento alla [panoramica XDM](../../home.md) e alle [nozioni di base sulla composizione dello schema](../../schema/composition.md) per sapere in che modo i tipi di dati contribuiscono agli schemi XDM.

Sebbene non sia richiesto per questa guida, si consiglia anche di seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità di [!DNL Schema Editor].

## Apri [!DNL Schema Editor] per un tipo di dati

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemas]** nel menu di navigazione a sinistra per aprire l’area di lavoro [!UICONTROL Schemas], quindi seleziona la scheda **[!UICONTROL Data types]** . Viene visualizzato un elenco dei tipi di dati disponibili, inclusi quelli definiti dall’Adobe e quelli creati dall’organizzazione.

![](../../images/ui/resources/data-types/data-types-tab.png)

Da qui puoi scegliere tra due opzioni:

- [Creare un nuovo tipo di dati](#create)
- [Selezionare un tipo di dati esistente da modificare](#edit)

### Crea un nuovo tipo di dati {#create}

Dalla scheda **[!UICONTROL Data types]** , seleziona **[!UICONTROL Create data type]**.

![](../../images/ui/resources/data-types/create.png)

Viene visualizzata la sezione [!DNL Schema Editor] che mostra la struttura corrente del nuovo tipo di dati nell’area di lavoro. Sul lato destro dell’editor, puoi fornire un nome visualizzato e una descrizione facoltativa per il tipo di dati. Assicurati di fornire un nome univoco e conciso per il tipo di dati, così come verrà identificato quando lo aggiungi a uno schema.

Questa esercitazione crea un tipo di dati che descrive una proprietà del ristorante, in modo che al tipo di dati venga assegnato il nome visualizzato &quot;Ristorante&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

Da qui, puoi passare alla [sezione successiva](#add-fields) per iniziare ad aggiungere campi al nuovo tipo di dati.

### Modificare un tipo di dati esistente

È possibile modificare solo i tipi di dati personalizzati definiti dall’organizzazione. Per limitare l’elenco visualizzato, seleziona l’icona del filtro (![Icona filtro](../../images/ui/resources/data-types/filter.png)) per visualizzare i controlli per il filtraggio in base a [!UICONTROL Owner]. Seleziona **[!UICONTROL Customer]** per mostrare solo i tipi di dati personalizzati di proprietà dell’organizzazione.

Seleziona il tipo di dati da modificare dall’elenco per aprire la barra a destra e visualizzare i dettagli del tipo di dati. Seleziona il nome del tipo di dati nella barra a destra per aprirne la struttura in [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Aggiungi campi al tipo di dati {#add-fields}

Per iniziare ad aggiungere campi al tipo di dati, seleziona l’icona **più (+)** accanto al campo a livello principale nell’area di lavoro. Di seguito viene visualizzato un nuovo campo e la barra a destra viene aggiornata per visualizzare i controlli per il nuovo campo.

![](../../images/ui/resources/data-types/new-field.png)

Utilizza i controlli nella barra a destra per configurare i dettagli del nuovo campo. Per passaggi specifici su come configurare e aggiungere un campo al tipo di dati, consulta la guida [Definizione dei campi nell’interfaccia utente](../fields/overview.md#define) .

Il tipo di dati Ristorante richiede un campo stringa per rappresentare il nome del ristorante. Di conseguenza, il valore [!UICONTROL Field name] è impostato come &quot;name&quot; e il valore [!UICONTROL Type] è impostato come &quot;[!UICONTROL String]&quot;. Seleziona **[!UICONTROL Apply]** per applicare le modifiche al campo.

![](../../images/ui/resources/data-types/name-field.png)

Se necessario, aggiungi altri campi al tipo di dati. Il tipo di dati Ristorante di esempio ora dispone di campi aggiuntivi per il marchio, la capacità dei posti a sedere e lo spazio sul pavimento.

![](../../images/ui/resources/data-types/more-fields.png)

Oltre ai campi di base, puoi nidificare altri tipi di dati all’interno del tipo di dati personalizzato. Ad esempio, il tipo di dati Ristorante richiede un campo che rappresenti l’indirizzo fisico della proprietà. In questo scenario, puoi aggiungere un nuovo campo &quot;address&quot; a cui è assegnato il tipo di dati standard &quot;[!UICONTROL Postal address]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Questo dimostra come i tipi di dati flessibili possono essere in termini di descrizione dei dati: i tipi di dati possono utilizzare campi che sono anche tipi di dati, che possono a loro volta contenere ulteriori tipi di dati e così via. Questo consente di astrarre e riutilizzare pattern di dati comuni in tutti gli schemi XDM, facilitando la rappresentazione di strutture di dati complesse.

Dopo aver aggiunto i campi al tipo di dati, seleziona **[!UICONTROL Save]** per salvare le modifiche e aggiungere il tipo di dati a [!DNL Schema Library].

## Aggiungi il tipo di dati a una classe o a un mixin

Dopo aver creato un tipo di dati, puoi iniziare a utilizzarlo negli schemi. Poiché gli schemi XDM sono composti da una classe e da zero o più mixin, i campi forniti da un tipo di dati non possono essere aggiunti direttamente a uno schema. Devono invece essere inclusi in una classe o in un mixin.

Per iniziare, segui i passaggi descritti in [aggiunta di un campo a una classe](./classes.md#add-fields) o [aggiunta di un campo a un mixin](./mixins.md#add-fields). Quando scegli il **[!UICONTROL Type]** per il nuovo campo, seleziona il nome del tipo di dati dal menu a discesa.

## Convertire un oggetto con più campi in un tipo di dati {#convert}

Quando si crea un campo di tipo oggetto con più campi secondari in [!DNL Schema Editor], è possibile convertirlo in un tipo di dati per utilizzare la stessa struttura di campo in una classe o un mixin diversi.

Per convertire un campo di tipo oggetto in un tipo di dati, selezionare il campo nell’area di lavoro. Prima di convertire il campo, accertati che il **[!UICONTROL Display name]** sia descrittivo dei dati che l’oggetto conterrà, in quanto questo diventerà il nome del tipo di dati. Quando sei pronto a convertire il campo, seleziona **[!UICONTROL Convert to new data type]** nella barra a destra.

![](../../images/ui/resources/data-types/convert-object.png)

L&#39;area di lavoro aggiorna il tipo di dati del campo da &quot;[!UICONTROL Object]&quot; al nuovo tipo di dati. Accanto ai sottocampi sono inoltre presenti piccole icone di blocco che indicano che non sono più campi singoli ma fanno parte di un tipo di dati con più campi. Questa struttura può ora essere riutilizzata in altre classi e mixin selezionando questo tipo di dati dal menu a discesa **[!UICONTROL Type]** durante la definizione di un nuovo campo.

![](../../images/ui/resources/data-types/converted.png)

## Passaggi successivi

Questa guida illustra come creare e modificare i tipi di dati tramite l’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas], consulta la [[!UICONTROL Schemas] panoramica dell&#39;area di lavoro](../overview.md).

Per informazioni su come gestire i tipi di dati utilizzando l&#39;API [!DNL Schema Registry], consulta la [guida all&#39;endpoint per i tipi di dati](../../api/data-types.md).
