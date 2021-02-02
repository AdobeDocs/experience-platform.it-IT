---
keywords: ' Experience Platform;home;argomenti più comuni;ui;XDM;XDM sistema;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;schema di registro;schema di registro;schema;schema;schemi;schemi;schemi;creare;tipo di dati;tipi di dati;'
solution: Experience Platform
title: Creazione e modifica di tipi di dati tramite l'interfaccia utente
topic: tutorial
type: Tutorial
description: Scoprite come creare e modificare i tipi di dati nell'interfaccia utente del Experience Platform .
translation-type: tm+mt
source-git-commit: eca896ca068a02da7ec7379e8ced2105bbca9f2d
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---


# Creazione e modifica di tipi di dati tramite l&#39;interfaccia utente

In Experience Data Model (XDM), i tipi di dati vengono utilizzati come campi di tipo riferimento nelle classi o nei mixin allo stesso modo dei campi letterali di base, con la differenza chiave che i tipi di dati possono definire più sottocampi. Anche se simili ai mixin in quanto consentono l&#39;uso coerente di una struttura multi-campo, i tipi di dati sono più flessibili perché possono essere inclusi ovunque nella struttura dello schema, mentre i mixin possono essere aggiunti solo a livello principale.

Adobe Experience Platform fornisce molti tipi di dati standard che possono essere utilizzati per coprire un&#39;ampia gamma di casi d&#39;uso comuni per la gestione dell&#39;esperienza. Tuttavia, puoi anche definire tipi di dati personalizzati per soddisfare esigenze aziendali specifiche.

Questa esercitazione descrive i passaggi per la creazione e la modifica di tipi di dati personalizzati nell&#39;interfaccia utente della piattaforma.

## Prerequisiti

Questa guida richiede una buona conoscenza del sistema XDM. Per un&#39;introduzione al ruolo di XDM nell&#39;ecosistema  Experience Platform, fare riferimento alla [panoramica XDM](../../home.md) e alle [nozioni di base della composizione dello schema](../../schema/composition.md) per sapere in che modo i tipi di dati contribuiscono agli schemi XDM.

Sebbene non sia richiesto per questa guida, si consiglia anche di seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire dimestichezza con le diverse funzionalità di [!DNL Schema Editor].

## Aprire la [!DNL Schema Editor] per un tipo di dati

Nell&#39;interfaccia utente della piattaforma, selezionare **[!UICONTROL Schemas]** nel menu di navigazione a sinistra per aprire l&#39;area di lavoro [!UICONTROL Schemas], quindi selezionare la scheda **[!UICONTROL Data types]**. Viene visualizzato un elenco dei tipi di dati disponibili, inclusi quelli definiti dal Adobe  e quelli creati dall&#39;organizzazione.

![](../../images/ui/resources/data-types/data-types-tab.png)

Da qui sono disponibili due opzioni:

