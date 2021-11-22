---
keywords: Experience Platform;home;argomenti popolari;schema;schema;gruppo di campi;gruppo di campi;gruppi di campi;tipo di dati;tipi di dati;tipi di dati;tipo di dati;struttura dello schema;tipo di dati;tipo di dati;tipo di dati;tipo di dati;schemi;schema;progettazione dello schema;mappa;mappa;
solution: Experience Platform
title: Vincoli del tipo di campo XDM
topic-legacy: overview
description: Un riferimento per i vincoli di tipo di campo in Experience Data Model (XDM), inclusi gli altri formati di serializzazione a cui possono essere mappati e le modalità di definizione dei tipi di campo personalizzati nell’API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 684237122e7384f6c611e1c602c30af2518aba58
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 3%

---

# Vincoli del tipo di campo XDM

Negli schemi Experience Data Model (XDM), il tipo di campo limita il tipo di dati che può contenere il campo. Questo documento fornisce una panoramica di ogni tipo di campo di base, inclusi gli altri formati di serializzazione a cui possono essere mappati e come definire i propri tipi di campo nell’API per applicare vincoli diversi.

## Introduzione

Prima di utilizzare questa guida, consulta la sezione [nozioni di base sulla composizione dello schema](./composition.md) introduzione a schemi, classi e gruppi di campi schema XDM.

Se prevedi di definire tipi di campi personalizzati nell’API, ti consigliamo vivamente di iniziare con [Guida per gli sviluppatori del Registro di sistema dello schema](../api/getting-started.md) per scoprire come creare gruppi di campi e tipi di dati in cui includere i campi personalizzati. Se utilizzi l’interfaccia utente di Experience Platform per creare gli schemi, consulta la guida in [definizione dei campi nell’interfaccia utente](../ui/fields/overview.md) per scoprire come implementare i vincoli nei campi definiti all’interno dei gruppi di campi personalizzati e dei tipi di dati.

## Struttura di base ed esempi

XDM è basato su uno schema JSON e pertanto i campi XDM ereditano una sintassi simile quando ne definiscono il tipo. Per comprendere in che modo diversi tipi di campi sono rappresentati nello schema JSON, è utile indicare i vincoli di base di ciascun tipo.

>[!NOTE]
>
>Consulta la sezione [Guida di base sulle API](../../landing/api-fundamentals.md#json-schema) per ulteriori informazioni sullo schema JSON e altre tecnologie sottostanti nelle API di Platform.

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
{ "type": "integer", "maximum": 9007199254740991, "minimo": -9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 2147483648, "minimo": -2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 32768, "minimo": -32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 128, "minimo": -128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date-time" }</pre>
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

**Tutte le stringhe formattate con data devono essere conformi allo standard ISO 8601 ([RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Mappatura di tipi XDM su altri formati

Le sezioni seguenti descrivono come ogni tipo XDM viene mappato su altri formati di serializzazione comuni:

* [Parquet, SQL Spark e Java](#parquet)
* [Scala, .NET e CosmosDB](#scala)
* [MongoDB, Aerospike e Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Tra i tipi XDM standard elencati nelle tabelle seguenti, il [!UICONTROL Mappa] è incluso anche il tipo . Le mappe vengono utilizzate negli schemi standard quando i dati sono rappresentati come chiavi che corrispondono a determinati valori, o quando le chiavi non possono essere ragionevolmente incluse in uno schema statico e devono essere trattate come valori di dati.
>
>I campi di tipo mappa sono riservati per l’utilizzo dello schema del settore e del fornitore e non possono quindi essere utilizzati nelle risorse personalizzate definite dall’utente. L’inclusione del tipo di mappa nelle tabelle seguenti ha lo scopo di aiutarti a determinare come mappare i dati esistenti su XDM se sono attualmente memorizzati in uno dei formati elencati di seguito.

### Parquet, SQL Spark e Java {#parquet}

| Tipo XDM | Parquet | SQL Spark | Java |
| --- | --- | --- | --- |
| [!UICONTROL Stringa] | Tipo: `BYTE_ARRAY`<br>Annotazione: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Doppio] | Tipo: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Lunga] | Tipo: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Intero] | Tipo: `INT32`<br>Annotazione: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Breve] | Tipo: `INT32`<br>Annotazione: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Tipo: `INT32`<br>Annotazione: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Data] | Tipo: `INT32`<br>Annotazione: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Tipo: `INT64`<br>Annotazione: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Booleano] | Tipo: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Mappa] | `MAP`-gruppo annotato<br><br>(`<key-type>` devono `STRING`) | `MapType`<br><br>(`keyType` devono `StringType`) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala, .NET e CosmosDB {#scala}

| Tipo XDM | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL Stringa] | `String` | `System.String` | `String` |
| [!UICONTROL Doppio] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Lunga] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Intero] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Breve] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Data] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Booleano] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Mappa] | `Map` | (N/D) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospike e Protobuf 2 {#mongo}

| Tipo XDM | MongoDB | Aerospik | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL Stringa] | `string` | `String` | `string` |
| [!UICONTROL Doppio] | `double` | `Double` | `double` |
| [!UICONTROL Lunga] | `long` | `Integer` | `int64` |
| [!UICONTROL Intero] | `int` | `Integer` | `int32` |
| [!UICONTROL Breve] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Data] | `date` | `Integer`<br>(millisecondi Unix) | `int64`<br>(millisecondi Unix) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(millisecondi Unix) | `int64`<br>(millisecondi Unix) |
| [!UICONTROL Booleano] | `bool` | `Integer`<br>(0/1 binario) | `bool` |
| [!UICONTROL Mappa] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## Definizione dei tipi di campi XDM nell’API {#define-fields}

