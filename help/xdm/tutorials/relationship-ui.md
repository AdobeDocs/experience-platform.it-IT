---
keywords: Experience Platform;home;argomenti popolari;ui;interfaccia utente;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;data model;modello dati;modello dati;modello dati;editor schema;schema;schema;schemi;schemi;creare;relazione;riferimento;riferimento;
solution: Experience Platform
title: Definire una relazione tra due schemi utilizzando l’Editor di schema
description: Questo documento fornisce un tutorial per definire una relazione tra due schemi utilizzando l’Editor di schema nell’interfaccia utente di Experienci Platform.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 8b5c1776804bbacad5c3d72dd48c1716380cca79
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 10%

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

La capacità di comprendere le relazioni tra i clienti e le loro interazioni con il brand attraverso vari canali è una parte importante di Adobe Experience Platform. Definizione di queste relazioni all&#39;interno della struttura [!DNL Experience Data Model] Gli schemi (XDM) consentono di ottenere informazioni complesse sui dati dei clienti.

Anche se le relazioni tra schemi possono essere dedotte tramite l’utilizzo dello schema di unione e [!DNL Real-Time Customer Profile], applicabile solo agli schemi che condividono la stessa classe. Per stabilire una relazione tra due schemi appartenenti a classi diverse, è necessario aggiungere a uno schema di origine un campo relazione dedicato che faccia riferimento all’identità dell’altro schema correlato.

