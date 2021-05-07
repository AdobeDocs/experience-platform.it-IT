---
keywords: Experience Platform;home;argomenti popolari;interfaccia utente;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;editor schema;Editor schema;schema;schema;schemi;schemi;schemi;creare;relazione;relazione;riferimento;riferimento;
solution: Experience Platform
title: Definire una relazione tra due schemi utilizzando l’Editor di schema
description: Questo documento fornisce un'esercitazione per definire una relazione tra due schemi utilizzando l'Editor di schema nell'interfaccia utente di Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 1%

---

# Definire una relazione tra due schemi utilizzando [!DNL Schema Editor]

La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il tuo marchio attraverso vari canali è una parte importante di Adobe Experience Platform. La definizione di queste relazioni all’interno della struttura degli schemi [!DNL Experience Data Model] (XDM) consente di ottenere informazioni complesse sui dati dei clienti.

Mentre le relazioni dello schema possono essere dedotte mediante l&#39;uso dello schema di unione e di [!DNL Real-time Customer Profile], questo vale solo per gli schemi che condividono la stessa classe. Per stabilire una relazione tra due schemi appartenenti a classi diverse, è necessario aggiungere un campo di relazione dedicato a uno schema di origine che fa riferimento all&#39;identità di uno schema di destinazione.

Questo documento fornisce un&#39;esercitazione per definire una relazione tra due schemi che utilizzano l&#39;Editor di schema nell&#39;interfaccia utente [!DNL Experience Platform]. Per i passaggi sulla definizione delle relazioni tra schemi utilizzando l&#39;API, consulta l&#39;esercitazione su [definizione di una relazione utilizzando l&#39;API del Registro di sistema dello schema](relationship-api.md).

## Introduzione

Questa esercitazione richiede una buona comprensione di [!DNL XDM System] e dell’Editor di schema nell’ interfaccia utente di [!DNL Experience Platform] . Prima di iniziare questa esercitazione, consulta la seguente documentazione:

* [Sistema XDM in Experience Platform](../home.md): Panoramica di XDM e della sua implementazione in  [!DNL Experience Platform].
* [Nozioni di base sulla composizione](../schema/composition.md) dello schema: Introduzione dei blocchi costitutivi degli schemi XDM.
* [Crea uno schema utilizzando [!DNL Schema Editor]](create-schema-ui.md): Un tutorial che illustra le nozioni di base sull’utilizzo di  [!DNL Schema Editor].

## Definire uno schema di origine e di destinazione

È previsto che siano già stati creati i due schemi che verranno definiti nella relazione. A scopo dimostrativo, questo tutorial crea una relazione tra i membri del programma fedeltà di un&#39;organizzazione (definito in uno schema &quot;[!DNL Loyalty Members]&quot;) e il loro hotel preferito (definito in uno schema &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Per stabilire una relazione, entrambi gli schemi devono avere identità principali definite ed essere abilitati per [!DNL Real-time Customer Profile]. Per informazioni su come configurare di conseguenza gli schemi, consulta la sezione relativa all’ [abilitazione di uno schema da utilizzare in Profile](./create-schema-ui.md#profile) nell’esercitazione sulla creazione dello schema.

Le relazioni dello schema sono rappresentate da un campo dedicato all&#39;interno di uno **schema di origine** che fa riferimento a un altro campo all&#39;interno di uno **schema di destinazione**. Nei passaggi seguenti, &quot;[!DNL Loyalty Members]&quot; sarà lo schema di origine, mentre &quot;[!DNL Hotels]&quot; fungerà da schema di destinazione.

A scopo di riferimento, le sezioni seguenti descrivono la struttura di ogni schema utilizzato in questa esercitazione prima che sia stata definita una relazione.

### [!DNL Loyalty Members] schema

