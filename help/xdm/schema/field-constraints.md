---
keywords: Experience Platform;home;argomenti popolari;schema;schema;gruppo di campi;gruppo di campi;gruppi di campi;tipo di dati;tipi di dati;tipi di dati;tipo di dati;struttura dello schema;tipo di dati;tipo di dati;tipo di dati;tipo di dati;schemi;schema;progettazione dello schema;mappa;mappa;
solution: Experience Platform
title: Vincoli del tipo di campo XDM
topic-legacy: overview
description: Un riferimento per i vincoli di tipo di campo in Experience Data Model (XDM), inclusi gli altri formati di serializzazione a cui possono essere mappati e le modalità di definizione dei tipi di campo personalizzati nell’API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 2a58236031834bbe298576e2fcab54b04ec16ac3
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 6%

---

# Vincoli del tipo di campo XDM

Negli schemi Experience Data Model (XDM), il tipo di campo limita il tipo di dati che può contenere il campo. Questo documento fornisce una panoramica di ogni tipo di campo di base, inclusi gli altri formati di serializzazione a cui possono essere mappati e come definire i propri tipi di campo nell’API per applicare vincoli diversi.

## Introduzione

Prima di utilizzare questa guida, consulta la sezione [nozioni di base sulla composizione dello schema](./composition.md) introduzione a schemi, classi e gruppi di campi schema XDM.

Se prevedi di definire tipi di campi personalizzati nell’API, ti consigliamo vivamente di iniziare con [Guida per gli sviluppatori del Registro di sistema dello schema](../api/getting-started.md) per scoprire come creare gruppi di campi e tipi di dati in cui includere i campi personalizzati. Se utilizzi l’interfaccia utente di Experience Platform per creare gli schemi, consulta la guida in [definizione dei campi nell’interfaccia utente](../ui/fields/overview.md) per scoprire come implementare i vincoli nei campi definiti all’interno dei gruppi di campi personalizzati e dei tipi di dati.

## Struttura di base ed esempi {#basic-types}

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

L’API del Registro di sistema dello schema consente di definire campi personalizzati tramite l’utilizzo di formati e vincoli facoltativi. Consulta la guida su [definizione dei campi personalizzati nell’API del Registro di sistema dello schema](../tutorials/custom-fields-api.md) per ulteriori informazioni.
