---
keywords: Experience Platform;home;argomenti popolari;XDM;sistema XDM;profilo individuale XDM;XDM ExperienceEvent;XDM ExperienceEvent;experienceEvent;experience event;XDM Experience Event;XDM ExperienceEvent;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;schema;risoluzione dei problemi;FAQ;schema unione;PROFILE UNION;profilo unione
solution: Experience Platform
title: Guida alla risoluzione dei problemi di sistema XDM
description: Questo documento fornisce le risposte alle domande più frequenti su Experience Data Model (XDM) e XDM System in Adobe Experience Platform, nonché una guida alla risoluzione dei problemi per gli errori comuni.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di sistema XDM

Questo documento fornisce le risposte alle domande più frequenti su [!DNL Experience Data Model] (XDM) e Sistema XDM in Adobe Experience Platform, nonché una guida alla risoluzione dei problemi per gli errori comuni. Per domande e risoluzione dei problemi relativi ad altri servizi di Platform, consulta la [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** è una specifica open-source che definisce schemi standardizzati per la gestione della customer experience. La metodologia su cui viene generato [!DNL Experience Platform], **XDM System**, rende operativi gli schemi [!DNL Experience Data Model] utilizzabili dai servizi [!DNL Platform]. Il **[!DNL Schema Registry]** fornisce un&#39;interfaccia utente e un&#39;API RESTful per accedere al **[!DNL Schema Library]** all&#39;interno di [!DNL Experience Platform]. Per ulteriori informazioni, consulta la [documentazione XDM](home.md) .

## Domande frequenti

Di seguito è riportato un elenco delle risposte alle domande frequenti sul sistema XDM e sull’utilizzo dell’ API [!DNL Schema Registry] .

### Come si aggiungono campi a uno schema?

È possibile aggiungere campi a uno schema utilizzando un mixin. Ogni mixin è compatibile con una o più classi, consentendo l&#39;utilizzo del mixin in qualsiasi schema che implementa una di queste classi compatibili. Mentre Adobe Experience Platform fornisce diversi mixin di settore con i propri campi predefiniti, puoi aggiungere i tuoi campi a uno schema creando nuovi mixin utilizzando l’API o l’interfaccia utente.

Per informazioni dettagliate sulla creazione di nuovi mixin nell&#39;API [!DNL Schema Registry], consulta la [guida all&#39;endpoint mixin](api/mixins.md#create). Se utilizzi l’interfaccia utente, consulta l’ [esercitazione Editor di schema](./tutorials/create-schema-ui.md).

### Quali sono gli usi migliori per i mixin rispetto ai tipi di dati?

[](./schema/composition.md#mixin) I mixin sono componenti che definiscono uno o più campi in uno schema. I mixin applicano la modalità di visualizzazione dei campi nella gerarchia dello schema e quindi presentano la stessa struttura in ogni schema in cui sono inclusi. I mixin sono compatibili solo con classi specifiche, come identificato dal loro attributo `meta:intendedToExtend` .

[I ](./schema/composition.md#data-type) tipi di dati possono inoltre fornire uno o più campi per uno schema. Tuttavia, a differenza dei mixin, i tipi di dati non sono vincolati a una particolare classe. Questo rende i tipi di dati un’opzione più flessibile per descrivere le strutture di dati comuni riutilizzabili tra più schemi con classi potenzialmente diverse.

### Qual è l&#39;ID univoco di uno schema?

Tutte le risorse [!DNL Schema Registry] (schemi, mixin, tipi di dati, classi) hanno un URI che agisce come ID univoco a scopo di riferimento e ricerca. Quando si visualizza uno schema nell’API, questo si trova negli attributi di livello principale `$id` e `meta:altId` .

Per ulteriori informazioni, consulta la sezione [identificazione delle risorse](api/getting-started.md#resource-identification) nella guida per gli sviluppatori API [!DNL Schema Registry].

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

Con lo schema aperto nell’Editor schema, seleziona il campo nella sezione **[!UICONTROL Structure]** dell’editor che desideri contrassegnare come identità. In **[!UICONTROL Field Properties]** a destra, seleziona la casella di controllo **[!UICONTROL Identity]**.

Per ulteriori dettagli sulla gestione delle identità nell&#39;interfaccia utente, consulta la sezione relativa alla [definizione dei campi di identità](./tutorials/create-schema-ui.md#identity-field) nell&#39;esercitazione dell&#39;Editor di schema.

### Lo schema deve avere un&#39;identità primaria?

Le identità principali sono facoltative, in quanto gli schemi possono avere 0 o 1 di essi. Tuttavia, uno schema deve disporre di un&#39;identità primaria affinché lo schema sia abilitato per l&#39;utilizzo in [!DNL Real-time Customer Profile]. Per ulteriori informazioni, consulta la sezione [identity](./tutorials/create-schema-ui.md#identity-field) dell’esercitazione Editor di schema .

### Come si attiva uno schema da utilizzare in [!DNL Real-time Customer Profile]?

Gli schemi sono abilitati per l&#39;utilizzo in [[!DNL Real-time Customer Profile]](../profile/home.md) tramite l&#39;aggiunta di un tag &quot;union&quot;, situato nell&#39;attributo `meta:immutableTags` dello schema. L’abilitazione di uno schema da utilizzare con [!DNL Profile] può essere eseguita utilizzando l’API o l’interfaccia utente.

#### Abilitazione di uno schema esistente per [!DNL Profile] utilizzando l’API

Effettua una richiesta PATCH per aggiornare lo schema e aggiungere l’attributo `meta:immutableTags` come array contenente il valore &quot;union&quot;. Se l&#39;aggiornamento ha esito positivo, la risposta mostrerà lo schema aggiornato che ora contiene il tag di unione.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;API per abilitare uno schema da utilizzare in [!DNL Real-time Customer Profile], consulta il documento [sindacati](./api/unions.md) della guida per gli sviluppatori [!DNL Schema Registry].

#### Abilitazione di uno schema esistente per [!DNL Profile] utilizzando l&#39;interfaccia utente

In [!DNL Experience Platform], seleziona **[!UICONTROL Schemas]** nel menu di navigazione a sinistra e seleziona il nome dello schema da abilitare dall’elenco degli schemi. Quindi, sul lato destro dell’editor in **[!UICONTROL Schema Properties]**, seleziona **[!UICONTROL Profile]** per attivarlo.


Per ulteriori informazioni, consulta la sezione sull’ [utilizzo in Profilo cliente in tempo reale](./tutorials/create-schema-ui.md#profile) nell’ esercitazione [!UICONTROL Schema Editor] .

### Posso modificare direttamente uno schema di unione?

Gli schemi dell’Unione sono di sola lettura e vengono generati automaticamente dal sistema. Non possono essere modificati direttamente. Gli schemi unione vengono creati per una classe specifica quando un tag &quot;union&quot; viene aggiunto allo schema che implementa tale classe.

Per ulteriori informazioni sui sindacati in XDM, consulta la sezione [sindacati](./api/unions.md) nella guida per gli sviluppatori API [!DNL Schema Registry].

### Come posso formattare il file di dati per acquisire dati nel mio schema?

[!DNL Experience Platform] accetta file di dati in formato JSON  [!DNL Parquet] o . Il contenuto di questi file deve essere conforme allo schema a cui fa riferimento il set di dati. Per informazioni dettagliate sulle best practice per l’inserimento dei file di dati, consulta la [panoramica sull’acquisizione batch](../ingestion/home.md).

## Errori e risoluzione dei problemi

Di seguito è riportato un elenco di messaggi di errore che potresti riscontrare durante l’utilizzo dell’ API [!DNL Schema Registry] .

### Oggetto non trovato

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

Questo errore viene visualizzato quando il sistema non è riuscito a trovare una risorsa specifica. La risorsa potrebbe essere stata eliminata o il percorso nella chiamata API non è valido. Assicurati di aver inserito un percorso valido per la chiamata API prima di riprovare. Puoi controllare di aver immesso l’ID corretto per la risorsa e che il percorso sia correttamente dotato di namespace con il contenitore appropriato (globale o tenant).

Per ulteriori informazioni sulla costruzione dei percorsi di ricerca nell’API, consulta le sezioni [container](./api/getting-started.md#container) e [identificazione delle risorse](api/getting-started.md#resource-identification) nella guida per gli sviluppatori [!DNL Schema Registry] .

### Il titolo deve essere univoco

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "Title must be unique. An object 
      https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d 
      already exists with the same title."
}
```

Questo messaggio di errore viene visualizzato quando si tenta di creare una risorsa con un titolo già utilizzato da un’altra risorsa. I titoli devono essere univoci per tutti i tipi di risorse. Ad esempio, se tenti di creare un mixin con un titolo già utilizzato da uno schema, riceverai questo errore.

### I campi personalizzati devono utilizzare un campo di primo livello

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

Questo messaggio di errore viene visualizzato quando si tenta di creare un nuovo mixin con campi con spazi dei nomi non appropriati. Per evitare conflitti con altre risorse del settore e del fornitore, i mixin definiti dall’organizzazione IMS devono assegnare ai rispettivi campi uno spazio dei nomi `TENANT_ID`. Esempi dettagliati di strutture dati appropriate per i mixin sono disponibili nella [guida endpoint mixins](./api/mixins.md#create).


### [!DNL Real-time Customer Profile] errori

I seguenti messaggi di errore sono associati alle operazioni di abilitazione degli schemi per [!DNL Real-time Customer Profile]. Per ulteriori informazioni, consulta la sezione [sindacati](./api/unions.md) nella guida per gli sviluppatori API [!DNL Schema Registry] .

#### Per abilitare i set di dati di profilo, lo schema deve essere valido

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Questo messaggio di errore viene visualizzato quando si tenta di abilitare un set di dati di profilo per uno schema non abilitato per [!DNL Real-time Customer Profile]. Assicurati che lo schema contenga un tag di unione prima di abilitare il set di dati.

#### Deve essere presente un descrittore di identità di riferimento

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For a schema to be able to participate in union, if any of its 
      property is associated with a xdm:descriptorOneToOne descriptor, there must 
      be a xdm:descriptorReferenceIdentity descriptor for that property"
}
```

Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema per [!DNL Profile] e una delle relative proprietà contiene un descrittore di relazione senza un descrittore di identità di riferimento. Aggiungi un descrittore di identità di riferimento al campo dello schema in questione per risolvere questo errore.

#### I namespace del campo del descrittore di identità di riferimento e dello schema di destinazione devono corrispondere

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "If both schemas from an already defined xdm:descriptorOneToOne 
      descriptor are promoted to union, and if there is a primary identity on one of 
      the schemas from the xdm:descriptorOneToOne descriptor, the 
      xdm:identityNamespace of the sourceSchema's descriptorReferenceIdentity and the 
      xdm:namespace field of the xdm:descriptorIdentity for the destinationSchema must 
      match"
}
```

Per abilitare gli schemi che contengono descrittori di relazione da utilizzare in [!DNL Profile], lo spazio dei nomi del campo di origine e dello spazio dei nomi primario del campo di destinazione deve essere lo stesso. Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema che contiene uno spazio dei nomi non corrispondente per il relativo descrittore di identità di riferimento. Per risolvere il problema, assicurati che il valore `xdm:namespace` del campo di identità dello schema di destinazione corrisponda a quello della proprietà `xdm:identityNamespace` nel descrittore di identità di riferimento del campo di origine.

Per un elenco dei codici dello spazio dei nomi di identità supportati, consulta la sezione relativa a [spazi dei nomi standard](../identity-service/namespaces.md) nella panoramica dello spazio dei nomi di identità.

### Accetta errori di intestazione

La maggior parte delle richieste GET nell’ API [!DNL Schema Registry] richiede un’intestazione Accept per consentire al sistema di determinare come formattare la risposta. Di seguito è riportato un elenco di errori comuni associati all&#39;intestazione Accept. Per gli elenchi delle intestazioni Accept compatibili per diverse richieste API, fai riferimento alle sezioni corrispondenti nella [Guida per gli sviluppatori del Registro di sistema dello schema](api/getting-started.md).

#### Il parametro di intestazione Accept è obbligatorio

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39;intestazione Accept da una richiesta API. Assicurati che sia inclusa un&#39;intestazione Accept prima di riprovare.

#### Supporto di accettazione sconosciuto

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Questo messaggio di errore viene visualizzato quando un&#39;intestazione Accept non è valida. Assicurati di aver immesso correttamente un’intestazione Accept compatibile con la richiesta API che stai tentando di effettuare prima di riprovare.

#### Formato di accettazione sconosciuto disponibile

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Questo messaggio di errore viene visualizzato quando l&#39;intestazione Accept è stata fornita in modo errato quando si cerca un descrittore. Assicurati di aver inserito correttamente una delle [intestazioni Accept supportate per i descrittori](./api/descriptors.md) prima di riprovare.

#### La versione deve essere fornita nell&#39;intestazione Accept

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Questo messaggio di errore viene visualizzato quando non è stato incluso un numero di versione nell&#39;intestazione Accept. Alcuni elementi, come gli schemi, richiedono che venga specificata una versione quando si cercano singole istanze. Un&#39;intestazione Accept contenente un numero di versione avrà un aspetto simile al seguente:

```plaintext
application/vnd.adobe.xed+json; version=1
```

Per un elenco delle intestazioni Accept supportate, consulta la sezione [Accept header](api/getting-started.md#accept) nella guida per sviluppatori [!DNL Schema Registry].

#### La versione non deve essere fornita nell&#39;intestazione Accept

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Se tenti di includere una versione nell’intestazione Accept durante l’inserimento di risorse (GET), riceverai questo errore. Le versioni sono necessarie solo quando si tenta una richiesta di ricerca su una singola risorsa. Rimuovi la versione dall&#39;intestazione Accept per risolvere l&#39;errore.
