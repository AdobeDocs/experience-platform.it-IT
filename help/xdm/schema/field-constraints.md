---
keywords: ' Experience Platform;home;temi comuni;schema;schema;mixin;mixin;mixins;mixins;tipo di dati;tipi di dati;tipi di dati;tipo di dati;schema;tipo di dati;tipo di dati;tipo di dati;tipo di dati;schema;schemi;schema di progettazione;mappa;Mappa;'
solution: Experience Platform
title: Vincoli tipo di campo XDM
topic: overview
description: Un riferimento per i vincoli relativi ai tipi di campo in Experience Data Model (XDM), inclusi gli altri formati di serializzazione a cui possono essere mappati e come definire i propri tipi di campo nell'API.
translation-type: tm+mt
source-git-commit: c9ea7471bb18c92443a5e45c14c8505ef3ccf30d
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 1%

---


# Vincoli del tipo di campo XDM

Negli schemi XDM (Experience Data Model), il tipo di campo vincola il tipo di dati che il campo può contenere. Questo documento fornisce una panoramica di ciascun tipo di campo di base, compresi gli altri formati di serializzazione a cui è possibile mappare e come definire i propri tipi di campo nell&#39;API per applicare vincoli diversi.

## Introduzione

Prima di utilizzare questa guida, vedere le [nozioni di base della composizione dello schema](./composition.md) per un&#39;introduzione agli schemi, alle classi e ai mixin XDM.

Se si prevede di definire i propri tipi di campo nell&#39;API, è fortemente consigliato iniziare con la [Guida per gli sviluppatori del Registro di sistema ](../api/getting-started.md) per imparare a creare mixin e includere i campi personalizzati. Se si utilizza l&#39;interfaccia utente del Experience Platform  per creare gli schemi, consultare la guida relativa alla [definizione dei campi nell&#39;interfaccia utente](../ui/fields/overview.md) per apprendere come implementare i vincoli sui campi definiti all&#39;interno di mixin e tipi di dati personalizzati.

## Struttura di base ed esempi

XDM è basato sullo schema JSON e pertanto i campi XDM ereditano una sintassi simile al momento della definizione del tipo. Comprendere in che modo diversi tipi di campi sono rappresentati nello schema JSON può aiutare a indicare i vincoli di base di ciascun tipo.

