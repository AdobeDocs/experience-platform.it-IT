---
title: Definire i campi XDM nell’API del Registro di sistema dello schema
description: Scopri come definire campi diversi durante la creazione di risorse personalizzate Experience Data Model (XDM) nell’API del Registro di sistema dello schema.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Definire i campi XDM nell’API del Registro di sistema dello schema

Tutti i campi Experience Data Model (XDM) sono definiti utilizzando lo standard [Schema JSON](https://json-schema.org/) vincoli applicabili al tipo di campo, con vincoli aggiuntivi per i nomi di campo applicati da Adobe Experience Platform. L’API del Registro di sistema dello schema consente di definire campi personalizzati negli schemi mediante l’uso di formati e vincoli facoltativi. I tipi di campo XDM sono esposti dall’attributo a livello di campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` è un valore generato dal sistema e pertanto non è necessario aggiungere questa proprietà al JSON per il campo quando si utilizza l’API (tranne quando [creazione di tipi di mappa personalizzati](#custom-maps)). Si consiglia di utilizzare i tipi di schema JSON (ad esempio `string` e `integer`) con i vincoli minimi/massimi appropriati, come definito nella tabella seguente.

Questa guida delinea la formattazione appropriata per definire diversi tipi di campi, compresi quelli con proprietà facoltative. Ulteriori informazioni sulle proprietà facoltative e sulle parole chiave specifiche per tipo sono disponibili tramite [Documentazione dello schema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Per iniziare, trova il tipo di campo desiderato e utilizza il codice di esempio fornito per generare la richiesta API per [creazione di un gruppo di campi](../api/field-groups.md#create) o [creazione di un tipo di dati](../api/data-types.md#create).

## [!UICONTROL Stringa] {#string}

[!UICONTROL Stringa] i campi sono indicati da `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Facoltativamente, puoi vincolare i tipi di valori che possono essere immessi per la stringa attraverso le seguenti proprietà aggiuntive:

* `pattern`: Un modello regex da vincolare.
* `minLength`: Lunghezza minima della stringa.
* `maxLength`: Lunghezza massima della stringa.

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

[!UICONTROL URI] i campi sono indicati da `type: string` con `format` proprietà impostata su `uri`. Non vengono accettate altre proprietà.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

[!UICONTROL Enum] i campi devono utilizzare `type: string`, con i valori enum stessi forniti in un `enum` array:

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

Facoltativamente, puoi fornire etichette rivolte al cliente per ogni valore sotto a `meta:enum` proprietà, con ogni etichetta associata a un valore corrispondente sotto `enum`.

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
>La `meta:enum` value does **not** dichiarare un&#39;enumerazione o eseguire autonomamente la convalida dei dati. Nella maggior parte dei casi, le stringhe fornite in `meta:enum` sono inoltre forniti ai sensi `enum` per garantire il vincolo dei dati. Tuttavia, in alcuni casi d’uso `meta:enum` è fornito senza `enum` array. Guarda l’esercitazione su [definizione dei valori suggeriti](../tutorials/suggested-values.md) per ulteriori informazioni.

Facoltativamente, puoi fornire un `default` per indicare il valore predefinito `enum` valore che il campo utilizzerà se non viene fornito alcun valore.

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
>Se no `default` viene fornito il valore e il campo enum è impostato su `required`, qualsiasi record in cui manca un valore accettato per questo campo non potrà essere convalidato al momento dell’acquisizione.

## [!UICONTROL Numero] {#number}

I campi numerici sono indicati da `type: number` e non dispongono di altre proprietà richieste.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` I tipi sono utilizzati per qualsiasi tipo numerico, sia intero che a virgola mobile, mentre [`integer` type](#integer) sono utilizzati specificamente per i numeri interi. Fai riferimento a [Documentazione dello schema JSON sui tipi numerici](https://json-schema.org/understanding-json-schema/reference/numeric.html) per ulteriori informazioni sui casi di utilizzo per ciascun tipo.

## [!UICONTROL Intero] {#integer}

[!UICONTROL Intero] i campi sono indicati da `type: integer` e non sono presenti altri campi obbligatori.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Quando `integer` i tipi si riferiscono in particolare ai numeri interi, [`number` type](#number) sono utilizzati per qualsiasi tipo numerico, sia in cifre che in numeri a virgola mobile. Fai riferimento a [Documentazione dello schema JSON sui tipi numerici](https://json-schema.org/understanding-json-schema/reference/numeric.html) per ulteriori informazioni sui casi di utilizzo per ciascun tipo.

Facoltativamente, puoi vincolare l’intervallo del numero intero aggiungendo `minimum` e `maximum` proprietà della definizione. Diversi altri tipi numerici supportati dall’interfaccia utente di Generatore di schema sono `integer` tipi con specifiche `minimum` e `maximum` vincoli, quali [[!UICONTROL Lunga]](#long), [[!UICONTROL Breve]](#short)e [[!UICONTROL Byte]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL Lunga] {#long}

L&#39;equivalente di un [!UICONTROL Lunga] il campo creato tramite l’interfaccia utente di Generatore schema è un [`integer` campo tipo](#integer) con specifiche `minimum` e `maximum` values (`-9007199254740992` e `9007199254740992`, rispettivamente).

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

L&#39;equivalente di un [!UICONTROL Breve] il campo creato tramite l’interfaccia utente di Generatore schema è un [`integer` campo tipo](#integer) con specifiche `minimum` e `maximum` values (`-32768` e `32768`, rispettivamente).

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

L&#39;equivalente di un [!UICONTROL Byte] il campo creato tramite l’interfaccia utente di Generatore schema è un [`integer` campo tipo](#integer) con specifiche `minimum` e `maximum` values (`-128` e `128`, rispettivamente).

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

[!UICONTROL Booleano] i campi sono indicati da `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Facoltativamente, puoi fornire un `default` valore che il campo utilizzerà quando non viene fornito alcun valore esplicito durante l’acquisizione.

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
>Se no `default` viene fornito il valore e il campo booleano è impostato su `required`, qualsiasi record in cui manca un valore accettato per questo campo non potrà essere convalidato al momento dell’acquisizione.

## [!UICONTROL Data] {#date}

[!UICONTROL Data] i campi sono indicati da `type: string` e `format: date`. Facoltativamente, puoi anche fornire un array di `examples` per sfruttare i casi in cui desideri visualizzare una stringa data di esempio per gli utenti che immettono manualmente i dati.

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DateTime] {#date-time}

[!UICONTROL DateTime] i campi sono indicati da `type: string` e `format: date-time`. Facoltativamente, puoi anche fornire un array di `examples` utilizzare nei casi in cui si desidera visualizzare una stringa datetime di esempio per gli utenti che immettono manualmente i dati.

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

[!UICONTROL Array] i campi sono indicati da `type: array` e `items` oggetto che definisce lo schema degli elementi accettati dalla matrice.

È possibile definire elementi array utilizzando tipi primitivi, ad esempio una matrice di stringhe:

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

È inoltre possibile definire gli elementi della matrice in base a un tipo di dati esistente facendo riferimento al `$id` del tipo di dati attraverso un `$ref` proprietà. Di seguito è riportata una matrice di [!UICONTROL Elemento di pagamento] oggetti:

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

[!UICONTROL Oggetto] i campi sono indicati da `type: object` e `properties` oggetto che definisce le proprietà secondarie del campo schema.

Ciascun sottocampo definito in `properties` può essere definito utilizzando qualsiasi `type` o facendo riferimento a un tipo di dati esistente tramite un `$ref` proprietà che punta al `$id` del tipo di dati in questione:

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

È inoltre possibile definire l’intero oggetto tramite il riferimento a un tipo di dati, purché il tipo di dati in questione sia definito come `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Mappa] {#map}

Un campo mappa è essenzialmente un [`object`campo -type](#object) con un set di chiavi non vincolato. Come gli oggetti, le mappe hanno un `type` valore `object`, ma `meta:xdmType` è impostato esplicitamente su `map`.

Una mappa **non deve** definire le proprietà. It **deve** definire un singolo `additionalProperties` schema per descrivere il tipo di valori contenuti nella mappa (ogni mappa può contenere un solo tipo di dati). La `type` deve essere `string` o `integer`.

Ad esempio, un campo mappa con valori di tipo stringa viene definito come segue:

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

Vedi la sezione seguente per ulteriori dettagli sulla creazione di campi mappa personalizzati.

### Creazione di tipi di mappa personalizzati {#custom-maps}

Per supportare in modo efficiente i dati &quot;simili a mappe&quot; in XDM, gli oggetti possono essere annotati con un `meta:xdmType` impostato su `map` per chiarire che un oggetto deve essere gestito come se il set di chiavi non fosse vincolato. I dati acquisiti nei campi mappa devono utilizzare le chiavi stringa e solo i valori stringa o interi (come determinato da `additionalProperties.type`).

XDM pone le seguenti restrizioni all&#39;utilizzo di questo hint di archiviazione:

* I tipi di mappa DEVONO essere di tipo `object`.
* I tipi di mappa NON DEVONO avere proprietà definite (in altre parole, definiscono oggetti &quot;vuoti&quot;).
* I tipi di mappa DEVONO includere `additionalProperties.type` campo che descrive i valori che possono essere inseriti all&#39;interno della mappa, `string` o `integer`.

Assicurati di utilizzare i campi di tipo mappa solo quando è assolutamente necessario, in quanto presentano i seguenti svantaggi prestazionali:

* Tempo di risposta da [Servizio query Adobe Experience Platform](../../query-service/home.md) degrada da tre a dieci secondi per 100 milioni di record.
* Le mappe devono avere meno di 16 chiavi, altrimenti rischiano un ulteriore deterioramento.

L’interfaccia utente di Platform presenta inoltre delle limitazioni nell’estrazione delle chiavi dei campi di tipo mappa. Mentre i campi di tipo oggetto possono essere espansi, le mappe vengono visualizzate come un singolo campo.

## Passaggi successivi

Questa guida illustra come definire diversi tipi di campi nell’API. Per ulteriori informazioni sulla formattazione dei tipi di campo XDM, consulta la guida [Vincoli del tipo di campo XDM](../schema/field-constraints.md).
