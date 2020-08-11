---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definire una relazione tra due schemi utilizzando l'Editor schema
topic: tutorials
translation-type: tm+mt
source-git-commit: 6d291ac9a8c194dd63e411e4d064492c38412749
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---


# Definire una relazione tra due schemi utilizzando la variabile [!DNL Schema Editor]

La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il tuo marchio attraverso vari canali è una parte importante di Adobe Experience Platform. La definizione di queste relazioni all&#39;interno della struttura degli schemi [!DNL Experience Data Model] (XDM) consente di acquisire informazioni complesse sui dati dei clienti.

Sebbene sia possibile dedurre le relazioni dello schema utilizzando lo schema unione e [!DNL Real-time Customer Profile], ciò vale solo per gli schemi che condividono la stessa classe. Per stabilire una relazione tra due schemi appartenenti a classi diverse, è necessario aggiungere un campo **di** relazione dedicato a uno schema di origine che faccia riferimento all&#39;identità di uno schema di destinazione.

Questo documento fornisce un&#39;esercitazione per definire una relazione tra due schemi utilizzando l&#39;Editor di schema nell&#39;interfaccia [!DNL Experience Platform] utente. Per i passaggi sulla definizione delle relazioni di schema mediante l&#39;API, vedete l&#39;esercitazione sulla [definizione di una relazione mediante l&#39;API](relationship-api.md)del Registro di sistema dello schema.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita di [!DNL XDM System] e dell&#39;Editor di schema nell&#39; [!DNL Experience Platform] interfaccia utente. Prima di iniziare questa esercitazione, consulta la seguente documentazione:

