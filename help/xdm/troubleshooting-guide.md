---
keywords: Experience Platform;argomenti popolari;XDM;XDM system;XDM profilo individuale;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience eventExperience event;XDM Experience Event;XDM ExperienceEvent;ExperienceEvent;Experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;schema;risoluzione dei problemi;FAQ;schema unione;PROFILO unione;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Guida alla risoluzione dei problemi del sistema XDM
description: Risposte alle domande frequenti su Experience Data Model (XDM), compresi i passaggi per risolvere gli errori API più comuni.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi del sistema XDM

Questo documento fornisce le risposte alle domande più frequenti su [!DNL Experience Data Model] (XDM) e il sistema XDM in Adobe Experience Platform, inclusa una guida alla risoluzione dei problemi per gli errori più comuni. Per domande e risoluzione dei problemi relativi ad altri servizi Platform, consulta [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** è una specifica open-source che definisce schemi standardizzati per la gestione della customer experience. La metodologia su cui [!DNL Experience Platform] è stato creato, **Sistema XDM**, operazionalizza [!DNL Experience Data Model] schemi utilizzati da [!DNL Platform] servizi. Il **[!DNL Schema Registry]** fornisce un’interfaccia utente e un’API RESTful per accedere al **[!DNL Schema Library]** entro [!DNL Experience Platform]. Consulta la [Documentazione XDM](home.md) per ulteriori informazioni.

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande più frequenti sul sistema XDM e sull’utilizzo di [!DNL Schema Registry] API.

### Come si aggiungono campi a uno schema?

È possibile aggiungere campi a uno schema utilizzando un gruppo di campi schema. Ogni gruppo di campi è compatibile con una o più classi, consentendo l&#39;utilizzo del gruppo di campi in qualsiasi schema che implementa una di queste classi compatibili. Sebbene Adobe Experience Platform fornisca a diversi gruppi di campi del settore i propri campi predefiniti, è possibile aggiungere campi personalizzati a uno schema creando gruppi di campi personalizzati utilizzando l’API o l’interfaccia utente.

Per informazioni dettagliate sulla creazione di gruppi di campi in [!DNL Schema Registry] API, consulta [guida dell’endpoint del gruppo di campi](api/field-groups.md#create). Se utilizzi l’interfaccia utente, consulta la sezione [Esercitazione sull’editor di schemi](./tutorials/create-schema-ui.md).

### Quali sono gli utilizzi migliori per i gruppi di campi rispetto ai tipi di dati?

[Gruppi di campi](./schema/composition.md#field-group) sono componenti che definiscono uno o più campi in uno schema. I gruppi di campi impongono il modo in cui i loro campi vengono visualizzati nella gerarchia dello schema e pertanto presentano la stessa struttura in ogni schema in cui sono inclusi. I gruppi di campi sono compatibili solo con classi specifiche, identificate dalle rispettive `meta:intendedToExtend` attributo.

[Tipi di dati](./schema/composition.md#data-type) può anche fornire uno o più campi per uno schema. Tuttavia, a differenza dei gruppi di campi, i tipi di dati non sono vincolati a una particolare classe. Questo rende i tipi di dati un’opzione più flessibile per descrivere strutture di dati comuni riutilizzabili in più schemi con classi potenzialmente diverse.

### Qual è l’ID univoco di uno schema?

Tutti [!DNL Schema Registry] le risorse (schemi, gruppi di campi, tipi di dati, classi) hanno un URI che funge da ID univoco a scopo di riferimento e ricerca. Lo schema visualizzato nell’API si trova nel livello superiore `$id` e `meta:altId` attributi.

Per ulteriori informazioni, vedere [identificazione risorsa](api/getting-started.md#resource-identification) sezione nella sezione [!DNL Schema Registry] Guida API di.

### Quando uno schema inizia a impedire l’interruzione delle modifiche?

È possibile apportare modifiche che causano interruzioni a uno schema purché non sia mai stato utilizzato nella creazione di un set di dati o abilitato per l’utilizzo in [[!DNL Real-Time Customer Profile]](../profile/home.md). Una volta che uno schema è stato utilizzato nella creazione di set di dati o abilitato per l’utilizzo con [!DNL Real-Time Customer Profile], le regole di [Evoluzione schema](schema/composition.md#evolution) essere rigorosamente applicate dal sistema.

### Qual è la dimensione massima di un tipo di campo lungo?

Un tipo di campo lungo è un numero intero con una dimensione massima di 53 (+1) bit, che può essere compreso tra -9007199254740992 e 9007199254740992. Ciò è dovuto a una limitazione del modo in cui le implementazioni JavaScript di JSON rappresentano i numeri interi lunghi.

Per ulteriori informazioni sui tipi di campo, consulta il documento su [Vincoli del tipo di campo XDM](./schema/field-constraints.md).

### Come posso definire le identità per il mio schema?

In entrata [!DNL Experience Platform], le identità vengono utilizzate per identificare un soggetto (in genere una singola persona) indipendentemente dalle fonti di dati interpretate. Vengono definiti negli schemi contrassegnando i campi chiave come &quot;Identità&quot;. I campi di uso comune per l’identità includono indirizzo e-mail, numero di telefono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it), ID CRM e altri campi ID univoci.

I campi possono essere contrassegnati come identità utilizzando l’API o l’interfaccia utente di.

#### Definizione delle identità nell’API

Nell’API, le identità vengono stabilite creando i descrittori di identità. I descrittori di identità segnalano che una particolare proprietà per uno schema è un identificatore univoco.

I descrittori di identità vengono creati da una richiesta POST all’endpoint /descriptors. In caso di esito positivo, riceverai un oggetto HTTP Status 201 (Creato) e un oggetto di risposta contenente i dettagli del nuovo descrittore.

Per ulteriori dettagli sulla creazione dei descrittori di identità nell’API, consulta il documento su [descrittori](api/descriptors.md) sezione nella sezione [!DNL Schema Registry] guida per gli sviluppatori.

#### Definizione delle identità nell’interfaccia utente

Con lo schema aperto nell’Editor di schema, seleziona il campo nella sezione **[!UICONTROL Struttura]** sezione dell’editor che desideri contrassegnare come identità. Sotto **[!UICONTROL Proprietà campo]** sul lato destro, seleziona la **[!UICONTROL Identità]** casella di controllo.

Per ulteriori dettagli sulla gestione delle identità nell’interfaccia utente, consulta la sezione su [definizione dei campi di identità](./tutorials/create-schema-ui.md#identity-field) nell’esercitazione dell’Editor di schema.

### Il mio schema richiede un’identità primaria?

Le identità primarie sono facoltative, poiché gli schemi possono avere zero o uno di essi. Tuttavia, uno schema deve avere un’identità primaria per essere abilitato all’utilizzo in [!DNL Real-Time Customer Profile]. Consulta la [identità](./tutorials/create-schema-ui.md#identity-field) sezione dell’esercitazione sull’Editor di schema per ulteriori informazioni.

### Come si abilita uno schema per l’utilizzo in [!DNL Real-Time Customer Profile]?

Gli schemi sono abilitati per l’utilizzo in [[!DNL Real-Time Customer Profile]](../profile/home.md) tramite l’aggiunta di un tag &quot;union&quot; all’interno del `meta:immutableTags` dello schema. Abilitazione di uno schema per l’utilizzo con [!DNL Profile] può essere eseguita utilizzando l’API o l’interfaccia utente di.

#### Abilitazione di uno schema esistente per [!DNL Profile] utilizzo dell’API

Effettua una richiesta PATCH per aggiornare lo schema e aggiungere `meta:immutableTags` come array contenente il valore &quot;union&quot;. Se l’aggiornamento ha esito positivo, la risposta mostrerà lo schema aggiornato che ora contiene il tag di unione.

Per ulteriori informazioni sull’utilizzo dell’API per abilitare uno schema da utilizzare in [!DNL Real-Time Customer Profile], vedere [sindacati](./api/unions.md) documento del [!DNL Schema Registry] guida per gli sviluppatori.

#### Abilitazione di uno schema esistente per [!DNL Profile] utilizzo dell’interfaccia utente

In entrata [!DNL Experience Platform], seleziona **[!UICONTROL Schemi]** nella barra di navigazione a sinistra, quindi seleziona il nome dello schema da abilitare dall’elenco degli schemi. Quindi, sul lato destro dell’editor sotto **[!UICONTROL Proprietà schema]**, seleziona **[!UICONTROL Profilo]** per attivarla.


Per ulteriori informazioni, consulta la sezione su [utilizzo in Real-Time Customer Profile](./tutorials/create-schema-ui.md#profile) nel [!UICONTROL Editor schema] esercitazione.

### Posso modificare direttamente uno schema di unione?

Gli schemi di unione sono di sola lettura e vengono generati automaticamente dal sistema. Non possono essere modificati direttamente. Gli schemi di unione vengono creati per una classe specifica quando un tag &quot;union&quot; viene aggiunto allo schema che implementa tale classe.

Per ulteriori informazioni sulle unioni in XDM, consulta la [sindacati](./api/unions.md) sezione nella sezione [!DNL Schema Registry] Guida API di.

### Come posso formattare il file di dati per acquisire i dati nel mio schema?

[!DNL Experience Platform] accetta file di dati in [!DNL Parquet] o in formato JSON. Il contenuto di questi file deve essere conforme allo schema a cui fa riferimento il set di dati. Per informazioni dettagliate sulle best practice per l’acquisizione dei file di dati, consulta [panoramica dell’acquisizione batch](../ingestion/home.md).

## Errori e risoluzione problemi

Di seguito è riportato un elenco di messaggi di errore che è possibile visualizzare quando si lavora con [!DNL Schema Registry] API.

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
>A seconda del tipo di risorsa da recuperare, questo errore può utilizzare uno dei seguenti `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Per ulteriori informazioni sulla creazione di percorsi di ricerca nell’API, consulta la sezione [contenitore](./api/getting-started.md#container) e [identificazione risorsa](api/getting-started.md#resource-identification) sezioni in [!DNL Schema Registry] guida per gli sviluppatori.

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
>A seconda della natura specifica dell’errore dello spazio dei nomi, questo errore può utilizzare uno dei seguenti `type` URI con dettagli di messaggio diversi:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Esempi dettagliati delle strutture di dati corrette per le risorse XDM sono disponibili nella guida dell’API del registro dello schema:

* [Creare una classe personalizzata](./api/classes.md#create)
* [Creare un gruppo di campi personalizzato](./api/field-groups.md#create)
* [Creare un tipo di dati personalizzato](./api/data-types.md#create)

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

GET le richieste in [!DNL Schema Registry] L&#39;API richiede un `Accept` affinché il sistema possa determinare come formattare la risposta. Questo errore si verifica quando è necessario `Accept` intestazione non valida o mancante.

A seconda dell&#39;endpoint che si sta utilizzando, il `detailed-message` proprietà indica che cosa è un `Accept` L’intestazione deve avere l’aspetto di una risposta corretta. Assicurati di aver inserito correttamente una `Accept` Intestazione compatibile con la richiesta API che stai tentando di effettuare prima di riprovare.

>[!NOTE]
>
>A seconda dell’endpoint utilizzato, questo errore può utilizzare uno dei seguenti `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Per gli elenchi di intestazioni compatibili di Accept per diverse richieste API, consulta le sezioni corrispondenti nella [Guida per gli sviluppatori del registro dello schema](./api/overview.md).

### [!DNL Real-Time Customer Profile] errori

I seguenti messaggi di errore sono associati alle operazioni necessarie per abilitare gli schemi per [!DNL Real-Time Customer Profile]. Consulta la [sindacati](./api/unions.md) sezione nella sezione [!DNL Schema Registry] Guida API di per ulteriori informazioni.

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

Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema per [!DNL Profile] e una delle sue proprietà contiene un descrittore di relazione senza un descrittore di identità di riferimento. Per risolvere l’errore, aggiungi un descrittore di identità di riferimento al campo dello schema in questione.

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

Per abilitare gli schemi che contengono descrittori di relazione da utilizzare in [!DNL Profile], lo spazio dei nomi del campo di origine e lo spazio dei nomi primario del campo di riferimento devono essere gli stessi. Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema che contiene uno spazio dei nomi senza corrispondenza per il relativo descrittore di identità di riferimento.

Assicurati che `xdm:namespace` il valore del campo di identità dello schema di riferimento corrisponde a quello del `xdm:identityNamespace` nel descrittore dell&#39;identità di riferimento del campo sorgente per risolvere questo problema.

Per un elenco dei codici dello spazio dei nomi di identità standard, consulta la sezione su [spazi dei nomi standard](../identity-service/namespaces.md) nella panoramica dello spazio dei nomi delle identità.

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

Prima di abilitare uno schema per il profilo, devi [creare un descrittore di identità primaria](./api/descriptors.md#create) per lo schema, oppure includi un campo identity map per agire sull’identità primaria.

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
