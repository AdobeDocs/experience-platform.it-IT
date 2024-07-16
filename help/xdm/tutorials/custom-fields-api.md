---
title: Definire i campi XDM nell’API del registro dello schema
description: Scopri come definire campi diversi durante la creazione di risorse Experience Data Model (XDM) personalizzate nell’API Schema Registry.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Definire i campi XDM nell’API del registro dello schema

Tutti i campi Experience Data Model (XDM) sono definiti utilizzando i vincoli standard [JSON Schema](https://json-schema.org/) che si applicano al relativo tipo di campo, con vincoli aggiuntivi per i nomi di campo applicati da Adobe Experience Platform. L’API Schema Registry consente di definire campi personalizzati negli schemi tramite l’utilizzo di formati e vincoli facoltativi. I tipi di campo XDM sono esposti dall&#39;attributo a livello di campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` è un valore generato dal sistema e pertanto non è necessario aggiungere questa proprietà al JSON per il campo quando si utilizza l&#39;API (tranne quando [si creano tipi di mappe personalizzati](#custom-maps)). Si consiglia di utilizzare i tipi di schema JSON (ad esempio `string` e `integer`) con i vincoli min/max appropriati come definito nella tabella seguente.

Questa guida descrive la formattazione appropriata per definire diversi tipi di campi, inclusi quelli con proprietà facoltative. Ulteriori informazioni sulle proprietà facoltative e sulle parole chiave specifiche per il tipo sono disponibili nella [documentazione sullo schema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Per iniziare, individua il tipo di campo desiderato e utilizza il codice di esempio fornito per generare la richiesta API per [la creazione di un gruppo di campi](../api/field-groups.md#create) o [la creazione di un tipo di dati](../api/data-types.md#create).

## [!UICONTROL Stringa] {#string}

I campi [!UICONTROL String] sono indicati da `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Facoltativamente, puoi vincolare i tipi di valori che possono essere immessi per la stringa attraverso le seguenti proprietà aggiuntive:

* `pattern`: un pattern regex da vincolare.
* `minLength`: lunghezza minima per la stringa.
* `maxLength`: lunghezza massima per la stringa.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field with added constraints.",
  "type": "string",
  "pattern": "^[A-Z]{2}$",
  "maxLength": 2
}
```

## [!UICONTROL URI] {#uri}

I campi [!UICONTROL URI] sono indicati da `type: string` con la proprietà `format` impostata su `uri`. Non sono accettate altre proprietà.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

I campi [!UICONTROL Enum] devono utilizzare `type: string`, con i valori enum forniti sotto una matrice `enum`:

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ]
}
```

Facoltativamente, è possibile fornire etichette rivolte al cliente per ogni valore sotto una proprietà `meta:enum`, con ogni etichetta digitata su un valore corrispondente in `enum`.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  }
}
```

>[!NOTE]
>
>Il valore `meta:enum` **not** dichiara un&#39;enumerazione o esegue da solo la convalida dei dati. Nella maggior parte dei casi, le stringhe fornite in `meta:enum` vengono fornite anche in `enum` per garantire che i dati siano vincolati. Tuttavia, in alcuni casi d&#39;uso `meta:enum` è fornito senza un array `enum` corrispondente. Per ulteriori informazioni, vedere il tutorial su [definizione dei valori suggeriti](../tutorials/suggested-values.md).

Facoltativamente, è possibile fornire una proprietà `default` per indicare il valore `enum` predefinito che verrà utilizzato dal campo se non viene fornito alcun valore.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels and a default value.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  },
  "default": "value1"
}
```

>[!IMPORTANT]
>
>Se non viene fornito alcun valore `default` e il campo enum è impostato su `required`, qualsiasi record senza un valore accettato per questo campo non supererà la convalida al momento dell&#39;acquisizione.

## [!UICONTROL Numero] {#number}

I campi numerici sono indicati da `type: number` e non hanno altre proprietà obbligatorie.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>I tipi `number` vengono utilizzati per qualsiasi tipo numerico, numeri interi o numeri a virgola mobile, mentre i tipi [`integer`](#integer) vengono utilizzati per i numeri integrali in modo specifico. Per ulteriori informazioni sui casi d&#39;uso per ciascun tipo, consulta la documentazione dello schema [JSON sui tipi numerici](https://json-schema.org/understanding-json-schema/reference/numeric.html).

## [!UICONTROL Numero intero] {#integer}

I campi [!UICONTROL Integer] sono indicati da `type: integer` e non contengono altri campi obbligatori.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Mentre i tipi `integer` fanno specifico riferimento a numeri integrali, i tipi [`number`](#number) vengono utilizzati per qualsiasi tipo numerico, ovvero numeri interi o numeri a virgola mobile. Per ulteriori informazioni sui casi d&#39;uso per ciascun tipo, consulta la documentazione dello schema [JSON sui tipi numerici](https://json-schema.org/understanding-json-schema/reference/numeric.html).

Facoltativamente, è possibile vincolare l&#39;intervallo del numero intero aggiungendo `minimum` e `maximum` proprietà alla definizione. Diversi altri tipi numerici supportati dall&#39;interfaccia utente di Schema Builder sono solo `integer` tipi con vincoli `minimum` e `maximum` specifici, ad esempio [[!UICONTROL Long]](#long), [[!UICONTROL Short]](#short) e [[!UICONTROL Byte]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL Lungo] {#long}

L&#39;equivalente di un campo [!UICONTROL Long] creato tramite l&#39;interfaccia utente di Schema Builder è un campo di tipo [`integer`](#integer) con valori `minimum` e `maximum` specifici (`-9007199254740992` e `9007199254740992`, rispettivamente).

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL Breve] {#short}

L&#39;equivalente di un campo [!UICONTROL Short] creato tramite l&#39;interfaccia utente di Schema Builder è un campo di tipo [`integer`](#integer) con valori `minimum` e `maximum` specifici (`-32768` e `32768`, rispettivamente).

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL Byte] {#byte}

L&#39;equivalente di un campo [!UICONTROL Byte] creato tramite l&#39;interfaccia utente di Schema Builder è un campo di tipo [`integer`](#integer) con valori `minimum` e `maximum` specifici (`-128` e `128`, rispettivamente).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL Booleano] {#boolean}

I campi [!UICONTROL Boolean] sono indicati da `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Facoltativamente, puoi fornire un valore `default` che il campo utilizzerà quando non viene fornito alcun valore esplicito durante l&#39;acquisizione.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field with a default value.",
  "type": "boolean",
  "default": false
}
```

>[!IMPORTANT]
>
>Se non viene fornito alcun valore `default` e il campo booleano è impostato su `required`, qualsiasi record in cui manca un valore accettato per questo campo non supererà la convalida al momento dell&#39;acquisizione.

## [!UICONTROL Data] {#date}

I campi [!UICONTROL Date] sono indicati da `type: string` e `format: date`. Facoltativamente, puoi anche fornire un array di `examples` da sfruttare nei casi in cui desideri visualizzare una stringa di data di esempio per gli utenti che immettono manualmente i dati.

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DataOra] {#date-time}

I campi [!UICONTROL DateTime] sono indicati da `type: string` e `format: date-time`. Facoltativamente, puoi anche fornire un array di `examples` da sfruttare nei casi in cui desideri visualizzare una stringa di esempio datetime per gli utenti che immettono manualmente i dati.

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL Array] {#array}

I campi [!UICONTROL Array] sono indicati da `type: array` e da un oggetto `items` che definisce lo schema degli elementi che l&#39;array accetterà.

Puoi definire gli elementi array utilizzando tipi primitivi, ad esempio una matrice di stringhe:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a primitive type.",
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

È inoltre possibile definire gli elementi array in base a un tipo di dati esistente facendo riferimento a `$id` del tipo di dati tramite una proprietà `$ref`. Di seguito è riportata una matrice di [!UICONTROL oggetti elemento di pagamento]:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a data type reference.",
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}
```