Tutti i campi XDM sono definiti utilizzando lo standard [Schema JSON](https://json-schema.org/) vincoli applicabili al tipo di campo, con vincoli aggiuntivi per i nomi di campo applicati da [!DNL Experience Platform]. L’API del Registro di sistema dello schema consente di definire ulteriori tipi di campi utilizzando i formati e i vincoli facoltativi. I tipi di campo XDM sono esposti dall’attributo a livello di campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` è un valore generato dal sistema e pertanto non è necessario aggiungere questa proprietà al JSON per il campo quando si utilizza l’API. Si consiglia di utilizzare i tipi di schema JSON (ad esempio `string` e `integer`) con i vincoli minimi/massimi appropriati, come definito nella tabella seguente.

La tabella seguente delinea la formattazione appropriata per definire diversi tipi di campi, compresi quelli con proprietà facoltative. Ulteriori informazioni sulle proprietà facoltative e sulle parole chiave specifiche per tipo sono disponibili tramite [Documentazione dello schema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Per iniziare, trova il tipo di campo desiderato e utilizza il codice di esempio fornito per generare la richiesta API per [creazione di un gruppo di campi](../api/field-groups.md#create) o [creazione di un tipo di dati](../api/data-types.md#create).

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
"sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2 }</pre>
    </td>
  </tr>
  <tr>
    <td>URI [!UICONTROL]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "uri" }</pre>
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
    <td>I valori di enum vincolati vengono forniti sotto la <code>enum</code> array, mentre è possibile fornire etichette facoltative rivolte al cliente per ogni valore in <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "enum": [ "value1", "value2", "value3" ], "meta:enum": { "value1": "Valore 1", "valore2": "Valore 2", "valore3": "Valore 3" }, "default": "value1" }</pre>
    <br>Tieni presente che <code>meta:enum</code> value does <strong>not</strong> dichiarare un'enumerazione o eseguire autonomamente la convalida dei dati. Nella maggior parte dei casi, le stringhe fornite in <code>meta:enum</code> sono inoltre forniti ai sensi <code>enum</code> per garantire il vincolo dei dati. Tuttavia, in alcuni casi d’uso <code>meta:enum</code> è fornito senza <code>enum</code> array. Guarda l’esercitazione su <a href="../tutorials/extend-soft-enum.md">estensione di enum soft</a> per ulteriori informazioni.
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "number" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -9007199254740992, "massimo": 9007199254740992 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -2147483648, "massimo": 2147483648 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -32768, "massimo": 32768 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -128, "massimo": 128 }</pre>
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
"sampleField": { "type": "booleano", "default": false }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Date]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date", "examples": ["2004-10-23"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date-time", "examples": ["2004-10-23T12:00:00-06:00"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>Matrice di tipi scalari di base (ad esempio stringhe):
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "type": "string" } }</pre>
      Matrice di oggetti definita da un altro schema:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "$ref": "https://ns.adobe.com/xdm/data/paymentitem" } }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Object]</td>
    <td></td>
    <td>La <code>type</code> attributo di ciascun sottocampo definito in <code>properties</code> può essere definito utilizzando qualsiasi tipo di scala:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "properties": { "field1": { "type": "string" }, "field2": { "type": "number" } } }</pre>
      I campi di tipo oggetto possono essere definiti facendo riferimento al <code>$id</code> di un tipo di dati:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Una mappa <strong>non deve</strong> definire le proprietà. It <strong>deve</strong> definire un singolo <code>additionalProperties</code> schema per descrivere il tipo di valori contenuti nella mappa (ogni mappa può contenere un solo tipo di dati). I valori possono essere qualsiasi XDM valido <code>type</code> o un riferimento a un altro schema utilizzando un <code>$ref</code> attributo.<br/><br/>Un campo mappa con valori di tipo stringa:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "type": "string" } }</pre>
    Campo mappa con array di stringhe per valori:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "type": "array", "items": { "type": "string" } } }</pre>
    Campo mappa che fa riferimento a un altro tipo di dati:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "$ref": "https://ns.adobe.com/xdm/data/paymentitem" } }</pre>
    </td>
  </tr>
</table>