* [Sistema XDM in  Experience Platform](../home.md): Panoramica di XDM e relativa implementazione in [!DNL Experience Platform].
* [Nozioni di base sulla composizione](../schema/composition.md)dello schema: Introduzione dei blocchi costitutivi degli schemi XDM.
* [Creare uno schema utilizzando l&#39;Editor](create-schema-ui.md)schema: Un&#39;esercitazione che illustra le nozioni di base dell&#39;utilizzo dell&#39; [!DNL Schema Editor].

## Definire uno schema di origine e di destinazione

È previsto che siano già stati creati i due schemi che verranno definiti nella relazione. A scopo dimostrativo, questa esercitazione crea una relazione tra i membri del programma fedeltà di un&#39;organizzazione (definito in uno schema &quot;[!UICONTROL Loyalty Members]&quot;) e i loro alberghi preferiti (definiti in uno schema &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Per stabilire una relazione, entrambi gli schemi devono avere identità principali definite ed essere attivati per [!DNL Real-time Customer Profile]. Per informazioni su come configurare gli schemi di conseguenza, vedere la sezione relativa all&#39; [abilitazione di uno schema da utilizzare nel profilo](./create-schema-ui.md#profile) nell&#39;esercitazione sulla creazione dello schema.

Le relazioni dello schema sono rappresentate da un campo dedicato all&#39;interno di uno schema **di** origine che fa riferimento a un altro campo all&#39;interno di uno schema **di** destinazione. Nei passaggi successivi, &quot;[!UICONTROL Loyalty Members]&quot; sarà lo schema di origine, mentre &quot;[!DNL Hotels]&quot; fungerà da schema di destinazione.

A scopo di riferimento, le sezioni seguenti descrivono la struttura di ogni schema utilizzato in questa esercitazione prima che sia stata definita una relazione.

### [!UICONTROL Loyalty Members] schema

Lo schema di origine &quot;[!UICONTROL Loyalty Members]&quot; è basato sulla [!DNL Individual Profile] classe XDM ed è lo schema creato nell&#39;esercitazione per [creare uno schema nell&#39;interfaccia utente](create-schema-ui.md). Include un oggetto &quot;[!UICONTROL loyalty]&quot; nello spazio dei nomi &quot;\_tenantId&quot;, che include diversi campi specifici per la fedeltà. Uno di questi campi, &quot;loyaltyId&quot;, funge da identità principale per lo schema nello spazio dei nomi &quot;[!UICONTROL Email]&quot;. Come mostrato in _[!UICONTROL Schema Properties]_, questo schema è stato abilitato per l&#39;uso in[!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### Hotels, schema

Lo schema di destinazione &quot;[!UICONTROL Hotels]&quot; è basato su una classe &quot;[!UICONTROL Hotels]&quot; personalizzata e contiene campi che descrivono un hotel. Il campo &quot;[!UICONTROL email]&quot; funge da identità principale per lo schema nello spazio dei nomi &quot;[!UICONTROL Email]&quot;. Come &quot;[!UICONTROL Loyalty Members]&quot;, anche questo schema è stato abilitato per [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Creazione di un mixin di relazione

>[!NOTE]
>
>Questo passaggio è richiesto solo se lo schema di origine non dispone di un campo di tipo stringa dedicato da utilizzare come riferimento a un altro schema. Se questo campo è già definito nello schema di origine, passare alla fase successiva della [definizione di un campo](#relationship-field)di relazione.

Per definire una relazione tra due schemi, lo schema di origine deve avere un campo dedicato da utilizzare come riferimento allo schema di destinazione. È possibile aggiungere questo campo allo schema di origine creando un nuovo mixin.

Per iniziare, fai clic **[!UICONTROL Add]** nella _[!UICONTROL Mixins]_sezione.

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Viene visualizzata _[!UICONTROL Add Mixin]_la finestra di dialogo. Da qui, clicca **[!UICONTROL Create New Mixin]**. Nei campi di testo visualizzati, immettete un nome visualizzato e una descrizione per il nuovo mixin. Al termine fai clic su **[!UICONTROL Add Mixin]**(Continua).

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Il quadro viene nuovamente visualizzato con &quot;[!UICONTROL Loyalty Relationship]&quot; nella _[!UICONTROL Mixins]_sezione. Fate clic sul nome del mixin, quindi fate clic **[!UICONTROL Add Field]**accanto al campo &quot;[!UICONTROL Loyalty Members]&quot; di livello principale.

![](../images/tutorials/relationship/loyalty-add-field.png)

Un nuovo campo viene visualizzato nell&#39;area di lavoro sotto lo spazio dei nomi &quot;\_tenantId&quot;. In _[!UICONTROL Field Properties]_, specificare un nome di campo e un nome visualizzato per il campo, quindi impostare il tipo su &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Al termine, fai clic su **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Il campo &quot;[!UICONTROL favoriteHotel]&quot; aggiornato viene visualizzato nel quadro. Fare clic **[!UICONTROL Save]** per finalizzare le modifiche allo schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definire un campo relazione per lo schema di origine {#relationship-field}

Una volta definito un campo di riferimento dedicato nello schema di origine, è possibile specificarlo come campo di relazione.

Selezionate il campo di riferimento nel quadro, quindi scorrete verso il basso sotto _[!UICONTROL Field Properties]_fino a visualizzare la **[!UICONTROL Relationship]**casella di controllo. Selezionate la casella di controllo per visualizzare i parametri richiesti per la configurazione di un campo di relazione.

![](../images/tutorials/relationship/relationship-checkbox.png)

Selezionare il menu a discesa per **[!UICONTROL Reference Schema]** e selezionare lo schema di destinazione per la relazione (&quot;[!UICONTROL Hotels]&quot; in questo esempio). Se lo schema di destinazione è abilitato per il profilo, il **[!UICONTROL Reference Identity Namespace]** campo viene automaticamente impostato sullo spazio dei nomi dell&#39;identità primaria dello schema di destinazione. Se lo schema non dispone di un&#39;identità primaria definita, è necessario selezionare manualmente dal menu a discesa lo spazio dei nomi che si intende utilizzare. Al termine fai clic su **[!UICONTROL Apply]** (Continua).

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Il campo viene visualizzato come una relazione nel quadro, con il nome e lo spazio dei nomi dell&#39;identità di riferimento dello schema di destinazione. Fate clic **[!UICONTROL Save]** per salvare le modifiche e completare il flusso di lavoro.

![](../images/tutorials/relationship/relationship-save.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una relazione uno-a-uno tra due schemi che utilizzano l&#39; [!DNL Schema Editor]. Per i passaggi su come definire le relazioni mediante l&#39;API, vedete l&#39;esercitazione sulla [definizione di una relazione mediante l&#39;API](relationship-api.md)del Registro di sistema dello schema.