Lo schema di origine &quot;[!DNL Loyalty Members]&quot; è basato sulla classe [!DNL XDM Individual Profile] ed è lo schema creato nell&#39;esercitazione per [la creazione di uno schema nell&#39;interfaccia utente](create-schema-ui.md). Include un oggetto `loyalty` nello spazio dei nomi `_tenantId`, che include diversi campi specifici per la fidelizzazione. Uno di questi campi, `loyaltyId`, funge da identità principale per lo schema nello spazio dei nomi [!UICONTROL Email] . Come mostrato in **[!UICONTROL Schema Properties]**, questo schema è stato abilitato per l&#39;utilizzo in [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Lo schema di destinazione &quot;[!DNL Hotels]&quot; è basato su una classe &quot;[!DNL Hotels]&quot; personalizzata e contiene campi che descrivono un hotel. Il campo `hotelId` funge da identità principale per lo schema in uno spazio dei nomi `hotelId` personalizzato. Come lo schema [!DNL Loyalty Members], anche questo schema è stato abilitato per [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Creare un gruppo di campi schema di relazione

>[!NOTE]
>
>Questo passaggio è necessario solo se lo schema di origine non dispone di un campo di tipo stringa dedicato da utilizzare come riferimento allo schema di destinazione. Se questo campo è già definito nello schema di origine, passa al passaggio successivo di [definizione di un campo di relazione](#relationship-field).

Per definire una relazione tra due schemi, lo schema di origine deve disporre di un campo dedicato da utilizzare come riferimento allo schema di destinazione. È possibile aggiungere questo campo allo schema di origine creando un nuovo gruppo di campi dello schema.

Inizia selezionando **[!UICONTROL Add]** nella sezione **[!UICONTROL Field groups]** .

![](../images/tutorials/relationship/loyalty-add-field-group.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Add field group]. Da qui, seleziona **[!UICONTROL Create new field group]**. Nei campi di testo visualizzati, immettere un nome visualizzato e una descrizione per il nuovo gruppo di campi. Al termine, fai clic su **[!UICONTROL Add field groups]**.

![](../images/tutorials/relationship/create-field-group.png)

L&#39;area di lavoro viene visualizzata nuovamente con &quot;[!DNL Favorite Hotel]&quot; nella sezione **[!UICONTROL Field groups]**. Selezionare il nome del gruppo di campi, quindi selezionare **[!UICONTROL Add field]** accanto al campo a livello principale `Loyalty Members`.

![](../images/tutorials/relationship/loyalty-add-field.png)

Un nuovo campo viene visualizzato nell’area di lavoro sotto lo spazio dei nomi `_tenantId` . In **[!UICONTROL Field properties]**, specificare un nome di campo e un nome visualizzato per il campo e impostare il relativo tipo su &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Al termine, seleziona **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Il campo aggiornato `favoriteHotel` viene visualizzato nell’area di lavoro. Seleziona **[!UICONTROL Save]** per finalizzare le modifiche allo schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definire un campo di relazione per lo schema di origine {#relationship-field}

Una volta definito il campo di riferimento dedicato dello schema di origine, è possibile assegnarlo come campo di relazione.

Seleziona il campo `favoriteHotel` nell’area di lavoro, quindi scorri verso il basso sotto **[!UICONTROL Field properties]** fino a visualizzare la casella di controllo **[!UICONTROL Relationship]**. Selezionare la casella di controllo per visualizzare i parametri richiesti per la configurazione di un campo di relazione.

![](../images/tutorials/relationship/relationship-checkbox.png)

Seleziona il menu a discesa per **[!UICONTROL Reference schema]** e seleziona lo schema di destinazione per la relazione (&quot;[!DNL Hotels]&quot; in questo esempio). Se lo schema di destinazione è abilitato per [!DNL Profile], il campo **[!UICONTROL Reference identity namespace]** viene automaticamente impostato sullo spazio dei nomi dell&#39;identità principale dello schema di destinazione. Se nello schema non è definita un&#39;identità primaria, è necessario selezionare manualmente lo spazio dei nomi che si intende utilizzare dal menu a discesa. Al termine, fai clic su **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Il campo `favoriteHotel` viene ora evidenziato come una relazione nell’area di lavoro, mostrando il nome e lo spazio dei nomi dell’identità di riferimento dello schema di destinazione. Seleziona **[!UICONTROL Save]** per salvare le modifiche e completare il flusso di lavoro.

![](../images/tutorials/relationship/relationship-save.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente una relazione uno-a-uno tra due schemi utilizzando il tag [!DNL Schema Editor]. Per i passaggi su come definire le relazioni utilizzando l’API, consulta l’esercitazione su [definizione di una relazione utilizzando l’API del Registro di sistema dello schema](relationship-api.md).
