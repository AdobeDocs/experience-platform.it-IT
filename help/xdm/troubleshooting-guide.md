---
keywords: ' Experience Platform;home;argomenti più comuni;XDM;XDM, sistema;XDM, profilo individuale;XDM Experience Event;XDM Experience Event;XDM Experience Event;XDM Experience Event;XDM Experience Event;XDM Experience Data Model;Experience Data Model;Data Model;Data Model;schema;risoluzione dei problemi;FAQ;faq;Union Schema;UNION PROFILE;Union profile'
solution: Experience Platform
title: Guida alla risoluzione dei problemi del sistema XDM (Experience Data Model)
description: Questo documento contiene le risposte alle domande frequenti sul sistema Experience Data Model (XDM) e una guida alla risoluzione dei problemi per individuare gli errori più comuni.
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 0%

---


# [!DNL Experience Data Model] (XDM) Guida alla risoluzione dei problemi di sistema

Questo documento contiene le risposte alle domande frequenti sul sistema [!DNL Experience Data Model] (XDM) e una guida alla risoluzione dei problemi per individuare gli errori più comuni. Per le domande e la risoluzione dei problemi relativi ad altri servizi Adobe Experience Platform, consultare la [Guida alla risoluzione dei problemi  Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** è una specifica open-source che definisce schemi standardizzati per la gestione dell&#39;esperienza cliente. La metodologia su cui è costruito [!DNL Experience Platform], **XDM System**, rende operativi gli schemi [!DNL Experience Data Model] per l&#39;utilizzo da parte dei servizi [!DNL Platform]. **[!DNL Schema Registry]** fornisce un&#39;interfaccia utente e un&#39;API RESTful per accedere alla **[!DNL Schema Library]** all&#39;interno di [!DNL Experience Platform]. Per ulteriori informazioni, consultare la [documentazione XDM](home.md).

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande frequenti sul sistema XDM e sull&#39;utilizzo dell&#39;API [!DNL Schema Registry].

### Come si aggiungono i campi a uno schema?

È possibile aggiungere campi a uno schema utilizzando un mixin. Ciascun mixin è compatibile con una o più classi, consentendo l&#39;utilizzo del mixin in qualsiasi schema che implementa una di queste classi compatibili. Adobe Experience Platform fornisce diversi mixin di settore con campi predefiniti, ma è possibile aggiungere campi personalizzati a uno schema creando nuovi mixin utilizzando l&#39;API o l&#39;interfaccia utente.

Per informazioni dettagliate sulla creazione di nuovi mixin nell&#39;API [!DNL Schema Registry], consultate la guida [agli endpoint del mixin](api/mixins.md#create). Se si utilizza l&#39;interfaccia utente, vedere l&#39;esercitazione [Editor di schema](./tutorials/create-schema-ui.md).

### Quali sono gli usi migliori per i mixin rispetto ai tipi di dati?

[I ](./schema/composition.md#mixin) diversi componenti sono componenti che definiscono uno o più campi in uno schema. I mixin applicano la modalità di visualizzazione dei campi nella gerarchia dello schema, mostrando quindi la stessa struttura in ogni schema in cui sono inclusi. I mixin sono compatibili solo con classi specifiche, identificate dall&#39;attributo `meta:intendedToExtend`.

[I ](./schema/composition.md#data-type) tipi di dati possono anche fornire uno o più campi per uno schema. Tuttavia, a differenza dei mixin, i tipi di dati non sono vincolati a una determinata classe. Questo rende i tipi di dati un&#39;opzione più flessibile per descrivere le strutture di dati comuni riutilizzabili tra più schemi con classi potenzialmente diverse.

### Qual è l&#39;ID univoco per uno schema?

Tutte le risorse [!DNL Schema Registry] (schemi, mixin, tipi di dati, classi) dispongono di un URI che funge da ID univoco a scopo di riferimento e di ricerca. Quando si visualizza uno schema nell&#39;API, questo si trova negli attributi di livello principale `$id` e `meta:altId`.

Per ulteriori informazioni, vedete la sezione [identificazione delle risorse](api/getting-started.md#resource-identification) nella guida per gli sviluppatori di [!DNL Schema Registry] API.

### Quando inizia uno schema per impedire l&#39;interruzione delle modifiche?

È possibile apportare modifiche allo schema a condizione che non sia mai stato utilizzato nella creazione di un dataset o sia abilitato per l&#39;uso in [[!DNL Real-time Customer Profile]](../profile/home.md). Una volta che uno schema è stato utilizzato nella creazione di set di dati o abilitato per l&#39;uso con [!DNL Real-time Customer Profile], le regole di [Evoluzione schema](schema/composition.md#evolution) vengono applicate in modo rigoroso dal sistema.

### Qual è la dimensione massima di un tipo di campo lungo?

Un tipo di campo lungo è un numero intero con una dimensione massima di 53 (+1) bit, il cui intervallo potrebbe essere compreso tra -9007199254740992 e 9007199254740992. Ciò è dovuto a una limitazione del modo in cui le implementazioni JavaScript di JSON rappresentano numeri interi lunghi.

Per ulteriori informazioni sui tipi di campo, consultare il documento relativo ai vincoli dei tipi di campo [XDM](./schema/field-constraints.md).

### Come si definiscono le identità per lo schema?

In [!DNL Experience Platform], le identità vengono utilizzate per identificare un oggetto (in genere una singola persona) indipendentemente dalle origini dei dati che vengono interpretate. Sono definiti negli schemi contrassegnando i campi chiave come &quot;Identità&quot;. I campi utilizzati comunemente per l&#39;identità includono indirizzo e-mail, numero di telefono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), ID CRM e altri campi ID univoci.

I campi possono essere contrassegnati come identità tramite l&#39;API o l&#39;interfaccia utente.

#### Definizione delle identità nell&#39;API

Nell&#39;API, le identità vengono stabilite creando descrittori di identità. I descrittori di identità indicano che una particolare proprietà per uno schema è un identificatore univoco.

I descrittori di identità vengono creati da una richiesta di POST all&#39;endpoint /descriptors. In caso di esito positivo, riceverete uno stato HTTP 201 (Creato) e un oggetto di risposta contenente i dettagli del nuovo descrittore.

Per ulteriori dettagli sulla creazione di descrittori di identità nell&#39;API, consultate il documento nella sezione [descrittori](api/descriptors.md) nella guida per gli sviluppatori [!DNL Schema Registry].

#### Definizione delle identità nell’interfaccia utente

Con lo schema aperto nell&#39;Editor schema, selezionare il campo nella sezione **[!UICONTROL Structure]** dell&#39;editor che si desidera contrassegnare come identità. In **[!UICONTROL Field Properties]** a destra, selezionare la casella di controllo **[!UICONTROL Identity]**.

Per ulteriori dettagli sulla gestione delle identità nell&#39;interfaccia utente, vedere la sezione relativa alla [definizione dei campi identità](./tutorials/create-schema-ui.md#identity-field) nell&#39;esercitazione dell&#39;Editor di schema.

### Lo schema deve avere un&#39;identità primaria?

Le identità principali sono facoltative, poiché gli schemi possono avere 0 o 1 di essi. Tuttavia, uno schema deve avere un&#39;identità primaria affinché lo schema sia abilitato per l&#39;uso in [!DNL Real-time Customer Profile]. Per ulteriori informazioni, vedere la sezione [identity](./tutorials/create-schema-ui.md#identity-field) dell&#39;esercitazione Editor di schema.

### Come si abilita uno schema da utilizzare in [!DNL Real-time Customer Profile]?

Gli schemi sono abilitati per l&#39;utilizzo in [[!DNL Real-time Customer Profile]](../profile/home.md) tramite l&#39;aggiunta di un tag &quot;unione&quot;, situato nell&#39;attributo `meta:immutableTags` dello schema. Per abilitare uno schema da utilizzare con [!DNL Profile] è possibile utilizzare l&#39;API o l&#39;interfaccia utente.

#### Abilitazione di uno schema esistente per [!DNL Profile] mediante l&#39;API

Eseguite una richiesta di PATCH per aggiornare lo schema e aggiungere l&#39;attributo `meta:immutableTags` come array contenente il valore &quot;union&quot;. Se l&#39;aggiornamento ha esito positivo, la risposta mostrerà lo schema aggiornato che ora contiene il tag unione.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;API per abilitare uno schema da utilizzare in [!DNL Real-time Customer Profile], consultare il documento [sindacati](./api/unions.md) della guida per gli sviluppatori [!DNL Schema Registry].

#### Abilitazione di uno schema esistente per [!DNL Profile] utilizzando l&#39;interfaccia utente

In [!DNL Experience Platform], selezionare **[!UICONTROL Schemas]** nella navigazione a sinistra, quindi selezionare il nome dello schema che si desidera abilitare dall&#39;elenco degli schemi. Quindi, sul lato destro dell&#39;editor in **[!UICONTROL Schema Properties]**, selezionare **[!UICONTROL Profile]** per attivarlo.


Per ulteriori informazioni, vedere la sezione sull&#39; [utilizzo in Real-time Customer Profile](./tutorials/create-schema-ui.md#profile) nell&#39; [!UICONTROL Schema Editor] esercitazione.

### Posso modificare direttamente uno schema di unione?

Gli schemi unione sono di sola lettura e vengono generati automaticamente dal sistema. Non possono essere modificati direttamente. Gli schemi unione vengono creati per una classe specifica quando viene aggiunto un tag &quot;unione&quot; allo schema che implementa tale classe.

Per ulteriori informazioni sui sindacati in XDM, consultate la sezione [sindacati](./api/unions.md) nella guida per gli sviluppatori di [!DNL Schema Registry] API.

### Come si formatta il file di dati per inserire i dati nello schema?

[!DNL Experience Platform] accetta file di dati in formato JSON  [!DNL Parquet] o . Il contenuto di questi file deve essere conforme allo schema a cui fa riferimento il dataset. Per informazioni dettagliate sulle procedure ottimali per l&#39;assimilazione dei file di dati, vedere la [panoramica sull&#39;inserimento dei batch](../ingestion/home.md).

## Errori e risoluzione dei problemi

Di seguito è riportato un elenco di messaggi di errore che potrebbero verificarsi durante l&#39;utilizzo dell&#39;API [!DNL Schema Registry].

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

Questo errore viene visualizzato quando il sistema non è in grado di trovare una risorsa specifica. La risorsa potrebbe essere stata eliminata oppure il percorso nella chiamata API non è valido. Prima di riprovare, verifica di aver immesso un percorso valido per la chiamata API. È possibile verificare di aver immesso l&#39;ID corretto per la risorsa e che il percorso sia correttamente associato al contenitore appropriato (globale o tenant).

Per ulteriori informazioni sulla creazione di percorsi di ricerca nell&#39;API, vedere le sezioni [container](./api/getting-started.md#container) e [identificazione delle risorse](api/getting-started.md#resource-identification) nella guida per gli sviluppatori [!DNL Schema Registry].

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

Questo messaggio di errore viene visualizzato quando tentate di creare una risorsa con un titolo già utilizzato da un’altra risorsa. I titoli devono essere univoci per tutti i tipi di risorse. Ad esempio, se si tenta di creare un mixin con un titolo già utilizzato da uno schema, si verificherà questo errore.

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

Questo messaggio di errore viene visualizzato quando tentate di creare un nuovo mixin con campi con nome non corretto. I mixin definiti dall&#39;organizzazione IMS devono assegnare ai campi uno spazio dei nomi `TENANT_ID` per evitare conflitti con altre risorse del settore e del fornitore. Esempi dettagliati di strutture di dati adeguate per i mixin si trovano nella [guida endpoint mixins](./api/mixins.md#create).


### [!DNL Real-time Customer Profile] error

I messaggi di errore riportati di seguito sono associati alle operazioni di abilitazione degli schemi per [!DNL Real-time Customer Profile]. Per ulteriori informazioni, vedi la sezione [sindacati](./api/unions.md) nella [!DNL Schema Registry] Guida per gli sviluppatori di API.

#### Per abilitare i set di dati del profilo, lo schema deve essere valido

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Questo messaggio di errore viene visualizzato quando si tenta di abilitare un dataset di profilo per uno schema che non è stato abilitato per [!DNL Real-time Customer Profile]. Prima di abilitare il dataset, assicurarsi che lo schema contenga un tag di unione.

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

Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema per [!DNL Profile] e una delle sue proprietà contiene un descrittore di relazione senza un descrittore di identità di riferimento. Aggiungete un descrittore di identità di riferimento al campo dello schema in questione per risolvere l&#39;errore.

#### Gli spazi dei nomi del campo descrittore dell&#39;identità di riferimento e dello schema di destinazione devono corrispondere

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

Per abilitare gli schemi che contengono descrittori di relazione da utilizzare in [!DNL Profile], lo spazio dei nomi del campo di origine e dello spazio dei nomi primario del campo di destinazione deve essere lo stesso. Questo messaggio di errore viene visualizzato quando si tenta di abilitare uno schema che contiene uno spazio nomi non corrispondente per il relativo descrittore di identità di riferimento. Verificare che il valore `xdm:namespace` del campo identità dello schema di destinazione corrisponda a quello della proprietà `xdm:identityNamespace` nel descrittore dell&#39;identità di riferimento del campo di origine per risolvere il problema.

Per un elenco dei codici dei nomi identità supportati, consultate la sezione relativa agli [spazi dei nomi standard](../identity-service/namespaces.md) nella panoramica dello spazio dei nomi identità.

### Accetta errori di intestazione

La maggior parte delle richieste di GET nell&#39;API [!DNL Schema Registry] richiede un&#39;intestazione Accetto per consentire al sistema di determinare come formattare la risposta. Di seguito è riportato un elenco di errori comuni associati all&#39;intestazione Accetto. Per gli elenchi delle intestazioni Accetta compatibili per diverse richieste API, fare riferimento alle sezioni corrispondenti nella [Guida per gli sviluppatori del Registro di sistema dello schema](api/getting-started.md).

#### Il parametro di intestazione Accetta è obbligatorio

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Questo messaggio di errore viene visualizzato quando manca un&#39;intestazione Accetto da una richiesta API. Prima di riprovare, verificate che sia inclusa un&#39;intestazione Accetto.

#### Supporto di accettazione sconosciuto

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Questo messaggio di errore viene visualizzato quando un&#39;intestazione Accetto non è valida. Assicuratevi di aver immesso correttamente un&#39;intestazione Accetto compatibile con la richiesta API che state tentando di eseguire prima di riprovare.

#### Formato Accetta sconosciuto disponibile

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Questo messaggio di errore viene visualizzato quando l&#39;intestazione Accetto è stata fornita in modo non corretto durante la ricerca di un descrittore. Prima di riprovare, assicurarsi di aver immesso correttamente una delle [intestazioni di accettazione supportate per i descrittori](./api/descriptors.md).

#### La versione deve essere fornita nell&#39;intestazione Accetto

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Questo messaggio di errore viene visualizzato quando un numero di versione non è stato incluso nell&#39;intestazione Accetto. Alcuni elementi come gli schemi richiedono che venga specificata una versione quando si ricercano singole istanze. Un&#39;intestazione Accetta contenente un numero di versione avrà un aspetto simile al seguente:

```plaintext
application/vnd.adobe.xed+json; version=1
```

Per un elenco delle intestazioni Accetto supportate, consultate la sezione [Accetta intestazione](api/getting-started.md#accept) nella guida per gli sviluppatori [!DNL Schema Registry].

#### La versione non deve essere specificata nell&#39;intestazione Accetto

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Se tenti di includere una versione nell’intestazione Accetto durante l’elencazione delle risorse (GET), riceverai l’errore. Le versioni sono necessarie solo quando si tenta di eseguire una richiesta di ricerca su una singola risorsa. Rimuovere la versione dall&#39;intestazione Accetto per risolvere l&#39;errore.