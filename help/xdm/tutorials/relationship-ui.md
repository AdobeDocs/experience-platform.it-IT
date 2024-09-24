---
keywords: Experience Platform;home;argomenti popolari;ui;interfaccia utente;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;data model;modello dati;modello dati;modello dati;editor schema;schema;schema;schemi;schemi;creare;relazione;riferimento;riferimento;
solution: Experience Platform
title: Definire una relazione tra due schemi utilizzando l’Editor di schema
description: Questo documento fornisce un tutorial per definire una relazione tra due schemi utilizzando l’Editor di schema nell’interfaccia utente di Experience Platform.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5f9fdc9eff4d8bba049c03058d24e80e9b89e953
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 9%

---

# Definire una relazione uno-a-uno tra due schemi utilizzando l’[!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="Relazioni tra gli schemi"
>abstract="Gli schemi appartenenti a classi diverse possono essere collegati contestualmente tramite campi di relazione, per creare regole di segmentazione più complesse. Per ulteriori informazioni sulle relazioni tra gli schemi, consulta la documentazione."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="Schema di riferimento"
>abstract="Seleziona lo schema con cui desideri stabilire una relazione. Questo schema può avere una classe diversa dallo schema attuale. Per ulteriori informazioni sulle relazioni tra gli schemi, consulta la documentazione."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="Spazio dei nomi delle identità di riferimento"
>abstract="Spazio dei nomi (tipo) per il campo di identità primaria dello schema di riferimento. Per poter partecipare a una relazione, nello schema di riferimento deve essere stato stabilito un campo di identità primaria. Per ulteriori informazioni sulle relazioni tra gli schemi, consulta la documentazione."

La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il brand attraverso vari canali è una parte importante di Adobe Experience Platform. La definizione di queste relazioni all&#39;interno della struttura degli schemi [!DNL Experience Data Model] (XDM) consente di ottenere informazioni complesse sui dati dei clienti.

Sebbene sia possibile dedurre le relazioni tra schemi tramite lo schema di unione e [!DNL Real-Time Customer Profile], questo vale solo per gli schemi che condividono la stessa classe. Per stabilire una relazione tra due schemi appartenenti a classi diverse, è necessario aggiungere a uno schema di origine un campo relazione dedicato che faccia riferimento all’identità dell’altro schema correlato.

