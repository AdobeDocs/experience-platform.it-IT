---
keywords: Experience Platform;argomenti popolari;XDM;XDM system;XDM profilo individuale;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience eventExperience event;XDM Experience Event;XDM ExperienceEvent;ExperienceEvent;Experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;schema;risoluzione dei problemi;FAQ;schema unione;PROFILO unione;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Guida alla risoluzione dei problemi del sistema XDM
description: Risposte alle domande frequenti su Experience Data Model (XDM), compresi i passaggi per risolvere gli errori API più comuni.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 83d3d31b2d24fd01876ff7b0f1c03a5670ed3845
workflow-type: tm+mt
source-wordcount: '2446'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi del sistema XDM

Questo documento contiene le risposte alle domande più frequenti su [!DNL Experience Data Model] (XDM) e sul sistema XDM in Adobe Experience Platform, inclusa una guida alla risoluzione dei problemi relativi agli errori più comuni. Per domande e risoluzione dei problemi relativi ad altri servizi Platform, consulta la [guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** è una specifica open-source che definisce schemi standardizzati per la gestione della customer experience. La metodologia su cui viene generato [!DNL Experience Platform], il **sistema XDM**, rende operativi [!DNL Experience Data Model] schemi per l&#39;utilizzo da parte dei servizi [!DNL Platform]. **[!DNL Schema Registry]** fornisce un&#39;interfaccia utente e un&#39;API RESTful per accedere a **[!DNL Schema Library]** entro [!DNL Experience Platform]. Per ulteriori informazioni, consulta la [documentazione XDM](home.md).

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande più frequenti sul sistema XDM e sull&#39;utilizzo dell&#39;API [!DNL Schema Registry].

## Nozioni di base sugli schemi

In questa sezione puoi trovare le risposte alle domande fondamentali sulla struttura dello schema, l’utilizzo dei campi e l’identificazione nel sistema XDM.

### Come si aggiungono campi a uno schema?

È possibile aggiungere campi a uno schema utilizzando un gruppo di campi schema. Ogni gruppo di campi è compatibile con una o più classi, consentendo l&#39;utilizzo del gruppo di campi in qualsiasi schema che implementa una di queste classi compatibili. Sebbene Adobe Experience Platform fornisca a diversi gruppi di campi del settore i propri campi predefiniti, è possibile aggiungere campi personalizzati a uno schema creando gruppi di campi personalizzati utilizzando l’API o l’interfaccia utente.

Per informazioni dettagliate sulla creazione di gruppi di campi nell&#39;API [!DNL Schema Registry], consulta la [guida dell&#39;endpoint del gruppo di campi](api/field-groups.md#create). Se utilizzi l&#39;interfaccia utente, consulta l&#39;[esercitazione sull&#39;editor di schemi](./tutorials/create-schema-ui.md).

### Quali sono gli utilizzi migliori per i gruppi di campi rispetto ai tipi di dati?

[I gruppi di campi](./schema/composition.md#field-group) sono componenti che definiscono uno o più campi in uno schema. I gruppi di campi impongono il modo in cui i loro campi vengono visualizzati nella gerarchia dello schema e pertanto presentano la stessa struttura in ogni schema in cui sono inclusi. I gruppi di campi sono compatibili solo con classi specifiche, identificate dal relativo attributo `meta:intendedToExtend`.

[I tipi di dati](./schema/composition.md#data-type) possono anche fornire uno o più campi per uno schema. Tuttavia, a differenza dei gruppi di campi, i tipi di dati non sono vincolati a una particolare classe. Questo rende i tipi di dati un’opzione più flessibile per descrivere strutture di dati comuni riutilizzabili in più schemi con classi potenzialmente diverse.

### Qual è l’ID univoco di uno schema?

Tutte le risorse [!DNL Schema Registry] (schemi, gruppi di campi, tipi di dati, classi) hanno un URI che funge da ID univoco a scopo di riferimento e ricerca. Quando si visualizza uno schema nell&#39;API, è possibile trovarlo negli attributi principali `$id` e `meta:altId`.

Per ulteriori informazioni, vedere la sezione [identificazione risorsa](api/getting-started.md#resource-identification) nella guida dell&#39;API [!DNL Schema Registry].

### Qual è la dimensione massima di un tipo di campo lungo?

Un tipo di campo lungo è un numero intero con una dimensione massima di 53 (+1) bit, che può essere compreso tra -9007199254740992 e 9007199254740992. Ciò è dovuto a una limitazione del modo in cui le implementazioni JavaScript di JSON rappresentano i numeri interi lunghi.

Per ulteriori informazioni sui tipi di campo, consulta il documento sui [vincoli per i tipi di campo XDM](./schema/field-constraints.md).

### Cos’è meta:AltId e come posso recuperarlo?

`meta:altId` è un identificatore univoco per uno schema. `meta:altId` fornisce un ID di riferimento semplice da utilizzare nelle chiamate API. Questo ID evita la necessità di codificarlo/decodificarlo ogni volta che viene utilizzato come con il formato URI JSON.
<!-- (Needs clarification - How do I retrieve it INCOMPLETE) ... -->

<!-- ### How can I generate a sample payload for a schema? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

### È possibile ottenere una rappresentazione JSON di esempio per creare un tipo di dati?

Per creare un tipo di dati, puoi utilizzare sia l’API Schema Registry che l’interfaccia utente di Platform. Consulta la documentazione per istruzioni su come:

- [Creare un tipo di dati utilizzando l’API](./api/data-types.md#create)
- [Creare un tipo di dati tramite l’interfaccia utente](./ui/resources/data-types.md#create)

### Quali sono le restrizioni di utilizzo per un tipo di dati mappa?

XDM pone le seguenti restrizioni sull’utilizzo di questo tipo di dati:

- I tipi di mappa DEVONO essere di tipo oggetto.
- I tipi di mappa NON DEVONO avere proprietà definite (in altre parole, definiscono oggetti &quot;vuoti&quot;).
- I tipi di mappa DEVONO includere un campo additionalProperties.type che descrive i valori che possono essere inseriti nella mappa, stringa o numero intero.
- La segmentazione multi-entità può essere definita solo in base alle chiavi della mappa e non ai valori.
- Le mappe non sono supportate per i tipi di pubblico dell’account.

Per ulteriori dettagli, vedere le [restrizioni di utilizzo per gli oggetti mappa](./ui/fields/map.md#restrictions).

>[!NOTE]
>
>Mappe a più livelli o mappe di mappe non sono supportate.

<!-- You cannot create a complex map object. However, you can define map fields in the Schema Editor. See the guide on [defining map fields in the UI](./ui/fields/map.md) for more information. -->

<!-- ### How do I create a complex map object using APIs? -->

<!-- You cannot create a complex map object. -->

<!-- ### How can I manage schema inheritance in Adobe Experience Platform? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

## Identity Management schema

Questa sezione contiene le risposte alle domande più frequenti sulla definizione e la gestione delle identità all’interno degli schemi.

### Come posso definire le identità per il mio schema?

In [!DNL Experience Platform], le identità vengono utilizzate per identificare un soggetto (in genere una singola persona) indipendentemente dalle origini dei dati interpretate. Vengono definiti negli schemi contrassegnando i campi chiave come &quot;Identità&quot;. I campi comunemente utilizzati per l&#39;identità includono l&#39;indirizzo e-mail, il numero di telefono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it), l&#39;ID del sistema di gestione delle relazioni con i clienti e altri campi ID univoci.

I campi possono essere contrassegnati come identità utilizzando l’API o l’interfaccia utente di.

### Definizione delle identità nell’API

Nell’API, le identità vengono stabilite creando i descrittori di identità. I descrittori di identità segnalano che una particolare proprietà per uno schema è un identificatore univoco.

I descrittori di identità vengono creati da una richiesta POST all’endpoint /descriptors. In caso di esito positivo, riceverai un oggetto HTTP Status 201 (Creato) e un oggetto di risposta contenente i dettagli del nuovo descrittore.

Per ulteriori dettagli sulla creazione di descrittori di identità nell&#39;API, consulta il documento sulla sezione [descriptors](api/descriptors.md) nella guida per gli sviluppatori di [!DNL Schema Registry].

### Definizione delle identità nell’interfaccia utente

Con lo schema aperto nell&#39;Editor schemi, seleziona il campo nella sezione **[!UICONTROL Struttura]** dell&#39;editor che desideri contrassegnare come identità. In **[!UICONTROL Proprietà campo]** sul lato destro, selezionare la casella di controllo **[!UICONTROL Identità]**.

Per ulteriori dettagli sulla gestione delle identità nell&#39;interfaccia utente, vedere la sezione relativa alla [definizione dei campi di identità](./tutorials/create-schema-ui.md#identity-field) nell&#39;esercitazione sull&#39;editor di schema.

### Il mio schema richiede un’identità primaria?

Le identità primarie sono facoltative, poiché gli schemi possono avere zero o uno di essi. Tuttavia, uno schema deve avere un&#39;identità primaria per poter essere abilitato per l&#39;utilizzo in [!DNL Real-Time Customer Profile]. Per ulteriori informazioni, consulta la sezione [identity](./tutorials/create-schema-ui.md#identity-field) dell&#39;esercitazione sull&#39;editor di schema.

## Abilitazione profilo schema

Questa sezione fornisce indicazioni sull’abilitazione degli schemi per l’utilizzo con Real-Time Customer Profile.

### Come si abilita uno schema da utilizzare in [!DNL Real-Time Customer Profile]?

Gli schemi sono abilitati per l&#39;utilizzo in [[!DNL Real-Time Customer Profile]](../profile/home.md) tramite l&#39;aggiunta di un tag &quot;union&quot; nell&#39;attributo `meta:immutableTags` dello schema. L&#39;abilitazione di uno schema per l&#39;utilizzo con [!DNL Profile] può essere eseguita utilizzando l&#39;API o l&#39;interfaccia utente.

### Abilitazione di uno schema esistente per [!DNL Profile] tramite l&#39;API

Effettuare una richiesta PATCH per aggiornare lo schema e aggiungere l&#39;attributo `meta:immutableTags` come array contenente il valore &quot;union&quot;. Se l’aggiornamento ha esito positivo, la risposta mostrerà lo schema aggiornato che ora contiene il tag di unione.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;API per abilitare uno schema da utilizzare in [!DNL Real-Time Customer Profile], vedere il documento [unions](./api/unions.md) della Guida per gli sviluppatori di [!DNL Schema Registry].

### Abilitazione di uno schema esistente per [!DNL Profile] tramite l&#39;interfaccia utente

In [!DNL Experience Platform], selezionare **[!UICONTROL Schemi]** nell&#39;area di navigazione a sinistra e selezionare il nome dello schema che si desidera abilitare dall&#39;elenco degli schemi. Quindi, sul lato destro dell&#39;editor in **[!UICONTROL Proprietà schema]**, seleziona **[!UICONTROL Profilo]** per attivarlo.

Per ulteriori informazioni, vedere la sezione sull&#39;[utilizzo in Real-Time Customer Profile](./tutorials/create-schema-ui.md#profile) nell&#39;esercitazione [!UICONTROL Schema Editor].

### Quando i dati di Adobe Analytics vengono importati come origine, lo schema creato automaticamente è abilitato per il profilo?

Lo schema non viene abilitato automaticamente per Real-Time Customer Profile. Devi abilitare esplicitamente il set di dati per il profilo in base allo schema abilitato per il profilo. Consulta la documentazione per scoprire i [passaggi e requisiti necessari per abilitare un set di dati da utilizzare in Real-Time Customer Profile](../catalog/datasets/user-guide.md#enable-profile).

### Posso eliminare gli schemi abilitati per il profilo?

Non puoi eliminare uno schema dopo che è stato abilitato per Real-Time Customer Profile. Una volta abilitato uno schema per il profilo, non è possibile disattivarlo o eliminarlo né rimuovere campi dallo schema. Pertanto, è fondamentale pianificare e verificare attentamente la configurazione dello schema prima di abilitarla per il profilo. Tuttavia, puoi eliminare un set di dati abilitato per il profilo. Le informazioni si trovano qui: <https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/user-guide#delete-a-profile-enabled-dataset>

>[!IMPORTANT]
>
>Per rimuovere uno schema abilitato per il profilo, è necessario l’aiuto del team di supporto della piattaforma XDM e procedere come segue:
>
> 1. Elimina tutti i set di dati associati allo schema (abilitato per Profilo)
> 2. Elimina lo snapshot di esportazione del profilo dalla sandbox (richiede l’aiuto del team di supporto della piattaforma XDM)
> 3. Forza eliminazione schema dalla sandbox (operazione che può essere eseguita solo dal team di supporto della piattaforma XDM)

## Modifica e restrizioni dello schema

Questa sezione fornisce chiarimenti sulle regole di modifica dello schema e sulla prevenzione dell’interruzione delle modifiche.

### Quando uno schema inizia a impedire l’interruzione delle modifiche?

È possibile apportare modifiche che causano interruzioni a uno schema se non è mai stato utilizzato nella creazione di un set di dati o abilitato per l&#39;utilizzo in [[!DNL Real-Time Customer Profile]](../profile/home.md). Una volta che uno schema è stato utilizzato nella creazione di set di dati o abilitato per l&#39;utilizzo con [!DNL Real-Time Customer Profile], le regole di [Schema Evolution](schema/composition.md#evolution) vengono rigorosamente applicate dal sistema.

### Posso modificare direttamente uno schema di unione?

Gli schemi di unione sono di sola lettura e vengono generati automaticamente dal sistema. Non possono essere modificati direttamente. Gli schemi di unione vengono creati per una classe specifica quando un tag &quot;union&quot; viene aggiunto allo schema che implementa tale classe.

Per ulteriori informazioni sulle unioni in XDM, consulta la sezione [unioni](./api/unions.md) nella guida dell&#39;API [!DNL Schema Registry].

### Come posso formattare il file di dati per acquisire i dati nel mio schema?

[!DNL Experience Platform] accetta file di dati in formato [!DNL Parquet] o JSON. Il contenuto di questi file deve essere conforme allo schema a cui fa riferimento il set di dati. Per informazioni dettagliate sulle best practice per l&#39;acquisizione dei file di dati, consulta la [panoramica sull&#39;acquisizione batch](../ingestion/home.md).

### Come posso convertire uno schema in uno schema di sola lettura?

Al momento non è possibile convertire uno schema in sola lettura.

## Errori e risoluzione problemi

Di seguito è riportato un elenco di messaggi di errore che è possibile visualizzare durante l&#39;utilizzo dell&#39;API [!DNL Schema Registry].

### Risorsa non trovata

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

Questo errore viene visualizzato quando il sistema non è riuscito a trovare una particolare risorsa. È possibile che la risorsa sia stata eliminata o che il percorso nella chiamata API non sia valido. Prima di riprovare, assicurati di aver inserito un percorso valido per la chiamata API. Puoi verificare di aver immesso l’ID corretto per la risorsa e che il percorso abbia un namespace corretto con il contenitore appropriato (globale o tenant).

>[!NOTE]
>
>A seconda del tipo di risorsa da recuperare, questo errore può utilizzare uno qualsiasi dei seguenti `type` URI:
>
>- `http://ns.adobe.com/aep/errors/XDM-1010-404`
>- `http://ns.adobe.com/aep/errors/XDM-1011-404`
>- `http://ns.adobe.com/aep/errors/XDM-1012-404`
>- `http://ns.adobe.com/aep/errors/XDM-1013-404`
>- `http://ns.adobe.com/aep/errors/XDM-1014-404`
>- `http://ns.adobe.com/aep/errors/XDM-1015-404`
>- `http://ns.adobe.com/aep/errors/XDM-1016-404`
>- `http://ns.adobe.com/aep/errors/XDM-1017-404`

Per ulteriori informazioni sulla costruzione dei percorsi di ricerca nell&#39;API, vedere le sezioni [container](./api/getting-started.md#container) e [resource identifier](api/getting-started.md#resource-identification) nella guida per gli sviluppatori [!DNL Schema Registry].

### Titolo non univoco

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

Questo messaggio di errore viene visualizzato quando si tenta di creare una risorsa con un titolo già utilizzato da un’altra risorsa. I titoli devono essere univoci per tutti i tipi di risorse. Ad esempio, se tenti di creare un gruppo di campi con un titolo già utilizzato da uno schema, riceverai questo errore.

### Errore di convalida dello spazio dei nomi

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

Questo messaggio di errore viene visualizzato quando si tenta di creare una risorsa con campi con spazio dei nomi errato o di aggiungere campi con spazio dei nomi errato a una risorsa esistente.

Le risorse definite dall’organizzazione devono assegnare uno spazio dei nomi ai relativi campi sotto l’ID tenant, al fine di evitare conflitti con altre risorse del settore e del fornitore. Quando crei uno schema utilizzando gruppi di campi standard, anche tutti i campi personalizzati aggiunti all’interno della struttura di tali gruppi di campi devono avere lo spazio dei nomi sotto l’ID tenant.

>[!NOTE]
>
>A seconda della natura specifica dell&#39;errore dello spazio dei nomi, questo errore può utilizzare uno qualsiasi dei seguenti URI `type` insieme a dettagli di messaggio diversi:
>
>- `http://ns.adobe.com/aep/errors/XDM-1020-400`
>- `http://ns.adobe.com/aep/errors/XDM-1021-400`
>- `http://ns.adobe.com/aep/errors/XDM-1022-400`
>- `http://ns.adobe.com/aep/errors/XDM-1023-400`
>- `http://ns.adobe.com/aep/errors/XDM-1024-400`

Esempi dettagliati delle strutture di dati corrette per le risorse XDM sono disponibili nella guida dell’API del registro dello schema:

- [Creare una classe personalizzata](./api/classes.md#create)
- [Creare un gruppo di campi personalizzato](./api/field-groups.md#create)
- [Creare un tipo di dati personalizzato](./api/data-types.md#create)

### Intestazione Accept non valida

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

Le richieste GET nell&#39;API [!DNL Schema Registry] richiedono un&#39;intestazione `Accept` per poter determinare come formattare la risposta. Questo errore si verifica quando un&#39;intestazione `Accept` richiesta non è valida o è mancante.

A seconda dell&#39;endpoint utilizzato, la proprietà `detailed-message` indica l&#39;aspetto di un&#39;intestazione `Accept` valida per una risposta corretta. Verificare di aver immesso correttamente un&#39;intestazione `Accept` compatibile con la richiesta API che si sta tentando di eseguire prima di riprovare.

>[!NOTE]
>
>A seconda dell&#39;endpoint utilizzato, questo errore può utilizzare uno qualsiasi dei seguenti URI `type`:
>
>- `http://ns.adobe.com/aep/errors/XDM-1006-400`
>- `http://ns.adobe.com/aep/errors/XDM-1007-400`
>- `http://ns.adobe.com/aep/errors/XDM-1008-400`
>- `http://ns.adobe.com/aep/errors/XDM-1009-400`

Per gli elenchi di intestazioni compatibili di Accept per diverse richieste API, fare riferimento alle sezioni corrispondenti nella [Guida per gli sviluppatori del registro dello schema](./api/overview.md).

### [!DNL Real-Time Customer Profile] errori

I seguenti messaggi di errore sono associati alle operazioni necessarie per abilitare gli schemi per [!DNL Real-Time Customer Profile]. Per ulteriori informazioni, consulta la sezione [unions](./api/unions.md) nella guida dell&#39;API [!DNL Schema Registry].

#### Deve essere presente un descrittore di identità di riferimento

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema per [!DNL Profile] e una delle relative proprietà contiene un descrittore di relazione senza un descrittore di identità di riferimento. Per risolvere l’errore, aggiungi un descrittore di identità di riferimento al campo dello schema in questione.

#### Gli spazi dei nomi del campo del descrittore dell’identità di riferimento e dello schema di destinazione devono corrispondere

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

>[!NOTE]
>
>Per questo errore, lo &quot;schema di destinazione&quot; fa riferimento allo schema di riferimento nella relazione.

Per abilitare gli schemi che contengono descrittori di relazione da utilizzare in [!DNL Profile], lo spazio dei nomi del campo di origine e lo spazio dei nomi primario del campo di riferimento devono essere uguali. Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema che contiene uno spazio dei nomi senza corrispondenza per il relativo descrittore di identità di riferimento.

Per risolvere il problema, verificare che il valore `xdm:namespace` del campo di identità dello schema di riferimento corrisponda a quello della proprietà `xdm:identityNamespace` nel descrittore di identità di riferimento del campo di origine.

Per un elenco dei codici dello spazio dei nomi di identità standard, vedere la sezione relativa agli [spazi dei nomi standard](../identity-service/features/namespaces.md) nella panoramica dello spazio dei nomi delle identità.

#### Lo schema deve includere un identityMap o un’identità primaria

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

Prima di abilitare uno schema per il profilo, devi [creare un descrittore di identità primaria](./api/descriptors.md#create) per lo schema oppure includere un campo di mappa identità per agire sull&#39;identità primaria.

#### Impossibile unire tipi di dati non compatibili

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

Tutti gli schemi abilitati per il profilo appartenenti alla stessa classe devono essere in grado di unirsi per creare lo schema di unione per tale classe. Questo errore viene visualizzato quando si tenta di aggiungere un campo a uno schema il cui percorso è condiviso da un altro schema abilitato per il profilo e il tipo di dati è diverso da quello originale. Poiché gli schemi sono entrambi abilitati per il profilo e contengono lo stesso percorso di campo, Profile tenterà di unire questi due campi in uno durante la costruzione dello schema di unione. Poiché non è possibile unire diversi tipi di dati, questo viene considerato un conflitto di unione e non è consentito.

Per risolvere il problema, scegli un nome diverso per il campo o nidificalo in un oggetto con spazio dei nomi univoco al fine di evitare conflitti di unione con altri schemi abilitati per i profili nella stessa classe con campi simili.