- [Creare un nuovo tipo di dati](#create)
- [Selezionare un tipo di dati esistente da modificare](#edit)

### Creare un nuovo tipo di dati {#create}

Dalla scheda **[!UICONTROL Data types]**, selezionare **[!UICONTROL Create data type]**.

![](../../images/ui/resources/data-types/create.png)

Viene visualizzata la [!DNL Schema Editor] che mostra la struttura corrente del nuovo tipo di dati nel quadro. Sul lato destro dell&#39;editor, è possibile fornire un nome visualizzato e una descrizione facoltativa per il tipo di dati. Assicurarsi di fornire un nome univoco e conciso per il tipo di dati, così come sarà identificato quando lo si aggiunge a uno schema.

Questa esercitazione crea un tipo di dati che descrive una proprietà ristorante, quindi al tipo di dati viene assegnato il nome visualizzato &quot;Restaurant&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

Da qui è possibile passare alla sezione [successiva](#add-fields) per iniziare ad aggiungere campi al nuovo tipo di dati.

### Modificare un tipo di dati esistente

È possibile modificare solo i tipi di dati personalizzati definiti dall&#39;organizzazione. Per restringere l&#39;elenco visualizzato, selezionate l&#39;icona del filtro (![Icona filtro](../../images/ui/resources/data-types/filter.png)) per visualizzare i controlli per il filtraggio in base a [!UICONTROL Owner]. Selezionare **[!UICONTROL Customer]** per mostrare solo i tipi di dati personalizzati di proprietà dell&#39;organizzazione.

Selezionare il tipo di dati che si desidera modificare dall&#39;elenco per aprire la barra laterale destra, mostrando i dettagli del tipo di dati. Selezionare il nome del tipo di dati nella barra a destra per aprirne la struttura in [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Aggiungere campi al tipo di dati {#add-fields}

Per iniziare ad aggiungere campi al tipo di dati, selezionare l&#39;icona **più (+)** accanto al campo di livello principale nell&#39;area di lavoro. Di seguito viene visualizzato un nuovo campo e la barra laterale destra si aggiorna per visualizzare i controlli per il nuovo campo.

![](../../images/ui/resources/data-types/new-field.png)

Utilizzate i controlli nella barra a destra per configurare i dettagli del nuovo campo. Per istruzioni su come configurare e aggiungere il campo al tipo di dati, vedere la guida relativa alla [definizione dei campi nell&#39;interfaccia utente](../fields/overview.md#define).

Il tipo di dati Ristorante richiede un campo stringa che rappresenti il nome del ristorante. Di conseguenza, [!UICONTROL Field name] è impostato come &quot;name&quot; e [!UICONTROL Type] come &quot;[!UICONTROL String]&quot;. Selezionare **[!UICONTROL Apply]** per applicare le modifiche al campo.

![](../../images/ui/resources/data-types/name-field.png)

Continua ad aggiungere altri campi al tipo di dati, se necessario. L&#39;esempio tipo di dati Ristorante dispone ora di campi aggiuntivi per marchio, capacità di posti a sedere e spazio pavimento.

![](../../images/ui/resources/data-types/more-fields.png)

Oltre ai campi di base, è anche possibile nidificare altri tipi di dati all&#39;interno del tipo di dati personalizzato. Ad esempio, il tipo di dati Ristorante richiede un campo che rappresenti l&#39;indirizzo fisico della proprietà. In questo scenario, è possibile aggiungere un nuovo campo &quot;indirizzo&quot; a cui è assegnato il tipo di dati standard &quot;[!UICONTROL Postal address]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Questo dimostra come i tipi di dati flessibili possono essere flessibili in termini di descrizione dei dati: i tipi di dati possono utilizzare campi che sono anche tipi di dati, che a loro volta possono contenere ulteriori tipi di dati, e così via. Questo consente di astrarre e riutilizzare pattern di dati comuni in tutti gli schemi XDM, semplificando la rappresentazione di strutture di dati complesse.

Dopo aver aggiunto i campi al tipo di dati, selezionare **[!UICONTROL Save]** per salvare le modifiche e aggiungere il tipo di dati al [!DNL Schema Library].

## Aggiungere il tipo di dati a una classe o a un mixin

Dopo aver creato un tipo di dati, è possibile iniziare a utilizzarlo negli schemi. Poiché gli schemi XDM sono composti da una classe e da zero o più mixin, i campi forniti da un tipo di dati non possono essere aggiunti direttamente a uno schema. Devono invece essere inclusi in una classe o in un mixin.

Per iniziare, seguire i passaggi relativi all&#39;aggiunta di un campo a una classe](./classes.md#add-fields) o [aggiunta di un campo a un mixin](./mixins.md#add-fields). [ Quando si sceglie **[!UICONTROL Type]** per il nuovo campo, selezionare il nome del tipo di dati dal menu a discesa.

## Conversione di un oggetto multicampo in un tipo di dati {#convert}

Quando si crea un campo di tipo oggetto con più campi secondari in [!DNL Schema Editor], è possibile convertire tale campo in un tipo di dati in modo da poter utilizzare la stessa struttura di campo in una classe o in un mixin diverso.

Per convertire un campo di tipo oggetto in un tipo di dati, selezionare il campo nell&#39;area di lavoro. Prima di convertire il campo, assicurarsi che la **[!UICONTROL Display name]** sia descrittiva dei dati che l&#39;oggetto conterrà, in quanto questo diventerà il nome del tipo di dati. Quando si è pronti per convertire il campo, selezionare **[!UICONTROL Convert to new data type]** nella barra a destra.

![](../../images/ui/resources/data-types/convert-object.png)

Il quadro aggiorna il tipo di dati del campo da &quot;[!UICONTROL Object]&quot; al nuovo tipo di dati. Accanto ai sottocampi sono inoltre presenti delle icone di blocco piccole, che indicano che non si tratta più di singoli campi ma piuttosto di un tipo di dati multicampo. È ora possibile riutilizzare questa struttura in altre classi e mixin selezionando questo tipo di dati dal menu a discesa **[!UICONTROL Type]** quando si definisce un nuovo campo.

![](../../images/ui/resources/data-types/converted.png)

## Passaggi successivi

Questa guida ha illustrato come creare e modificare i tipi di dati utilizzando l&#39;interfaccia utente della piattaforma. Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemas]](../overview.md).

Per informazioni su come gestire i tipi di dati utilizzando l&#39;API [!DNL Schema Registry], consultare la guida [endpoint dei tipi di dati](../../api/data-types.md).