>[!NOTE]
>
>Se gli schemi di origine e di destinazione appartengono entrambi alla stessa classe, deve essere utilizzato un campo relazione dedicato **non**. In questo caso, utilizza l’interfaccia utente dello schema di unione per visualizzare la relazione. Le istruzioni su come eseguire questa operazione sono disponibili nella sezione [visualizza relazioni](../../profile/ui/union-schema.md#view-relationships) della guida dell&#39;interfaccia utente dello schema di unione.

Questo documento fornisce un&#39;esercitazione per definire una relazione tra due schemi utilizzando l&#39;Editor di schema nell&#39;interfaccia utente [!DNL Experience Platform]. Per i passaggi relativi alla definizione delle relazioni tra schemi tramite l&#39;API, vedere il tutorial su [definizione di una relazione tramite l&#39;API Schema Registry](relationship-api.md).

>[!NOTE]
>
>Per i passaggi su come creare una relazione molti-a-uno in Adobe Real-time Customer Data Platform B2B Edition, consulta la guida sulla [creazione di relazioni B2B](./relationship-b2b.md).

## Introduzione

Questo tutorial richiede una buona conoscenza di [!DNL XDM System] e dell&#39;Editor di schema nell&#39;interfaccia utente di [!DNL Experience Platform]. Prima di iniziare questo tutorial, consulta la seguente documentazione:

* [Sistema XDM nell&#39;Experience Platform](../home.md): panoramica di XDM e della relativa implementazione in [!DNL Experience Platform].
* [Nozioni di base sulla composizione dello schema](../schema/composition.md): introduzione dei blocchi predefiniti degli schemi XDM.
* [Crea uno schema utilizzando  [!DNL Schema Editor]](create-schema-ui.md): un tutorial che illustra le nozioni di base sull&#39;utilizzo di [!DNL Schema Editor].

## Definire uno schema di origine e di riferimento

È previsto che tu abbia già creato i due schemi che verranno definiti nella relazione. A scopo dimostrativo, questa esercitazione crea una relazione tra i membri del programma fedeltà di un&#39;organizzazione (definito in uno schema &quot;[!DNL Loyalty Members]&quot;) e il loro hotel preferito (definito in uno schema &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Per stabilire una relazione, entrambi gli schemi devono avere identità primarie definite ed essere abilitati per [!DNL Real-Time Customer Profile]. Per istruzioni su come configurare di conseguenza gli schemi, consulta la sezione su [abilitazione di uno schema da utilizzare nel profilo](./create-schema-ui.md#profile) nell&#39;esercitazione per la creazione dello schema.

Le relazioni tra schemi sono rappresentate da un campo dedicato all&#39;interno di uno **schema di origine** che punta a un altro campo all&#39;interno di uno **schema di riferimento**. Nei passaggi seguenti, &quot;[!DNL Loyalty Members]&quot; sarà lo schema di origine, mentre &quot;[!DNL Hotels]&quot; fungerà da schema di riferimento.

Le sezioni seguenti descrivono la struttura di ogni schema utilizzato in questa esercitazione prima della definizione di una relazione.

### Schema [!DNL Loyalty Members]

Lo schema di origine &quot;[!DNL Loyalty Members]&quot; è basato sulla classe [!DNL XDM Individual Profile], contenente un campo che descrive i membri di un programma fedeltà. Uno di questi campi, `personalEmail.addess`, funge da identità primaria per lo schema nello spazio dei nomi [!UICONTROL E-mail]. Come visto in **[!UICONTROL Proprietà schema]**, questo schema è stato abilitato per l&#39;utilizzo in [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### Schema [!DNL Hotels]

Lo schema di riferimento &quot;[!DNL Hotels]&quot; è basato su una classe &quot;[!DNL Hotels]&quot; personalizzata e contiene campi che descrivono un hotel. Per poter partecipare a una relazione, lo schema di riferimento deve inoltre avere un&#39;identità primaria definita ed essere abilitato per [!UICONTROL Profilo]. In questo caso, `_tenantId.hotelId`funge da identità primaria per lo schema, utilizzando uno spazio dei nomi di identità &quot;[!DNL Hotel ID]&quot; personalizzato.

![Attiva per profilo](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Per informazioni su come creare spazi dei nomi di identità personalizzati, consulta la [documentazione di Identity Service](../../identity-service/features/namespaces.md#manage-namespaces).

## Creare un gruppo di campi relazione

>[!NOTE]
>
>Questo passaggio è necessario solo se lo schema di origine non dispone di un campo di tipo stringa dedicato da utilizzare come puntatore all’identità primaria dello schema di riferimento. Se questo campo è già definito nello schema di origine, passare al passaggio successivo di [definizione di un campo relazione](#relationship-field).

Per definire una relazione tra due schemi, lo schema di origine deve disporre di un campo dedicato che indicherà l’identità primaria dello schema di riferimento. È possibile aggiungere questo campo allo schema di origine creando un nuovo gruppo di campi schema o estendendone uno esistente.

Nel caso dello schema [!DNL Loyalty Members], verrà aggiunto un nuovo campo `preferredHotel` per indicare l&#39;hotel preferito del membro fedeltà per le visite aziendali. Per iniziare, seleziona l&#39;icona più (**+**) accanto al nome dello schema di origine.

![](../images/tutorials/relationship/loyalty-add-field.png)

Nell’area di lavoro viene visualizzato un nuovo segnaposto di campo. In **[!UICONTROL Proprietà campo]**, fornire un nome di campo e un nome visualizzato per il campo e impostarne il tipo su &quot;[!UICONTROL Stringa]&quot;. In **[!UICONTROL Assegna a]**, selezionare un gruppo di campi esistente da estendere o digitare un nome univoco per creare un nuovo gruppo di campi. In questo caso, viene creato un nuovo gruppo di campi &quot;[!DNL Preferred Hotel]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Al termine, selezionare **[!UICONTROL Applica]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Il campo `preferredHotel` aggiornato viene visualizzato nell&#39;area di lavoro, che si trova sotto un oggetto `_tenantId` poiché è un campo personalizzato. Seleziona **[!UICONTROL Salva]** per finalizzare le modifiche allo schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definire un campo relazione per lo schema di origine {#relationship-field}

Una volta definito un campo di riferimento dedicato per lo schema di origine, puoi designarlo come campo di relazione.

>[!NOTE]
>
>Le relazioni possono essere supportate solo nei campi stringa o matrice di stringhe.

Seleziona il campo `preferredHotel` nell&#39;area di lavoro, quindi seleziona **[!UICONTROL Aggiungi relazione]** nella barra laterale **[!UICONTROL Proprietà campo]**.

![L&#39;Editor di schema con la relazione Aggiungi evidenziata nella barra laterale delle proprietà del campo.](../images/tutorials/relationship/add-relationship.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Aggiungi relazione]. Da questa finestra di dialogo è possibile impostare i parametri richiesti per la configurazione di un campo relazione. Per gli utenti di Real-Time CDP B2C, puoi **only** impostare una relazione uno-a-uno tra lo schema di origine e quello di riferimento.

>[!NOTE]
>
>Se hai accesso a Real-Time CDP B2B Edition, puoi utilizzare i controlli della barra a destra dell&#39;area di lavoro per definire un campo di relazione e creare una relazione molti-a-uno utilizzando la [stessa finestra di dialogo](./relationship-b2b.md#relationship-field).

![Finestra di dialogo Aggiungi relazione.](../images/tutorials/relationship/add-relationship-dialog.png)

Utilizza il menu a discesa per **[!UICONTROL Schema di riferimento]** e seleziona lo schema di riferimento per la relazione (&quot;[!DNL Hotels]&quot; in questo esempio).

>[!NOTE]
>
>Solo gli schemi che contengono un’identità primaria sono inclusi nel menu a discesa dello schema di riferimento. Questa protezione impedisce la creazione accidentale di una relazione con uno schema non ancora configurato correttamente.

Lo spazio dei nomi dell&#39;identità dello schema di riferimento (in questo caso, &quot;[!DNL Hotel ID]&quot;) viene popolato automaticamente in **[!UICONTROL Spazio dei nomi dell&#39;identità di riferimento]**. Al termine, seleziona **[!UICONTROL Applica]**.

![La finestra di dialogo Aggiungi relazione con i parametri di relazione configurati e Applica evidenziati.](../images/tutorials/relationship/apply-relationship.png)

Il campo `preferredHotel` è ora evidenziato come relazione nell&#39;area di lavoro, con il nome dello schema di riferimento. Seleziona **[!UICONTROL Salva]** per salvare le modifiche e completare il flusso di lavoro.

![Editor schema con i riferimenti di relazione e Salva evidenziati.](../images/tutorials/relationship/relationship-save.png)

### Modifica un campo relazione esistente {#edit-relationship}

Per modificare lo schema di riferimento, selezionare un campo con una relazione esistente, quindi selezionare **[!UICONTROL Modifica relazione]** nella barra laterale **[!UICONTROL Proprietà campo]**.

![Editor di schema con relazione di modifica evidenziata.](../images/tutorials/relationship/edit-relationship.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Modifica relazione]. Da qui puoi seguire il processo descritto in [definizione di un campo relazione](#relationship-field) o eliminare la relazione. Selezionare **[!UICONTROL Elimina relazione]** per rimuovere la relazione con lo schema di riferimento.

![Finestra di dialogo Modifica relazione.](../images/tutorials/relationship/edit-relationship-dialog.png)

## Filtrare e cercare relazioni {#filter-and-search}

Puoi filtrare e cercare relazioni specifiche all&#39;interno degli schemi dalla scheda [!UICONTROL Relazioni] dell&#39;area di lavoro [!UICONTROL Schemi]. È possibile utilizzare questa visualizzazione per individuare e gestire rapidamente le relazioni. Per istruzioni dettagliate sulle opzioni di filtro, leggi il documento su [esplorazione delle risorse dello schema](../ui/explore.md#lookup).

![Scheda Relazioni nell&#39;area di lavoro Schemi.](../images/tutorials/relationship-b2b/relationship-tab.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una relazione uno-a-uno tra due schemi utilizzando [!DNL Schema Editor]. Per i passaggi su come definire le relazioni utilizzando l&#39;API, vedere l&#39;esercitazione su [definizione di una relazione mediante l&#39;API Schema Registry](relationship-api.md).
