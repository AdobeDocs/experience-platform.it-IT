---
keywords: Experience Platform;argomenti popolari;XDM;sistema XDM;profilo individuale XDM;XDM ExperienceEvent;XDM ExperienceEvent;experienceEvent;experience eventExperience event;XDM Experience Event;XDM ExperienceEvent;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;schema;risoluzione dei problemi;FAQ;schema unione;PROFILE UNION;profilo unione;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Guida alla risoluzione dei problemi di sistema XDM
description: Trova le risposte alle domande frequenti su Experience Data Model (XDM), inclusi i passaggi per la risoluzione di errori API comuni.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 5ffc93c8715d1184b2a239c1d631b117a531e5c1
workflow-type: tm+mt
source-wordcount: '2060'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di sistema XDM

Questo documento fornisce le risposte alle domande frequenti sulle [!DNL Experience Data Model] (XDM) e Sistema XDM in Adobe Experience Platform, inclusa una guida alla risoluzione dei problemi relativi a errori comuni. Per domande e risoluzione dei problemi relativi ad altri servizi Platform, consulta la sezione [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** ?? una specifica open-source che definisce schemi standardizzati per la gestione della customer experience. La metodologia su cui [!DNL Experience Platform] ?? costruito, **Sistema XDM**, operazionalizza [!DNL Experience Data Model] schemi utilizzati da [!DNL Platform] servizi. La **[!DNL Schema Registry]** fornisce un???interfaccia utente e un???API RESTful per accedere al **[!DNL Schema Library]** entro [!DNL Experience Platform]. Consulta la sezione [Documentazione di XDM](home.md) per ulteriori informazioni.

## Domande frequenti

Di seguito ?? riportato un elenco delle risposte alle domande pi?? frequenti sul sistema XDM e sull&#39;utilizzo del [!DNL Schema Registry] API.

### Come si aggiungono campi a uno schema?

?? possibile aggiungere campi a uno schema utilizzando un gruppo di campi dello schema. Ogni gruppo di campi ?? compatibile con una o pi?? classi, consentendo l&#39;utilizzo del gruppo di campi in qualsiasi schema che implementa una di queste classi compatibili. Mentre Adobe Experience Platform fornisce diversi gruppi di campi del settore con i propri campi predefiniti, ?? possibile aggiungere campi personalizzati a uno schema creando gruppi di campi personalizzati utilizzando l???API o l???interfaccia utente.

Per i dettagli sulla creazione di gruppi di campi nel [!DNL Schema Registry] API, vedi [guida all???endpoint per gruppi di campi](api/field-groups.md#create). Se utilizzi l???interfaccia utente, consulta [Esercitazione sull???Editor di schema](./tutorials/create-schema-ui.md).

### Quali sono gli usi migliori per i gruppi di campi e i tipi di dati?

[Gruppi di campi](./schema/composition.md#field-group) sono componenti che definiscono uno o pi?? campi in uno schema. I gruppi di campi impongono la modalit?? di visualizzazione dei campi nella gerarchia dello schema e quindi presentano la stessa struttura in ogni schema in cui sono inclusi. I gruppi di campi sono compatibili solo con classi specifiche identificate dalle rispettive `meta:intendedToExtend` attributo.

[Tipi di dati](./schema/composition.md#data-type) pu?? inoltre fornire uno o pi?? campi per uno schema. Tuttavia, a differenza dei gruppi di campi, i tipi di dati non sono vincolati a una particolare classe. Questo rende i tipi di dati un???opzione pi?? flessibile per descrivere le strutture di dati comuni riutilizzabili tra pi?? schemi con classi potenzialmente diverse.

### Qual ?? l&#39;ID univoco di uno schema?

Tutto [!DNL Schema Registry] le risorse (schemi, gruppi di campi, tipi di dati, classi) dispongono di un URI che funge da ID univoco a scopo di riferimento e di ricerca. Quando si visualizza uno schema nell???API, questo si trova nel livello principale `$id` e `meta:altId` attributi.

Per ulteriori informazioni, consulta la sezione [identificazione delle risorse](api/getting-started.md#resource-identification) nella sezione [!DNL Schema Registry] Guida all???API.

### Quando uno schema inizia a impedire l&#39;interruzione delle modifiche?

?? possibile apportare modifiche allo schema purch?? non sia mai stato utilizzato nella creazione di un set di dati o sia abilitato per l???utilizzo in [[!DNL Real-time Customer Profile]](../profile/home.md). Una volta che uno schema ?? stato utilizzato nella creazione di un set di dati o abilitato per l???utilizzo con [!DNL Real-time Customer Profile], le norme [Evoluzione schema](schema/composition.md#evolution) essere rigorosamente applicato dal sistema.

### Qual ?? la dimensione massima di un tipo di campo lungo?

Un tipo di campo lungo ?? un numero intero con una dimensione massima di 53(+1) bit, che gli offre un intervallo potenziale compreso tra -9007199254740992 e 9007199254740992. Ci?? ?? dovuto a una limitazione del modo in cui le implementazioni JavaScript di JSON rappresentano numeri interi lunghi.

Per ulteriori informazioni sui tipi di campo, consulta il documento [Vincoli del tipo di campo XDM](./schema/field-constraints.md).

### Come si definiscono le identit?? per lo schema?

In [!DNL Experience Platform], le identit?? vengono utilizzate per identificare un soggetto (in genere una persona singola) indipendentemente dalle origini dei dati che vengono interpretate. Sono definite negli schemi contrassegnando i campi chiave come &quot;Identit??&quot;. I campi comunemente utilizzati per l&#39;identit?? includono indirizzo e-mail, numero di telefono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it), ID CRM e altri campi ID univoci.

I campi possono essere contrassegnati come identit?? utilizzando l???API o l???interfaccia utente.

#### Definizione delle identit?? nell???API

Nell???API, le identit?? vengono stabilite creando descrittori di identit??. I descrittori di identit?? segnalano che una particolare propriet?? per uno schema ?? un identificatore univoco.

I descrittori di identit?? vengono creati da una richiesta POST all???endpoint /descriptors. In caso di esito positivo, riceverai uno stato HTTP 201 (Creato) e un oggetto di risposta contenente i dettagli del nuovo descrittore.

Per ulteriori dettagli sulla creazione di descrittori di identit?? nell???API, consulta il documento su [descrittori](api/descriptors.md) nella sezione [!DNL Schema Registry] guida per sviluppatori.

#### Definizione delle identit?? nell???interfaccia utente

Con lo schema aperto nell???Editor di schema, selezionare il campo nel **[!UICONTROL Struttura]** della sezione dell???editor che desideri contrassegnare come identit??. Sotto **[!UICONTROL Propriet?? campo]** a destra, selezionare il **[!UICONTROL Identit??]** casella di controllo.

Per ulteriori dettagli sulla gestione delle identit?? nell&#39;interfaccia utente, consulta la sezione su [definizione dei campi di identit??](./tutorials/create-schema-ui.md#identity-field) nell???esercitazione Editor di schema.

### Lo schema deve avere un&#39;identit?? primaria?

Le identit?? principali sono facoltative, in quanto gli schemi possono avere zero o uno di essi. Tuttavia, uno schema deve disporre di un&#39;identit?? primaria affinch?? lo schema sia abilitato per l&#39;utilizzo in [!DNL Real-time Customer Profile]. Consulta la sezione [identit??](./tutorials/create-schema-ui.md#identity-field) per ulteriori informazioni, consulta la sezione dell???esercitazione Editor di schema .

### Come abilitare uno schema da utilizzare in [!DNL Real-time Customer Profile]?

Gli schemi sono abilitati per l&#39;uso in [[!DNL Real-time Customer Profile]](../profile/home.md) mediante l&#39;aggiunta di un tag &quot;union&quot; all&#39;interno del `meta:immutableTags` attributo dello schema. Abilitazione di uno schema da utilizzare con [!DNL Profile] pu?? essere eseguito utilizzando l???API o l???interfaccia utente.

#### Abilitazione di uno schema esistente per [!DNL Profile] utilizzo dell???API

Effettua una richiesta di PATCH per aggiornare lo schema e aggiungere il `meta:immutableTags` come array contenente il valore &quot;union&quot;. Se l&#39;aggiornamento ha esito positivo, la risposta mostrer?? lo schema aggiornato che ora contiene il tag di unione.

Per ulteriori informazioni sull???utilizzo dell???API per abilitare uno schema da utilizzare in [!DNL Real-time Customer Profile], vedi [sindacati](./api/unions.md) documento [!DNL Schema Registry] guida per sviluppatori.

#### Abilitazione di uno schema esistente per [!DNL Profile] utilizzo dell???interfaccia

In [!DNL Experience Platform], seleziona **[!UICONTROL Schemi]** nella navigazione a sinistra e selezionare il nome dello schema che si desidera abilitare dall???elenco degli schemi. Quindi, sul lato destro dell&#39;editor sotto **[!UICONTROL Propriet?? schema]**, seleziona **[!UICONTROL Profilo]** per attivarlo.


Per ulteriori informazioni, consulta la sezione su [utilizzo in Profilo cliente in tempo reale](./tutorials/create-schema-ui.md#profile) in [!UICONTROL Editor di schema] esercitazione.

### Posso modificare direttamente uno schema di unione?

Gli schemi dell???Unione sono di sola lettura e vengono generati automaticamente dal sistema. Non possono essere modificati direttamente. Gli schemi unione vengono creati per una classe specifica quando un tag &quot;union&quot; viene aggiunto allo schema che implementa tale classe.

Per ulteriori informazioni sui sindacati in XDM, consulta la sezione [sindacati](./api/unions.md) nella sezione [!DNL Schema Registry] Guida all???API.

### Come posso formattare il file di dati per acquisire dati nel mio schema?

[!DNL Experience Platform] accetta file di dati in [!DNL Parquet] o formato JSON. Il contenuto di questi file deve essere conforme allo schema a cui fa riferimento il set di dati. Per informazioni dettagliate sulle best practice per l???inserimento dei file di dati, consulta la [panoramica sull???acquisizione in batch](../ingestion/home.md).

## Errori e risoluzione dei problemi

Di seguito ?? riportato un elenco di messaggi di errore che si possono verificare durante l&#39;utilizzo di [!DNL Schema Registry] API.

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

Questo errore viene visualizzato quando il sistema non ?? riuscito a trovare una risorsa specifica. La risorsa potrebbe essere stata eliminata o il percorso nella chiamata API non ?? valido. Assicurati di aver inserito un percorso valido per la chiamata API prima di riprovare. Puoi controllare di aver immesso l???ID corretto per la risorsa e che il percorso sia correttamente dotato di namespace con il contenitore appropriato (globale o tenant).

>[!NOTE]
>
>A seconda del tipo di risorsa da recuperare, questo errore pu?? utilizzare uno dei seguenti `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Per ulteriori informazioni sulla costruzione dei percorsi di ricerca nell???API, consulta [container](./api/getting-started.md#container) e [identificazione delle risorse](api/getting-started.md#resource-identification) sezioni [!DNL Schema Registry] guida per sviluppatori.

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

Questo messaggio di errore viene visualizzato quando si tenta di creare una risorsa con un titolo gi?? utilizzato da un???altra risorsa. I titoli devono essere univoci per tutti i tipi di risorse. Ad esempio, se tenti di creare un gruppo di campi con un titolo gi?? utilizzato da uno schema, riceverai questo errore.

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

Per evitare conflitti con altre risorse del settore e del fornitore, le risorse definite dall???organizzazione IMS devono assegnare un namespace ai propri campi nell???ID tenant. Quando si crea uno schema utilizzando gruppi di campi standard, anche tutti i campi personalizzati aggiunti all???interno della struttura di tali gruppi di campi devono avere un namespace nell???ID tenant.

>[!NOTE]
>
>A seconda della natura specifica dell???errore dello spazio dei nomi, questo errore pu?? utilizzare uno dei seguenti `type` URI e diversi dettagli del messaggio:
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

GET nelle [!DNL Schema Registry] L???API richiede un `Accept` per consentire al sistema di determinare come formattare la risposta. Questo errore si verifica quando ?? richiesto `Accept` intestazione non valida o mancante.

A seconda dell???endpoint utilizzato, il `detailed-message` la propriet?? indica un valore valido `Accept` L&#39;intestazione deve essere simile alla risposta corretta. Assicurati di aver immesso correttamente un `Accept` intestazione compatibile con la richiesta API che si sta tentando di effettuare prima di riprovare.

>[!NOTE]
>
>A seconda dell???endpoint utilizzato, questo errore pu?? utilizzare uno dei seguenti `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Per gli elenchi delle intestazioni Accept compatibili per diverse richieste API, fai riferimento alle sezioni corrispondenti nella [Guida per gli sviluppatori del Registro di sistema dello schema](./api/overview.md).

### [!DNL Real-time Customer Profile] errori

I seguenti messaggi di errore sono associati alle operazioni necessarie per abilitare gli schemi per [!DNL Real-time Customer Profile]. Consulta la sezione [sindacati](./api/unions.md) nella sezione [!DNL Schema Registry] Guida all???API per ulteriori informazioni.

#### Deve essere presente un descrittore di identit?? di riferimento

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

Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema per [!DNL Profile] e una delle sue propriet?? contiene un descrittore di relazione senza un descrittore di identit?? di riferimento. Aggiungi un descrittore di identit?? di riferimento al campo dello schema in questione per risolvere questo errore.

#### I namespace del campo del descrittore di identit?? di riferimento e dello schema di destinazione devono corrispondere

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

Per abilitare gli schemi che contengono descrittori di relazione da utilizzare in [!DNL Profile], lo spazio dei nomi del campo di origine e dello spazio dei nomi primario del campo di destinazione deve essere lo stesso. Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema che contiene uno spazio dei nomi non corrispondente per il relativo descrittore di identit?? di riferimento. Assicurati che `xdm:namespace` il valore del campo di identit?? dello schema di destinazione corrisponde a quello del `xdm:identityNamespace` nel descrittore di identit?? di riferimento del campo di origine per risolvere il problema.

Per un elenco dei codici dei namespace di identit?? standard, consulta la sezione [namespace standard](../identity-service/namespaces.md) nella panoramica dello spazio dei nomi identit??.

#### Lo schema deve includere una identityMap o un&#39;identit?? primaria

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

Prima di abilitare uno schema per il profilo, devi prima [creare un descrittore di identit?? principale](./api/descriptors.md#create) per lo schema, oppure includere un campo mappa identit?? per agire all&#39;identit?? principale.

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

Tutti gli schemi abilitati per il profilo appartenenti alla stessa classe devono essere in grado di unirsi per creare lo schema di unione per quella classe. Questo errore viene visualizzato quando si tenta di aggiungere un campo a uno schema il cui percorso ?? condiviso da un altro schema abilitato per il profilo e il tipo di dati ?? diverso dall&#39;originale. Poich?? gli schemi sono entrambi abilitati per il profilo e contengono lo stesso percorso di campo, Profile tenter?? di unire questi due campi in un unico quando si crea lo schema di unione. Poich?? i diversi tipi di dati non possono essere uniti tra loro, si tratta di un conflitto di unione e non ?? consentito.

Per risolvere il problema, scegli un nome diverso per il campo o nidificalo sotto un oggetto con nomi univoci per evitare conflitti con altri schemi abilitati per il profilo nella stessa classe con campi simili.
