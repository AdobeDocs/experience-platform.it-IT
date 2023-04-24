---
keywords: Experience Platform;home;argomenti popolari;interfaccia utente;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;editor schema;Editor schema;schema;schema;schemi;schemi;schemi;creare;relazione;relazione;riferimento;riferimento;
solution: Experience Platform
title: Definire una relazione tra due schemi utilizzando l’Editor di schema
description: Questo documento fornisce un'esercitazione per definire una relazione tra due schemi utilizzando l'Editor di schema nell'interfaccia utente di Experience Platform.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 9%

---

# Definire una relazione uno-a-uno tra due schemi utilizzando il [!DNL Schema Editor] {#relationship-ui}

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

La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il tuo marchio attraverso vari canali è una parte importante di Adobe Experience Platform. Definizione di queste relazioni all’interno della struttura [!DNL Experience Data Model] Gli schemi (XDM) ti consentono di ottenere informazioni complesse sui dati dei clienti.

Mentre le relazioni dello schema possono essere dedotte mediante l&#39;uso dello schema dell&#39;unione e [!DNL Real-Time Customer Profile], questo vale solo per gli schemi che condividono la stessa classe. Per stabilire una relazione tra due schemi appartenenti a classi diverse, è necessario aggiungere un campo di relazione dedicato a uno schema di origine che fa riferimento all&#39;identità dell&#39;altro schema correlato.

Questo documento fornisce un&#39;esercitazione per definire una relazione tra due schemi che utilizzano l&#39;Editor di schema nel [!DNL Experience Platform] interfaccia utente. Per i passaggi sulla definizione delle relazioni tra schemi utilizzando l’API, consulta l’esercitazione su [definizione di una relazione utilizzando l’API del Registro di sistema dello schema](relationship-api.md).

>[!NOTE]
>
>Per i passaggi su come creare una relazione molti-a-uno in Adobe Real-time Customer Data Platform B2B Edition, consulta la guida su [creazione di relazioni B2B](./relationship-b2b.md).

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei [!DNL XDM System] e nell’Editor di schema in [!DNL Experience Platform] Interfaccia utente. Prima di iniziare questa esercitazione, consulta la seguente documentazione:

* [Sistema XDM in Experience Platform](../home.md): Panoramica di XDM e della sua implementazione in [!DNL Experience Platform].
* [Nozioni di base sulla composizione dello schema](../schema/composition.md): Introduzione dei blocchi costitutivi degli schemi XDM.
* [Creare uno schema utilizzando [!DNL Schema Editor]](create-schema-ui.md): Un tutorial che illustra le nozioni di base sull’utilizzo delle [!DNL Schema Editor].

## Definire uno schema di origine e di riferimento

È previsto che siano già stati creati i due schemi che verranno definiti nella relazione. A scopo dimostrativo, questo tutorial crea una relazione tra i membri del programma fedeltà di un&#39;organizzazione (definito in &quot;[!DNL Loyalty Members]&quot; schema) e il loro hotel preferito (definito in un &quot;[!DNL Hotels]&quot; schema).