## [!UICONTROL Oggetto] {#object}

I campi [!UICONTROL Object] sono indicati da `type: object` e da un oggetto `properties` che definisce sottoproprietà per il campo schema.

Ogni sottocampo definito in `properties` può essere definito utilizzando qualsiasi elemento di base `type` o facendo riferimento a un tipo di dati esistente tramite una proprietà `$ref` che punta a `$id` del tipo di dati in questione:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field.",
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "$ref": "https://ns.adobe.com/xdm/common/measure"
    }
  }
}
```

È inoltre possibile definire l&#39;intero oggetto tramite facendo riferimento a un tipo di dati, a condizione che il tipo di dati in questione sia esso stesso definito come `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Mappa] {#map}

Un campo mappa è essenzialmente un campo di tipo [`object`](#object) con un set di chiavi non vincolato. Come gli oggetti, le mappe hanno un valore `type` di `object`, ma il loro `meta:xdmType` è impostato in modo esplicito su `map`.

Una mappa **non deve** definire proprietà. **deve** definire un singolo schema `additionalProperties` per descrivere il tipo di valori contenuti nella mappa (ogni mappa può contenere solo un singolo tipo di dati). Il valore `type` deve essere `string` o `integer`.

Ad esempio, un campo mappa con valori di tipo stringa sarebbe definito come segue:

```json
"sampleField": {
  "title": "Sample Map Field",
  "description": "An example map field.",
  "type": "object",
  "meta:xdmType": "map",
  "additionalProperties": {
    "type": "string"
  }
}
```

Per ulteriori dettagli sulla creazione di campi mappa personalizzati, consulta la sezione seguente.

### Creazione di tipi di mappe personalizzati {#custom-maps}

Per supportare in modo efficiente i dati di tipo mappa in XDM, agli oggetti può essere aggiunta un&#39;annotazione con `meta:xdmType` impostato su `map` per chiarire che un oggetto deve essere gestito come se il set di chiavi non fosse vincolato. I dati acquisiti nei campi mappa devono utilizzare chiavi stringa e solo valori stringa o interi (come determinato da `additionalProperties.type`).

XDM pone le seguenti restrizioni sull’utilizzo di questo hint di archiviazione:

* I tipi di mappa DEVONO essere di tipo `object`.
* I tipi di mappa NON DEVONO avere proprietà definite (in altre parole, definiscono oggetti &quot;vuoti&quot;).
* I tipi di mappa DEVONO includere un campo `additionalProperties.type` che descrive i valori che possono essere inseriti nella mappa, `string` o `integer`.

Assicurati di utilizzare campi di tipo mappa solo quando assolutamente necessario, in quanto presentano i seguenti svantaggi in termini di prestazioni:

* Il tempo di risposta di [Adobe Experience Platform Query Service](../../query-service/home.md) diminuisce da tre a dieci secondi per 100 milioni di record.
* Le mappe devono avere meno di 16 chiavi altrimenti si rischia un ulteriore degrado.

Anche l’interfaccia utente di Platform presenta limitazioni su come estrarre le chiavi dei campi di tipo mappa. Mentre i campi di tipo oggetto possono essere espansi, le mappe vengono visualizzate come un singolo campo.

## Passaggi successivi

Questa guida illustra come definire diversi tipi di campi nell’API. Per ulteriori informazioni sulla formattazione dei tipi di campo XDM, consulta la guida sui [vincoli per i tipi di campo XDM](../schema/field-constraints.md).
