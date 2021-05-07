---
keywords: Experience Platform;home;argomenti popolari;schema;schema;gruppo di campi;gruppo di campi;gruppi di campi;tipo di dati;tipi di dati;tipi di dati;tipo di dati;struttura dello schema;tipo di dati;tipo di dati;tipo di dati;tipo di dati;schemi;schema;progettazione dello schema;mappa;mappa;
solution: Experience Platform
title: Vincoli del tipo di campo XDM
topic-legacy: overview
description: Un riferimento per i vincoli di tipo di campo in Experience Data Model (XDM), inclusi gli altri formati di serializzazione a cui possono essere mappati e le modalità di definizione dei tipi di campo personalizzati nell’API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 1%

---

# Vincoli del tipo di campo XDM

Negli schemi Experience Data Model (XDM), il tipo di campo limita il tipo di dati che può contenere il campo. Questo documento fornisce una panoramica di ogni tipo di campo di base, inclusi gli altri formati di serializzazione a cui possono essere mappati e come definire i propri tipi di campo nell’API per applicare vincoli diversi.

## Introduzione

Prima di utilizzare questa guida, controlla le [nozioni di base sulla composizione dello schema](./composition.md) per un&#39;introduzione agli schemi, alle classi e ai gruppi di campi dello schema XDM.

Se prevedi di definire i tuoi tipi di campo nell&#39;API, ti consigliamo vivamente di iniziare con la [Guida per gli sviluppatori del Registro di sistema dello schema](../api/getting-started.md) per scoprire come creare gruppi di campi e tipi di dati in cui includere i campi personalizzati. Se utilizzi l’interfaccia utente Experience Platform per creare gli schemi, consulta la guida [Definizione dei campi nell’interfaccia utente](../ui/fields/overview.md) per scoprire come implementare i vincoli sui campi definiti all’interno di gruppi di campi personalizzati e tipi di dati.

## Struttura di base ed esempi

XDM è basato su uno schema JSON e pertanto i campi XDM ereditano una sintassi simile quando ne definiscono il tipo. Per comprendere in che modo diversi tipi di campi sono rappresentati nello schema JSON, è utile indicare i vincoli di base di ciascun tipo.

