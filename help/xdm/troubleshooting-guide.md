---
keywords: Experience Platform;argomenti popolari;XDM;sistema XDM;profilo individuale XDM;XDM ExperienceEvent;XDM ExperienceEvent;experienceEvent;experience eventExperience event;XDM Experience Event;XDM ExperienceEvent;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;schema;risoluzione dei problemi;FAQ;schema unione;PROFILE UNION;profilo unione;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Guida alla risoluzione dei problemi di sistema XDM
description: Trova le risposte alle domande frequenti su Experience Data Model (XDM), inclusi i passaggi per la risoluzione di errori API comuni.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 4743d844b33ff391ace0d2693b66ca4298994025
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di sistema XDM

Questo documento fornisce le risposte alle domande frequenti su [!DNL Experience Data Model] (XDM) e sul sistema XDM in Adobe Experience Platform, inclusa una guida alla risoluzione dei problemi per gli errori comuni. Per domande e risoluzione dei problemi relativi ad altri servizi di Platform, consulta la [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** è una specifica open-source che definisce schemi standardizzati per la gestione della customer experience. La metodologia su cui viene generato [!DNL Experience Platform], **XDM System**, rende operativi gli schemi [!DNL Experience Data Model] utilizzabili dai servizi [!DNL Platform]. Il **[!DNL Schema Registry]** fornisce un&#39;interfaccia utente e un&#39;API RESTful per accedere al **[!DNL Schema Library]** all&#39;interno di [!DNL Experience Platform]. Per ulteriori informazioni, consulta la [documentazione XDM](home.md) .

## Domande frequenti

Di seguito è riportato un elenco delle risposte alle domande frequenti sul sistema XDM e sull’utilizzo dell’ API [!DNL Schema Registry] .

### Come si aggiungono campi a uno schema?

È possibile aggiungere campi a uno schema utilizzando un gruppo di campi dello schema. Ogni gruppo di campi è compatibile con una o più classi, consentendo l&#39;utilizzo del gruppo di campi in qualsiasi schema che implementa una di queste classi compatibili. Mentre Adobe Experience Platform fornisce diversi gruppi di campi del settore con i propri campi predefiniti, è possibile aggiungere campi personalizzati a uno schema creando gruppi di campi personalizzati utilizzando l’API o l’interfaccia utente.

Per informazioni dettagliate sulla creazione di gruppi di campi nell&#39;API [!DNL Schema Registry], consulta la [guida all&#39;endpoint del gruppo di campi](api/field-groups.md#create). Se utilizzi l’interfaccia utente, consulta l’ [esercitazione Editor di schema](./tutorials/create-schema-ui.md).

### Quali sono gli usi migliori per i gruppi di campi e i tipi di dati?

[I ](./schema/composition.md#field-group) gruppi di campi sono componenti che definiscono uno o più campi in uno schema. I gruppi di campi impongono la modalità di visualizzazione dei campi nella gerarchia dello schema e quindi presentano la stessa struttura in ogni schema in cui sono inclusi. I gruppi di campi sono compatibili solo con classi specifiche, identificate dall’attributo `meta:intendedToExtend` corrispondente.

[I ](./schema/composition.md#data-type) tipi di dati possono inoltre fornire uno o più campi per uno schema. Tuttavia, a differenza dei gruppi di campi, i tipi di dati non sono vincolati a una particolare classe. Questo rende i tipi di dati un’opzione più flessibile per descrivere le strutture di dati comuni riutilizzabili tra più schemi con classi potenzialmente diverse.

### Qual è l&#39;ID univoco di uno schema?

Tutte le risorse [!DNL Schema Registry] (schemi, gruppi di campi, tipi di dati, classi) dispongono di un URI che funge da ID univoco a scopo di riferimento e ricerca. Quando si visualizza uno schema nell’API, questo si trova negli attributi di livello principale `$id` e `meta:altId` .

Per ulteriori informazioni, consulta la sezione [identificazione delle risorse](api/getting-started.md#resource-identification) nella guida API [!DNL Schema Registry].

### Quando uno schema inizia a impedire l&#39;interruzione delle modifiche?

È possibile apportare modifiche interrotte a uno schema purché non sia mai stato utilizzato nella creazione di un set di dati o sia abilitato per l’utilizzo in [[!DNL Real-time Customer Profile]](../profile/home.md). Una volta che uno schema è stato utilizzato nella creazione del set di dati o è abilitato per l’utilizzo con [!DNL Real-time Customer Profile], le regole di [Evoluzione schema](schema/composition.md#evolution) vengono applicate rigorosamente dal sistema.

### Qual è la dimensione massima di un tipo di campo lungo?

Un tipo di campo lungo è un numero intero con una dimensione massima di 53(+1) bit, che gli offre un intervallo potenziale compreso tra -9007199254740992 e 9007199254740992. Ciò è dovuto a una limitazione del modo in cui le implementazioni JavaScript di JSON rappresentano numeri interi lunghi.

Per ulteriori informazioni sui tipi di campo, consultare il documento relativo ai vincoli di tipo di campo [XDM](./schema/field-constraints.md).

### Come si definiscono le identità per lo schema?

In [!DNL Experience Platform], le identità vengono utilizzate per identificare un soggetto (in genere una persona singola) indipendentemente dalle origini dei dati che vengono interpretate. Sono definite negli schemi contrassegnando i campi chiave come &quot;Identità&quot;. I campi di identità comunemente utilizzati includono indirizzo e-mail, numero di telefono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), ID del sistema di gestione delle relazioni con i clienti e altri campi di ID univoci.

I campi possono essere contrassegnati come identità utilizzando l’API o l’interfaccia utente.

#### Definizione delle identità nell’API

Nell’API, le identità vengono stabilite creando descrittori di identità. I descrittori di identità segnalano che una particolare proprietà per uno schema è un identificatore univoco.

I descrittori di identità vengono creati da una richiesta POST all’endpoint /descriptors. In caso di esito positivo, riceverai uno stato HTTP 201 (Creato) e un oggetto di risposta contenente i dettagli del nuovo descrittore.

Per ulteriori dettagli sulla creazione di descrittori di identità nell&#39;API, consulta il documento sulla sezione [descrittori](api/descriptors.md) nella guida per gli sviluppatori [!DNL Schema Registry] .

#### Definizione delle identità nell’interfaccia utente

Con lo schema aperto nell’Editor di schema, seleziona il campo nella sezione **[!UICONTROL Struttura]** dell’editor che desideri contrassegnare come identità. In **[!UICONTROL Proprietà campo]** a destra, seleziona la casella di controllo **[!UICONTROL Identità]**.

Per ulteriori dettagli sulla gestione delle identità nell&#39;interfaccia utente, consulta la sezione relativa alla [definizione dei campi di identità](./tutorials/create-schema-ui.md#identity-field) nell&#39;esercitazione dell&#39;Editor di schema.

### Lo schema deve avere un&#39;identità primaria?

Le identità principali sono facoltative, in quanto gli schemi possono avere zero o uno di essi. Tuttavia, uno schema deve disporre di un&#39;identità primaria affinché lo schema sia abilitato per l&#39;utilizzo in [!DNL Real-time Customer Profile]. Per ulteriori informazioni, consulta la sezione [identity](./tutorials/create-schema-ui.md#identity-field) dell’esercitazione Editor di schema .

### Come si attiva uno schema da utilizzare in [!DNL Real-time Customer Profile]?

Gli schemi sono abilitati per l&#39;utilizzo in [[!DNL Real-time Customer Profile]](../profile/home.md) tramite l&#39;aggiunta di un tag &quot;union&quot; all&#39;interno dell&#39;attributo `meta:immutableTags` dello schema. L’abilitazione di uno schema da utilizzare con [!DNL Profile] può essere eseguita utilizzando l’API o l’interfaccia utente.

#### Abilitazione di uno schema esistente per [!DNL Profile] utilizzando l’API

Effettua una richiesta PATCH per aggiornare lo schema e aggiungere l’attributo `meta:immutableTags` come array contenente il valore &quot;union&quot;. Se l&#39;aggiornamento ha esito positivo, la risposta mostrerà lo schema aggiornato che ora contiene il tag di unione.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;API per abilitare uno schema da utilizzare in [!DNL Real-time Customer Profile], consulta il documento [sindacati](./api/unions.md) della guida per gli sviluppatori [!DNL Schema Registry].

#### Abilitazione di uno schema esistente per [!DNL Profile] utilizzando l&#39;interfaccia utente

In [!DNL Experience Platform], selezionare **[!UICONTROL Schemi]** nel menu di navigazione a sinistra, quindi selezionare il nome dello schema che si desidera abilitare dall’elenco degli schemi. Quindi, sul lato destro dell&#39;editor in **[!UICONTROL Proprietà schema]**, seleziona **[!UICONTROL Profilo]** per attivarlo.


Per ulteriori informazioni, consulta la sezione sull’ [utilizzo in Profilo cliente in tempo reale](./tutorials/create-schema-ui.md#profile) nell’ esercitazione [!UICONTROL Editor schema] .

### Posso modificare direttamente uno schema di unione?

Gli schemi dell’Unione sono di sola lettura e vengono generati automaticamente dal sistema. Non possono essere modificati direttamente. Gli schemi unione vengono creati per una classe specifica quando un tag &quot;union&quot; viene aggiunto allo schema che implementa tale classe.

Per ulteriori informazioni sui sindacati in XDM, consulta la sezione [sindacati](./api/unions.md) nella guida API [!DNL Schema Registry].

### Come posso formattare il file di dati per acquisire dati nel mio schema?

[!DNL Experience Platform] accetta file di dati in formato JSON  [!DNL Parquet] o . Il contenuto di questi file deve essere conforme allo schema a cui fa riferimento il set di dati. Per informazioni dettagliate sulle best practice per l’inserimento dei file di dati, consulta la [panoramica sull’acquisizione batch](../ingestion/home.md).

## Errori e risoluzione dei problemi

Di seguito è riportato un elenco di messaggi di errore che potresti riscontrare durante l’utilizzo dell’ API [!DNL Schema Registry] .

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

Questo errore viene visualizzato quando il sistema non è riuscito a trovare una risorsa specifica. La risorsa potrebbe essere stata eliminata o il percorso nella chiamata API non è valido. Assicurati di aver inserito un percorso valido per la chiamata API prima di riprovare. Puoi controllare di aver immesso l’ID corretto per la risorsa e che il percorso sia correttamente dotato di namespace con il contenitore appropriato (globale o tenant).

>[!NOTE]
>
>A seconda del tipo di risorsa da recuperare, questo errore può utilizzare uno dei seguenti URI `type`:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Per ulteriori informazioni sulla costruzione dei percorsi di ricerca nell’API, consulta le sezioni [container](./api/getting-started.md#container) e [identificazione delle risorse](api/getting-started.md#resource-identification) nella guida per gli sviluppatori [!DNL Schema Registry] .

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

Questo messaggio di errore viene visualizzato quando si tenta di creare una risorsa con campi con spazi dei nomi non appropriati o si aggiungono campi con spazi dei nomi non appropriati a una risorsa esistente.

Per evitare conflitti con altre risorse del settore e del fornitore, le risorse definite dall’organizzazione IMS devono assegnare un namespace ai propri campi nell’ID tenant. Quando si crea uno schema utilizzando gruppi di campi standard, anche tutti i campi personalizzati aggiunti all’interno della struttura di tali gruppi di campi devono avere un namespace nell’ID tenant.

>[!NOTE]
>
>A seconda della natura specifica dell’errore dello spazio dei nomi, questo errore può utilizzare uno dei seguenti URI `type` insieme a diversi dettagli del messaggio:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Esempi dettagliati di strutture di dati appropriate per le risorse XDM sono disponibili nella guida API del Registro di sistema dello schema:

* [Creare una classe personalizzata](./api/classes.md#create)
* [Creare un gruppo di campi personalizzato](./api/field-groups.md#create)
* [Creare un tipo di dati personalizzato](./api/data-types.md#create)

### Intestazione di accettazione non valida

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

Le richieste GET nell’ API [!DNL Schema Registry] richiedono un’intestazione `Accept` per consentire al sistema di determinare come formattare la risposta. Questo errore si verifica quando un&#39;intestazione `Accept` richiesta non è valida o mancante.

A seconda dell&#39;endpoint utilizzato, la proprietà `detailed-message` indica l&#39;aspetto di un&#39;intestazione `Accept` valida per una risposta corretta. Assicurati di aver immesso correttamente un&#39;intestazione `Accept` compatibile con la richiesta API che stai tentando di effettuare prima di riprovare.

>[!NOTE]
>
>A seconda dell’endpoint utilizzato, questo errore può utilizzare uno dei seguenti URI `type`:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Per gli elenchi delle intestazioni Accept compatibili per diverse richieste API, fai riferimento alle sezioni corrispondenti nella [Guida per gli sviluppatori del Registro di sistema dello schema](./api/overview.md).

### [!DNL Real-time Customer Profile] errori

I seguenti messaggi di errore sono associati alle operazioni di abilitazione degli schemi per [!DNL Real-time Customer Profile]. Per ulteriori informazioni, consulta la sezione [sindacati](./api/unions.md) nella guida [!DNL Schema Registry] API .

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

Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema per [!DNL Profile] e una delle relative proprietà contiene un descrittore di relazione senza un descrittore di identità di riferimento. Aggiungi un descrittore di identità di riferimento al campo dello schema in questione per risolvere questo errore.

#### I namespace del campo del descrittore di identità di riferimento e dello schema di destinazione devono corrispondere

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

Per abilitare gli schemi che contengono descrittori di relazione da utilizzare in [!DNL Profile], lo spazio dei nomi del campo di origine e dello spazio dei nomi primario del campo di destinazione deve essere lo stesso. Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema che contiene uno spazio dei nomi non corrispondente per il relativo descrittore di identità di riferimento. Per risolvere il problema, assicurati che il valore `xdm:namespace` del campo di identità dello schema di destinazione corrisponda a quello della proprietà `xdm:identityNamespace` nel descrittore di identità di riferimento del campo di origine.

Per un elenco dei codici standard dello spazio dei nomi delle identità, consulta la sezione relativa a [spazi dei nomi standard](../identity-service/namespaces.md) nella panoramica dello spazio dei nomi delle identità.

#### Lo schema deve includere una identityMap o un&#39;identità primaria

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

Prima di abilitare uno schema per Profilo, è necessario [creare un descrittore di identità principale](./api/descriptors.md#create) per lo schema oppure includere un campo di mappa di identità per agire all&#39;identità principale.