>[!NOTE]
>
>Se gli schemi di origine e di destinazione appartengono entrambi alla stessa classe, un campo relazione dedicato deve **non** essere utilizzati. In questo caso, utilizza l’interfaccia utente dello schema di unione per visualizzare la relazione. Le istruzioni per eseguire questa operazione sono reperibili nella sezione [visualizza relazioni](../../profile/ui/union-schema.md#view-relationships) sezione della guida dell’interfaccia utente dello schema di unione.

Questo documento fornisce un tutorial per definire una relazione tra due schemi utilizzando l’Editor di schema nel [!DNL Experience Platform] dell&#39;utente. Per informazioni sulla definizione delle relazioni tra schemi tramite l’API, consulta l’esercitazione su [definizione di una relazione tramite l’API Schema Registry](relationship-api.md).

>[!NOTE]
>
>Per i passaggi su come creare una relazione molti-a-uno in Adobe Real-time Customer Data Platform B2B Edition, consulta la guida su [creazione di relazioni B2B](./relationship-b2b.md).

## Introduzione

Questo tutorial richiede una buona conoscenza di [!DNL XDM System] e l’Editor di schema nel [!DNL Experience Platform] UI. Prima di iniziare questo tutorial, consulta la seguente documentazione:

* [Sistema XDM in Experience Platform](../home.md): panoramica di XDM e della relativa implementazione in [!DNL Experience Platform].
* [Nozioni di base sulla composizione dello schema](../schema/composition.md): introduzione dei blocchi predefiniti degli schemi XDM.
* [Creare uno schema utilizzando [!DNL Schema Editor]](create-schema-ui.md): tutorial che illustra le nozioni di base sull’utilizzo di [!DNL Schema Editor].

## Definire uno schema di origine e di riferimento

È previsto che tu abbia già creato i due schemi che verranno definiti nella relazione. A scopo dimostrativo, questa esercitazione crea una relazione tra i membri del programma fedeltà di un’organizzazione (definito in un’ &quot;[!DNL Loyalty Members]&quot;) e il loro hotel preferito (definito in una &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Per stabilire una relazione, entrambi gli schemi devono avere identità primarie definite ed essere abilitati per [!DNL Real-Time Customer Profile]. Consulta la sezione su [abilitazione di uno schema da utilizzare nel profilo](./create-schema-ui.md#profile) nell’esercitazione sulla creazione di schemi se hai bisogno di istruzioni su come configurare di conseguenza gli schemi.

Le relazioni tra schemi sono rappresentate da un campo dedicato all’interno di un **schema di origine** che punta a un altro campo all’interno di un **schema di riferimento**. Nei passaggi successivi, &quot;[!DNL Loyalty Members]&quot; sarà lo schema di origine, mentre &quot;[!DNL Hotels]&quot; fungerà da schema di riferimento.

Le sezioni seguenti descrivono la struttura di ogni schema utilizzato in questa esercitazione prima della definizione di una relazione.

### [!DNL Loyalty Members] schema

Lo schema di origine &quot;[!DNL Loyalty Members]&quot; si basa sul [!DNL XDM Individual Profile] classe, contenente un campo che descrive i membri di un programma fedeltà. Uno di questi campi, `personalEmail.addess`, funge da identità primaria per lo schema nella sezione [!UICONTROL E-mail] spazio dei nomi. Come mostrato nella **[!UICONTROL Proprietà schema]**, questo schema è stato abilitato per l’utilizzo in [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Lo schema di riferimento &quot;[!DNL Hotels]&quot; si basa su un personalizzato &quot;[!DNL Hotels]&quot; e contiene campi che descrivono un hotel. Per poter partecipare a una relazione, lo schema di riferimento deve anche avere un’identità primaria definita ed essere abilitato per [!UICONTROL Profilo]. In questo caso, `_tenantId.hotelId`funge da identità primaria per lo schema, utilizzando un tag personalizzato &quot;[!DNL Hotel ID]&quot; spazio dei nomi delle identità.

![Abilita per Profilo](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Per informazioni su come creare spazi dei nomi di identità personalizzati, consulta [Documentazione del servizio Identity](../../identity-service/namespaces.md#manage-namespaces).

## Creare un gruppo di campi relazione

>[!NOTE]
>
>Questo passaggio è necessario solo se lo schema di origine non dispone di un campo di tipo stringa dedicato da utilizzare come puntatore all’identità primaria dello schema di riferimento. Se questo campo è già definito nello schema di origine, passa al passaggio successivo di [definizione di un campo relazione](#relationship-field).

Per definire una relazione tra due schemi, lo schema di origine deve disporre di un campo dedicato che indicherà l’identità primaria dello schema di riferimento. È possibile aggiungere questo campo allo schema di origine creando un nuovo gruppo di campi schema o estendendone uno esistente.

Nel caso di [!DNL Loyalty Members] schema, un nuovo `preferredHotel` verrà aggiunto il campo per indicare l’hotel preferito dal membro fedeltà per le visite aziendali. Per iniziare, seleziona l’icona più (**+**) accanto al nome dello schema di origine.

![](../images/tutorials/relationship/loyalty-add-field.png)

Nell’area di lavoro viene visualizzato un nuovo segnaposto di campo. Sotto **[!UICONTROL Proprietà campo]**, fornire un nome di campo e un nome visualizzato per il campo e impostarne il tipo su &quot;[!UICONTROL Stringa]&quot;. Sotto **[!UICONTROL Assegna a]**, selezionare un gruppo di campi esistente da estendere o digitare un nome univoco per creare un nuovo gruppo di campi. In questo caso, un nuovo &quot;[!DNL Preferred Hotel]&quot;viene creato un gruppo di campi.

![](../images/tutorials/relationship/relationship-field-details.png)

Al termine, seleziona **[!UICONTROL Applica]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Il valore aggiornato `preferredHotel` viene visualizzato nell’area di lavoro, sotto a `_tenantId` poiché è un campo personalizzato. Seleziona **[!UICONTROL Salva]** per finalizzare le modifiche apportate allo schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definire un campo relazione per lo schema di origine {#relationship-field}

Una volta definito un campo di riferimento dedicato per lo schema di origine, puoi designarlo come campo di relazione.

>[!NOTE]
>
>I passaggi seguenti descrivono come definire un campo di relazione utilizzando i controlli nella barra a destra nell’area di lavoro. Se hai accesso a Real-Time CDP B2B Edition, puoi anche definire una relazione uno-a-uno utilizzando [stessa finestra](./relationship-b2b.md#relationship-field) come quando si creano relazioni molti-a-uno.

Seleziona la `preferredHotel` nell’area di lavoro, quindi scorri verso il basso in **[!UICONTROL Proprietà campo]** fino al **[!UICONTROL Relazione]** viene visualizzata la casella di controllo. Selezionare la casella di controllo per visualizzare i parametri richiesti per la configurazione di un campo relazione.

![](../images/tutorials/relationship/relationship-checkbox.png)

Seleziona il menu a discesa per **[!UICONTROL Schema di riferimento]** e seleziona lo schema di riferimento per la relazione (&quot;[!DNL Hotels]&quot; in questo esempio). Sotto **[!UICONTROL Spazio dei nomi dell’identità di riferimento]**, seleziona lo spazio dei nomi del campo di identità dello schema di riferimento (in questo caso, &quot;[!DNL Hotel ID]&quot;). Seleziona **[!UICONTROL Applica]** al termine.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Il `preferredHotel` viene ora evidenziato come relazione nell’area di lavoro, con il nome dello schema di riferimento. Seleziona **[!UICONTROL Salva]** per salvare le modifiche e completare il flusso di lavoro.

![](../images/tutorials/relationship/relationship-save.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente una relazione uno-a-uno tra due schemi utilizzando [!DNL Schema Editor]. Per i passaggi su come definire le relazioni utilizzando l’API, consulta l’esercitazione su [definizione di una relazione tramite l’API Schema Registry](relationship-api.md).