>[!IMPORTANT]
>
>Per stabilire una relazione, entrambi gli schemi devono avere identità principali definite e devono essere abilitati per [!DNL Real-Time Customer Profile]. Vedi la sezione su [abilitazione di uno schema da utilizzare nel profilo](./create-schema-ui.md#profile) nell’esercitazione sulla creazione dello schema, se hai bisogno di indicazioni su come configurare gli schemi di conseguenza.

Le relazioni dello schema sono rappresentate da un campo dedicato all’interno di un **schema di origine** che punta a un altro campo all&#39;interno di un **schema di riferimento**. Nei passi successivi, &quot;[!DNL Loyalty Members]&quot; sarà lo schema di origine, mentre &quot;[!DNL Hotels]&quot; fungerà da schema di riferimento.

Le sezioni seguenti descrivono la struttura di ogni schema utilizzato in questa esercitazione prima che sia stata definita una relazione.

### [!DNL Loyalty Members] schema

Lo schema di origine &quot;[!DNL Loyalty Members]&quot; si basa sul [!DNL XDM Individual Profile] Classe, contenente un campo che descrive i membri di un programma fedeltà. Uno di questi campi, `personalEmail.addess`, funge da identità principale per lo schema in [!UICONTROL E-mail] spazio dei nomi. Come visto sotto **[!UICONTROL Proprietà schema]**, questo schema è stato abilitato per l&#39;utilizzo in [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Schema di riferimento &quot;[!DNL Hotels]&quot; si basa su un &quot;[!DNL Hotels]&quot; classe e contiene campi che descrivono un hotel. Per partecipare a una relazione, lo schema di riferimento deve avere anche un&#39;identità primaria definita ed abilitata per [!UICONTROL Profilo]. In questo caso, `_tenantId.hotelId`agisce come identità principale per lo schema, utilizzando un &quot;[!DNL Hotel ID]&quot; namespace identity.

![Abilita per Profilo](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Per informazioni su come creare spazi dei nomi di identità personalizzati, consulta [Documentazione del servizio Identity](../../identity-service/namespaces.md#manage-namespaces).

## Creare un gruppo di campi di relazione

>[!NOTE]
>
>Questo passaggio è necessario solo se lo schema di origine non dispone di un campo di tipo stringa dedicato da utilizzare come puntatore all&#39;identità primaria dello schema di riferimento. Se questo campo è già definito nello schema di origine, passa al passaggio successivo di [definizione di un campo relazione](#relationship-field).

Per definire una relazione tra due schemi, lo schema di origine deve disporre di un campo dedicato che indichi l’identità principale dello schema di riferimento. È possibile aggiungere questo campo allo schema di origine creando un nuovo gruppo di campi dello schema o estendendone uno esistente.

Nel caso di [!DNL Loyalty Members] schema, nuovo `preferredHotel` verrà aggiunto un campo per indicare l’hotel preferito del membro fedeltà per le visite aziendali. Inizia selezionando l’icona più (**+**) accanto al nome dello schema di origine.

![](../images/tutorials/relationship/loyalty-add-field.png)

Nell’area di lavoro viene visualizzato un nuovo segnaposto campo. Sotto **[!UICONTROL Proprietà campo]**, fornire un nome di campo e un nome visualizzato per il campo e impostarne il tipo su &quot;[!UICONTROL Stringa]&quot;. Sotto **[!UICONTROL Assegna a]**, seleziona un gruppo di campi esistente da estendere o digita un nome univoco per creare un nuovo gruppo di campi. In questo caso, un nuovo &quot;[!DNL Preferred Hotel]&quot; viene creato un gruppo di campi.

![](../images/tutorials/relationship/relationship-field-details.png)

Al termine, seleziona **[!UICONTROL Applica]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Il `preferredHotel` il campo viene visualizzato nell&#39;area di lavoro, situata sotto a `_tenantId` poiché si tratta di un campo personalizzato. Seleziona **[!UICONTROL Salva]** per finalizzare le modifiche allo schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definire un campo di relazione per lo schema di origine {#relationship-field}

Una volta definito il campo di riferimento dedicato dello schema di origine, è possibile assegnarlo come campo di relazione.

>[!NOTE]
>
>I passaggi seguenti descrivono come definire un campo di relazione utilizzando i controlli della barra a destra nell’area di lavoro. Se hai accesso a Real-Time CDP B2B Edition, puoi anche definire una relazione uno-a-uno utilizzando la [stessa finestra di dialogo](./relationship-b2b.md#relationship-field) come quando si creano relazioni molti-a-uno.

Seleziona la `preferredHotel` nell’area di lavoro, quindi scorri verso il basso sotto **[!UICONTROL Proprietà campo]** fino al **[!UICONTROL Relazione]** viene visualizzata la casella di controllo . Selezionare la casella di controllo per visualizzare i parametri richiesti per la configurazione di un campo di relazione.

![](../images/tutorials/relationship/relationship-checkbox.png)

Seleziona il menu a discesa per **[!UICONTROL Schema di riferimento]** e selezionare lo schema di riferimento per la relazione (&quot;[!DNL Hotels]&quot; in questo esempio). Sotto **[!UICONTROL Spazio dei nomi identità di riferimento]**, seleziona lo spazio dei nomi del campo di identità dello schema di riferimento (in questo caso, &quot;[!DNL Hotel ID]&quot;). Seleziona **[!UICONTROL Applica]** una volta finito.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

La `preferredHotel` il campo viene ora evidenziato come una relazione nell&#39;area di lavoro, visualizzando il nome dello schema di riferimento. Seleziona **[!UICONTROL Salva]** per salvare le modifiche e completare il flusso di lavoro.

![](../images/tutorials/relationship/relationship-save.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una relazione uno-a-uno tra due schemi utilizzando [!DNL Schema Editor]. Per i passaggi su come definire le relazioni utilizzando l’API, consulta l’esercitazione su [definizione di una relazione utilizzando l’API del Registro di sistema dello schema](relationship-api.md).