>[!NOTE]
>
>Per ulteriori informazioni sullo schema JSON e sulle altre tecnologie sottostanti nelle API di Platform, consulta la [Guida ai fondamentali dell’API](../../landing/api-fundamentals.md#json-schema) .

La tabella seguente illustra il modo in cui ogni tipo XDM viene rappresentato nello schema JSON, insieme a un valore di esempio conforme al tipo:

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>Tipo XDM</th>
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
      <td>[!UICONTROL Doppio]</td>
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
  "massimo": 9007199254740991,
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
  "massimo": 2147483648,
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
  "massimo": 32768,
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
  "massimo": 128,
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

## Mappatura di tipi XDM su altri formati

Le sezioni seguenti descrivono come ogni tipo XDM viene mappato su altri formati di serializzazione comuni:

* [Parquet, SQL Spark e Java](#parquet)
* [Scala, .NET e CosmosDB](#scala)
* [MongoDB, Aerospike e Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Tra i tipi XDM standard elencati nelle tabelle seguenti, è incluso anche il tipo [!UICONTROL Map] . Le mappe vengono utilizzate negli schemi standard quando i dati sono rappresentati come chiavi che corrispondono a determinati valori, o quando le chiavi non possono essere ragionevolmente incluse in uno schema statico e devono essere trattate come valori di dati.
>
>I campi di tipo mappa sono riservati per l’utilizzo dello schema del settore e del fornitore e non possono quindi essere utilizzati nelle risorse personalizzate definite dall’utente. L’inclusione del tipo di mappa nelle tabelle seguenti ha lo scopo di aiutarti a determinare come mappare i dati esistenti su XDM se sono attualmente memorizzati in uno dei formati elencati di seguito.

### Parquet, SQL Spark e Java {#parquet}

| Tipo XDM | Parquet | SQL Spark | Java |
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
| [!UICONTROL Map] | `MAP`-gruppo<br><br> annotato(`<key-type>` deve essere  `STRING`) | `MapType`<br><br>(`keyType` deve essere  `StringType`) | `java.util.Map` |

### Scala, .NET e CosmosDB {#scala}

| Tipo XDM | Scala | .NET | CosmosDB |
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

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospike e Protobuf 2 {#mongo}

| Tipo XDM | MongoDB | Aerospik | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Double] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>(millisecondi Unix) | `int64`<br>(millisecondi Unix) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(millisecondi Unix) | `int64`<br>(millisecondi Unix) |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>(0/1 binario) | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## Definizione dei tipi di campi XDM nell’API {#define-fields}

Tutti i campi XDM sono definiti utilizzando i vincoli standard [JSON Schema](https://json-schema.org/) applicabili al tipo di campo, con vincoli aggiuntivi per i nomi di campo applicati da [!DNL Experience Platform]. L’API del Registro di sistema dello schema consente di definire ulteriori tipi di campi utilizzando i formati e i vincoli facoltativi. I tipi di campo XDM sono esposti dall’attributo a livello di campo `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` è un valore generato dal sistema e pertanto non è necessario aggiungere questa proprietà al JSON per il campo quando si utilizza l’API. Si consiglia di utilizzare i tipi di schema JSON (ad esempio `string` e `integer`) con i vincoli minimi/massimi appropriati, come definito nella tabella seguente.

La tabella seguente delinea la formattazione appropriata per definire diversi tipi di campi, compresi quelli con proprietà facoltative. Ulteriori informazioni sulle proprietà facoltative e sulle parole chiave specifiche per tipo sono disponibili tramite la [documentazione dello schema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Per iniziare, trova il tipo di campo desiderato e utilizza il codice di esempio fornito per generare la richiesta API per [creare un gruppo di campi](../api/field-groups.md#create) o [creare un tipo di dati](../api/data-types.md#create).

<table style="table-layout:auto">
  <tr>
    <th>Tipo XDM</th>
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
    <td>URI [!UICONTROL]</td>
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
    <td>I valori enum vincolati vengono forniti sotto la matrice <code>enum</code>, mentre le etichette facoltative rivolte al cliente per ciascun valore possono essere fornite sotto <code>meta:enum</code>:
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
  "massimo": 9007199254740992
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
  "massimo": 2147483648
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
  "massimo": 32768
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
  "massimo": 128
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
  "type": "booleano",
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
    <td>Matrice di tipi scalari di base (ad esempio stringhe):
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "array",
  "items": {
    "type": "string"
  }
}</pre>
      Array di oggetti definiti da un altro schema:<br/>
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
    <td>L'attributo <code>type</code> di ciascun sottocampo definito in <code>properties</code> può essere definito utilizzando qualsiasi tipo di scala:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "oggetto",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "type": "number"
    }
  }
}</pre>
      I campi di tipo oggetto possono essere definiti facendo riferimento a <code>$id</code> di un tipo di dati:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "oggetto",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Una mappa <strong>non deve</strong> definire proprietà. Per descrivere il tipo di valori contenuti nella mappa, <strong>deve</strong> definire un singolo schema <code>additionalProperties</code> (ogni mappa può contenere solo un singolo tipo di dati). I valori possono essere qualsiasi attributo XDM valido <code>type</code> o un riferimento a un altro schema utilizzando un attributo <code>$ref</code>.<br/><br/>Un campo mappa con valori di tipo stringa:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "oggetto",
  "additionalProperties":{
    "type": "string"
  }
}</pre>
    Campo mappa con array di stringhe per valori:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "oggetto",
  "additionalProperties":{
    "type": "array",
    "items": {
      "type": "string"
    }
  }
}</pre>
    Campo mappa che fa riferimento a un altro tipo di dati:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "oggetto",
  "additionalProperties":{
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>