>[!NOTE]
>
>Per ulteriori informazioni sullo schema JSON e sulle altre tecnologie sottostanti nelle API della piattaforma, vedi la [Guida di base delle API](../../landing/api-fundamentals.md#json-schema).

Nella tabella seguente è illustrato come ciascun tipo XDM è rappresentato nello schema JSON, insieme a un valore di esempio conforme al tipo:

<table>
  <thead>
    <tr>
      <th>XDM, tipo</th>
      <th>Schema JSON</th>
      <th>Esempio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL String]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Double]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "massima": 9007199254740991,
  "minimo": -9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "massima": 2147483648,
  "minimo": -2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "massima": 32768,
  "minimo": -32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "massima": 128,
  "minimo": -128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "string",
  "format": "date"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "string",
  "format": "data-ora"
}</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Tutte le stringhe in formato data devono essere conformi allo standard ISO 8601 ([RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Mappatura di tipi XDM ad altri formati

Le sezioni seguenti descrivono il modo in cui ciascun tipo XDM viene mappato ad altri formati di serializzazione comuni:

* [Parquet, SQL Spark e Java](#parquet)
* [Scala, .NET e CosmosDB](#scala)
* [MongoDB, Aerospike e Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Tra i tipi XDM standard elencati nelle tabelle seguenti, è incluso anche il tipo [!UICONTROL Map]. Le mappe vengono utilizzate negli schemi standard quando i dati sono rappresentati come chiavi che corrispondono a determinati valori, o quando le chiavi non possono essere ragionevolmente incluse in uno schema statico e devono essere trattate come valori di dati.
>
>I campi del tipo di mappa sono riservati all&#39;utilizzo di schemi del settore e del fornitore e pertanto non possono essere utilizzati nelle risorse personalizzate definite dall&#39;utente. L&#39;inclusione del tipo di mappa nelle tabelle riportate di seguito è solo utile per determinare come mappare i dati esistenti su XDM se sono attualmente memorizzati in uno dei formati elencati di seguito.

### Parquet, SQL Spark e Java {#parquet}

| XDM, tipo | Parquet | SQL Spark | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | Tipo: `BYTE_ARRAY`<br>Annotazione: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Double] | Tipo: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | Tipo: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | Tipo: `INT32`<br>Annotazione: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | Tipo: `INT32`<br>Annotazione: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Tipo: `INT32`<br>Annotazione: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | Tipo: `INT32`<br>Annotazione: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Tipo: `INT64`<br>Annotazione: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | Tipo: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP`-annotated group<br><br>(`<key-type>` must be  `STRING`) | `MapType`<br><br>(`keyType` deve essere  `StringType`) | `java.util.Map` |

### Scala, .NET e CosmosDB {#scala}

| XDM, tipo | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Double] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | (N/D) | `object` |

### MongoDB, Aerospike e Protobuf 2 {#mongo}

| XDM, tipo | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Double] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>(Unix millisecondi) | `int64`<br>(Unix millisecondi) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix millisecondi) | `int64`<br>(Unix millisecondi) |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>(0/1 binario) | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

## Definizione dei tipi di campo XDM nell&#39;API {#define-fields}

Tutti i campi XDM sono definiti utilizzando i vincoli standard [JSON Schema](https://json-schema.org/) applicabili al tipo di campo, con vincoli aggiuntivi per i nomi di campo applicati da [!DNL Experience Platform]. L&#39;API del Registro di sistema dello schema consente di definire ulteriori tipi di campi mediante l&#39;uso di formati e vincoli facoltativi. I tipi di campo XDM sono esposti dall&#39;attributo a livello di campo `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` è un valore generato dal sistema e pertanto non è necessario aggiungere questa proprietà al JSON per il campo quando si utilizza l&#39;API. Come procedura ottimale si consiglia di utilizzare i tipi di schema JSON (ad esempio `string` e `integer`) con i vincoli min/max appropriati, come definito nella tabella seguente.

La tabella seguente delinea la formattazione appropriata per definire tipi di campi diversi, compresi quelli con proprietà facoltative. Ulteriori informazioni sulle proprietà facoltative e sulle parole chiave specifiche per i tipi sono disponibili tramite la [documentazione sullo schema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Per iniziare, trova il tipo di campo desiderato e utilizza il codice di esempio fornito per creare la richiesta API per la creazione di un mixin](../api/mixins.md#create) o [creazione di un tipo di dati](../api/data-types.md#create).[

<table>
  <tr>
    <th>XDM, tipo</th>
    <th>Proprietà facoltative</th>
    <th>Esempio</th>
  </tr>
  <tr>
    <td>[!UICONTROL String]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
    "type": "string",
    "pattern": "^[A-Z]{2}$",
    "maxLength": 2
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "format": "uri"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Enum]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>I valori enum vincolati sono forniti nell'array <code>enum</code>, mentre le etichette personalizzate facoltative per ciascun valore possono essere fornite in <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Valore 1",
      "value2": "Valore 2",
      "value3": "Valore 3"
  },
  "default": "value1"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "number"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimo": -9007199254740992,
  "massima": 9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimo": -2147483648,
  "massima": 2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimo": -32768,
  "massima": 32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimo": -128,
  "massima": 128
  }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Boolean]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "boolean",
  "default": false
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Date]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "format": "date",
  "esempi": ["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "format": "data-ora",
  "esempi": ["2004-10-23T12:00:00-06:00"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>Un array di tipi scalari di base (ad esempio, stringhe):
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "array",
  "items": {
    "type": "string"
  }
}</pre>
      Un array di oggetti definiti da un altro schema:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Object]</td>
    <td></td>
    <td>L'attributo <code>type</code> di ciascun sottocampo definito in <code>properties</code> può essere definito utilizzando qualsiasi tipo scalare:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "type": "number"
    }
  }
}</pre>
      I campi del tipo di oggetto possono essere definiti facendo riferimento a <code>$id</code> di un tipo di dati:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Una mappa <strong>non deve </strong> definire proprietà. <strong>deve </strong> definire un singolo schema <code>additionalProperties</code> per descrivere il tipo di valori contenuti nella mappa (ogni mappa può contenere solo un singolo tipo di dati). I valori possono essere qualsiasi attributo XDM <code>type</code> valido o un riferimento a un altro schema che utilizza un attributo <code>$ref</code>.<br/><br/>Campo mappa con valori di tipo stringa:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "AdditionalProperties":{
    "type": "string"
  }
}</pre>
    Campo mappa con array di stringhe per valori:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "AdditionalProperties":{
    "type": "array",
    "items": {
      "type": "string"
    }
  }
}</pre>
    Campo mappa che fa riferimento a un altro tipo di dati:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "AdditionalProperties":{
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>
