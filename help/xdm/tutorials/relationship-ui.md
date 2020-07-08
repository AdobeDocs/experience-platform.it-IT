---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definire una relazione tra due schemi utilizzando l'Editor schema
topic: tutorials
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Definire una relazione tra due schemi utilizzando l&#39;Editor di schema

La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il tuo marchio attraverso vari canali è una parte importante del  Adobe Experience Platform. La definizione di queste relazioni all&#39;interno della struttura degli schemi del modello dati esperienza (XDM) consente di acquisire informazioni complesse sui dati dei clienti.

Questo documento fornisce un&#39;esercitazione per definire una relazione uno-a-uno tra due schemi definiti dall&#39;organizzazione mediante l&#39;Editor di schema nell&#39;interfaccia utente di Experience Platform . Per i passaggi sulla definizione delle relazioni di schema mediante l&#39;API, vedete l&#39;esercitazione sulla [definizione di una relazione mediante l&#39;API](relationship-api.md)del Registro di sistema dello schema.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita del sistema XDM e dell&#39;Editor di schema nell&#39;interfaccia utente  di Experience Platform. Prima di iniziare questa esercitazione, consulta la seguente documentazione:

* [Sistema XDM in  Experience Platform](../home.md): Panoramica di XDM e della relativa implementazione in  Experience Platform.
* [Nozioni di base sulla composizione](../schema/composition.md)dello schema: Introduzione dei blocchi costitutivi degli schemi XDM.
* [Creare uno schema utilizzando l&#39;Editor](create-schema-ui.md)schema: Esercitazione sulle nozioni di base dell&#39;utilizzo dell&#39;Editor di schema.

## Definire uno schema di origine e di destinazione

È previsto che siano già stati creati i due schemi che verranno definiti nella relazione. A scopo dimostrativo, questa esercitazione crea una relazione tra i membri del programma fedeltà di un&#39;organizzazione (definito in uno schema &quot;Membri fedeltà&quot;) e i loro alberghi preferiti (definiti in uno schema &quot;Hotel&quot;).

Le relazioni dello schema sono rappresentate da uno schema **di** origine con un campo che fa riferimento a un altro campo all&#39;interno di uno schema **di** destinazione. Nei passaggi successivi, &quot;Membri fedeltà&quot; sarà lo schema di origine, mentre &quot;Alberghi&quot; fungerà da schema di destinazione.

A scopo di riferimento, le sezioni seguenti descrivono la struttura di ogni schema utilizzato in questa esercitazione prima che sia stata definita una relazione.

### Schema Membri fedeltà

Lo schema di origine &quot;Membri fedeltà&quot; è lo schema creato nell&#39;esercitazione per [creare uno schema nell&#39;interfaccia utente](create-schema-ui.md). Include un oggetto &quot;fedeltà&quot; nello spazio dei nomi &quot;\_tenantId&quot;, che include diversi campi specifici per la fedeltà. Uno di questi campi, &quot;loyaltyId&quot;, funge da identità principale per lo schema nello spazio dei nomi &quot;Email&quot;. Come mostrato in Proprietà __ schema, questo schema è stato abilitato per l&#39;uso nel profilo [cliente](../../profile/home.md)in tempo reale.

![](../images/tutorials/relationship/loyalty-members.png)

### Hotels, schema

Lo schema di destinazione &quot;Hotel&quot; contiene campi che descrivono un hotel, che includono il suo indirizzo, il marchio, il numero di stanze e la classificazione a stella. Il campo &quot;hotelId&quot; funge da identità principale per lo schema nello spazio dei nomi &quot;ECID&quot;. A differenza di &quot;Membri fedeltà&quot;, questo schema non è stato abilitato per il profilo cliente in tempo reale.

![](../images/tutorials/relationship/hotels.png)

## Creazione di un mixin di relazione

>[!NOTE]
>
>Questo passaggio è richiesto solo se lo schema di origine non dispone di un campo di tipo stringa dedicato da utilizzare come riferimento a un altro schema. Se questo campo è già definito nello schema di origine, passare alla fase successiva della [definizione di un campo](#relationship-field)di relazione.

Per definire una relazione tra due schemi, lo schema di origine deve avere un campo dedicato da utilizzare come riferimento allo schema di destinazione. È possibile aggiungere questo campo allo schema di origine creando un nuovo mixin.

Per iniziare, fai clic su **Aggiungi** nella sezione _Mixins_ .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Viene visualizzata la finestra di dialogo _Aggiungi mixin_ . Da qui, fate clic su **Crea nuovo mixin**. Nei campi di testo visualizzati, immettete un nome visualizzato e una descrizione per il nuovo mixin. Al termine, fate clic su **Aggiungi mixin** .

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Il quadro viene nuovamente visualizzato con &quot;Relazione fedeltà&quot; nella sezione _Mixins_ . Fate clic sul nome del mixin, quindi fate clic su **Aggiungi campo** accanto al campo &quot;Membri fedeltà&quot; a livello principale.

![](../images/tutorials/relationship/loyalty-add-field.png)

Un nuovo campo viene visualizzato nell&#39;area di lavoro sotto lo spazio dei nomi &quot;\_tenantId&quot;. In Proprietà __ campo specificare un nome di campo e un nome visualizzato per il campo, quindi impostare il tipo su &quot;String&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Al termine, fate clic su **Applica**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Il campo &quot;loyaltyRelationship&quot; aggiornato viene visualizzato nel quadro. Fate clic su **Salva** per finalizzare le modifiche allo schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definire un campo relazione per lo schema di origine {#relationship-field}

Una volta definito un campo di riferimento dedicato nello schema di origine, è possibile specificarlo come campo di relazione.

Fare clic sul campo di riferimento nel quadro, quindi scorrere verso il basso in Proprietà __ campo fino a visualizzare la casella di controllo **Relazione** . Selezionate la casella di controllo per visualizzare i parametri richiesti per la configurazione di un campo di relazione.

![](../images/tutorials/relationship/relationship-checkbox.png)

Fare clic sul menu a discesa per Schema **di** riferimento e selezionare lo schema di destinazione per la relazione (&quot;Hotel&quot; in questo esempio). Se lo schema di destinazione è abilitato per l&#39;unione, il campo **Reference Identity Namespace** (Spazio dei nomi identità di riferimento) viene impostato automaticamente sullo spazio dei nomi dell&#39;identità primaria dello schema di destinazione. Se lo schema non dispone di un&#39;identità primaria definita, è necessario selezionare manualmente dal menu a discesa lo spazio dei nomi che si intende utilizzare. Click **Apply** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Il campo viene visualizzato come una relazione nel quadro, con il nome e lo spazio dei nomi dell&#39;identità di riferimento dello schema di destinazione. Fate clic su **Salva** per salvare le modifiche e completare il flusso di lavoro.

![](../images/tutorials/relationship/relationship-save.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una relazione uno-a-uno tra due schemi utilizzando l&#39;Editor di schema. Per i passaggi su come definire le relazioni mediante l&#39;API, vedete l&#39;esercitazione sulla [definizione di una relazione mediante l&#39;API](relationship-api.md)del Registro di sistema dello schema.