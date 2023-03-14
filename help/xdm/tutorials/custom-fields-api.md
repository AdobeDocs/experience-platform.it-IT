---
title: Definire i campi XDM nell’API del registro dello schema
description: Scopri come definire campi diversi durante la creazione di risorse Experience Data Model (XDM) personalizzate nell’API Schema Registry.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Definire i campi XDM nell’API del registro dello schema

Tutti i campi Experience Data Model (XDM) sono definiti utilizzando lo standard [Schema JSON](https://json-schema.org/) vincoli che si applicano al relativo tipo di campo, con vincoli aggiuntivi per i nomi di campo applicati da Adobe Experience Platform. L’API Schema Registry consente di definire campi personalizzati negli schemi tramite l’utilizzo di formati e vincoli facoltativi. I tipi di campo XDM vengono esposti dall’attributo a livello di campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` è un valore generato dal sistema, pertanto non è necessario aggiungere questa proprietà al JSON per il campo quando si utilizza l’API (tranne quando [creazione di tipi di mappe personalizzati](#custom-maps)). Si consiglia di utilizzare i tipi di schema JSON (ad esempio `string` e `integer`) con i vincoli min/max appropriati definiti nella tabella seguente.

Questa guida descrive la formattazione appropriata per definire diversi tipi di campi, inclusi quelli con proprietà facoltative. Ulteriori informazioni sulle proprietà facoltative e sulle parole chiave specifiche per tipo sono disponibili tramite [Documentazione sullo schema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Per iniziare, individua il tipo di campo desiderato e utilizza il codice di esempio fornito per creare la richiesta API per [creazione di un gruppo di campi](../api/field-groups.md#create) o [creazione di un tipo di dati](../api/data-types.md#create).

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

* `pattern`: pattern regex da vincolare con.
* `minLength`: lunghezza minima della stringa.
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

[!UICONTROL URI] i campi sono indicati da `type: string` con un `format` proprietà impostata su `uri`. Non sono accettate altre proprietà.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

[!UICONTROL Enum] i campi devono utilizzare `type: string`, con i valori enum forniti sotto un `enum` array:

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

Facoltativamente, puoi fornire etichette rivolte al cliente per ciascun valore in una `meta:enum` con ogni etichetta digitata su un valore corrispondente in `enum`.

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
>Il `meta:enum` il valore fa **non** dichiarare un’enumerazione o eseguire da sola la convalida dei dati. Nella maggior parte dei casi, le stringhe fornite in `meta:enum` sono fornite anche in `enum` per garantire la limitazione dei dati. Tuttavia, in alcuni casi d’uso `meta:enum` è fornito senza un corrispondente `enum` array. Guarda il tutorial su [definizione dei valori suggeriti](../tutorials/suggested-values.md) per ulteriori informazioni.

Facoltativamente, puoi fornire una `default` per indicare il valore predefinito `enum` valore che il campo utilizzerà se non viene fornito alcun valore.

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
>In caso negativo `default` viene fornito un valore e il campo enum è impostato su `required`, qualsiasi record in cui manca un valore accettato per questo campo non supererà la convalida al momento dell’acquisizione.

## [!UICONTROL Numero] {#number}

I campi numerici sono indicati da `type: number` e non hanno altre proprietà richieste.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` i tipi vengono utilizzati per qualsiasi tipo numerico, ovvero numeri interi o numeri a virgola mobile, mentre [`integer` tipi](#integer) sono utilizzati specificamente per i numeri integrali. Consulta la sezione [Documentazione dello schema JSON sui tipi numerici](https://json-schema.org/understanding-json-schema/reference/numeric.html) per ulteriori informazioni sui casi d’uso per ciascun tipo.

## [!UICONTROL Intero] {#integer}

[!UICONTROL Intero] i campi sono indicati da `type: integer` e non hanno altri campi obbligatori.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Mentre `integer` i tipi si riferiscono specificamente a numeri integrali, [`number` tipi](#number) vengono utilizzati per qualsiasi tipo numerico, numeri interi o numeri a virgola mobile. Consulta la sezione [Documentazione dello schema JSON sui tipi numerici](https://json-schema.org/understanding-json-schema/reference/numeric.html) per ulteriori informazioni sui casi d’uso per ciascun tipo.

Facoltativamente, puoi vincolare l’intervallo del numero intero aggiungendo `minimum` e `maximum` alla definizione. Diversi altri tipi numerici supportati dall’interfaccia utente di Schema Builder sono semplicemente `integer` tipi con specifiche `minimum` e `maximum` vincoli, come [[!UICONTROL Lungo]](#long), [[!UICONTROL Breve]](#short), e [[!UICONTROL Byte]](#byte).

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

L&#39;equivalente di un [!UICONTROL Lungo] creato tramite l’interfaccia utente di Schema Builder è un campo [`integer` campo tipo](#integer) con specifiche `minimum` e `maximum` valori (`-9007199254740992` e `9007199254740992`, rispettivamente).

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

L&#39;equivalente di un [!UICONTROL Breve] creato tramite l’interfaccia utente di Schema Builder è un campo [`integer` campo tipo](#integer) con specifiche `minimum` e `maximum` valori (`-32768` e `32768`, rispettivamente).

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

L&#39;equivalente di un [!UICONTROL Byte] creato tramite l’interfaccia utente di Schema Builder è un campo [`integer` campo tipo](#integer) con specifiche `minimum` e `maximum` valori (`-128` e `128`, rispettivamente).

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

Facoltativamente, puoi fornire una `default` valore che il campo utilizzerà quando non viene fornito alcun valore esplicito durante l’acquisizione.

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
>In caso negativo `default` viene fornito un valore e il campo booleano viene impostato su `required`, qualsiasi record in cui manca un valore accettato per questo campo non supererà la convalida al momento dell’acquisizione.

## [!UICONTROL Data] {#date}

[!UICONTROL Data] i campi sono indicati da `type: string` e `format: date`. Facoltativamente, puoi anche fornire un array di `examples` per sfruttare nei casi in cui desideri visualizzare una stringa di data di esempio per gli utenti che immettono manualmente i dati.

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

[!UICONTROL DateTime] i campi sono indicati da `type: string` e `format: date-time`. Facoltativamente, puoi anche fornire un array di `examples` per sfruttare nei casi in cui desideri visualizzare una stringa di esempio datetime per gli utenti che immettono manualmente i dati.

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

[!UICONTROL Array] i campi sono indicati da `type: array` e un `items` oggetto che definisce lo schema degli elementi che l’array accetterà.

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

È inoltre possibile definire gli elementi array in base a un tipo di dati esistente facendo riferimento al `$id` del tipo di dati tramite un `$ref` proprietà. Di seguito è riportato un array di [!UICONTROL Voce di pagamento] oggetti:

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

[!UICONTROL Oggetto] i campi sono indicati da `type: object` e un `properties` oggetto che definisce le sottoproprietà per il campo schema.

Ogni sottocampo definito in `properties` può essere definito utilizzando qualsiasi valore primitivo `type` o facendo riferimento a un tipo di dati esistente tramite un `$ref` proprietà che punta al `$id` del tipo di dati in questione:

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

Un campo mappa è essenzialmente un [`object`campo -type](#object) con un set di chiavi non vincolato. Analogamente agli oggetti, le mappe presentano `type` valore di `object`, ma il loro `meta:xdmType` è impostato esplicitamente su `map`.

Una mappa **non deve** definisci eventuali proprietà. It **deve** definire un singolo `additionalProperties` schema per descrivere il tipo di valori contenuti nella mappa (ogni mappa può contenere un solo tipo di dati). Il `type` il valore deve essere `string` o `integer`.

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

Per supportare in modo efficiente i dati di tipo mappa in XDM, gli oggetti possono essere annotati con una `meta:xdmType` imposta su `map` per chiarire che un oggetto deve essere gestito come se il set di chiavi non fosse vincolato. I dati acquisiti nei campi mappa devono utilizzare chiavi stringa e solo valori stringa o interi (come determinato da `additionalProperties.type`).

XDM pone le seguenti restrizioni sull’utilizzo di questo hint di archiviazione:

* I tipi di mappa DEVONO essere di tipo `object`.
* I tipi di mappa NON DEVONO avere proprietà definite (in altre parole, definiscono oggetti &quot;vuoti&quot;).
* I tipi di mappa DEVONO includere un `additionalProperties.type` che descrive i valori che possono essere inseriti nella mappa, `string` o `integer`.

Assicurati di utilizzare campi di tipo mappa solo quando assolutamente necessario, in quanto presentano i seguenti svantaggi in termini di prestazioni:

* Tempo di risposta da [Servizio query Adobe Experience Platform](../../query-service/home.md) si riducono da tre a dieci secondi per 100 milioni di record.
* Le mappe devono avere meno di 16 chiavi altrimenti si rischia un ulteriore degrado.

Anche l’interfaccia utente di Platform presenta limitazioni su come estrarre le chiavi dei campi di tipo mappa. Mentre i campi di tipo oggetto possono essere espansi, le mappe vengono visualizzate come un singolo campo.

## Passaggi successivi

Questa guida illustra come definire diversi tipi di campi nell’API. Per ulteriori informazioni sulla formattazione dei tipi di campo XDM, consulta la guida su [Vincoli del tipo di campo XDM](../schema/field-constraints.md).
