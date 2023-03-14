---
keywords: Experience Platform;home;argomenti popolari;schema;schema;gruppo di campi;gruppo di campi;gruppi di campi;gruppi di campi;tipo di dati;tipi di dati;tipi di dati;tipo di dati;progettazione schema;tipo di dati;tipo di dati;tipo di dati;tipo di dati;schemi;schemi;progettazione schema;mappa;mappa;
solution: Experience Platform
title: Vincoli per il tipo di campo XDM
description: Un riferimento per i vincoli dei tipi di campo in Experience Data Model (XDM), inclusi gli altri formati di serializzazione a cui possono essere mappati e come definire tipi di campo personalizzati nell’API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 4%

---

# Vincoli del tipo di campo XDM

Negli schemi Experience Data Model (XDM), il tipo di un campo limita il tipo di dati che il campo può contenere. Questo documento fornisce una panoramica di ogni tipo di campo principale, inclusi gli altri formati di serializzazione a cui possono essere mappati e come definire tipi di campo personalizzati nell’API per applicare vincoli diversi.

## Introduzione

Prima di utilizzare questa guida, consultare [nozioni di base sulla composizione dello schema](./composition.md) per un’introduzione a schemi, classi e gruppi di campi di schema XDM.

Se prevedi di definire tipi di campo personalizzati nell’API, si consiglia vivamente di iniziare con [Guida per gli sviluppatori del registro dello schema](../api/getting-started.md) per scoprire come creare gruppi di campi e tipi di dati per includere i campi personalizzati in. Se utilizzi l’interfaccia utente di Experience Platform per creare gli schemi, consulta la guida su [definizione dei campi nell’interfaccia utente](../ui/fields/overview.md) per scoprire come implementare vincoli sui campi definiti all’interno di gruppi di campi e tipi di dati personalizzati.

## Struttura di base ed esempi {#basic-types}

XDM è basato su schema JSON e pertanto i campi XDM ereditano una sintassi simile durante la definizione del relativo tipo. Informazioni sulla modalità di rappresentazione dei diversi tipi di campo nello schema JSON possono essere utili per indicare i vincoli di base di ciascun tipo.

>[!NOTE]
>
>Consulta la [Guida di base sulle API](../../landing/api-fundamentals.md#json-schema) per ulteriori informazioni sullo schema JSON e su altre tecnologie sottostanti nelle API di Platform.

La tabella seguente illustra come ogni tipo XDM viene rappresentato nello schema JSON, insieme a un valore di esempio conforme al tipo:

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
      <td>[!UICONTROL Stringa]</td>
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
{ "type": "integer", "maximum": 9007199254740991, "minimum": -9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 2147483648, "minimum": -2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 32768, "minimum": -32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 128, "minimum": -128 }</pre>
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

**Tutte le stringhe in formato data devono essere conformi allo standard ISO 8601 ([RFC 3339, paragrafo 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Mappatura dei tipi XDM su altri formati

Le sezioni seguenti descrivono come ogni tipo XDM viene mappato su altri formati di serializzazione comuni:

* [Parquet, Spark SQL e Java](#parquet)
* [Scala, .NET e CosmosDB](#scala)
* [MongoDB, Aerospike e Protobuf 2](#mongo)

>[!NOTE]
>
>Tra i tipi XDM standard elencati nelle tabelle seguenti, il [!UICONTROL Mappa] è incluso anche il tipo. Le mappe vengono utilizzate negli schemi standard quando i dati sono rappresentati come chiavi che si associano a determinati valori, o quando le chiavi non possono essere ragionevolmente incluse in uno schema statico e devono essere trattate come valori di dati.
>
>Molti componenti XDM standard utilizzano tipi di mappa e puoi anche [definire campi mappa personalizzati](../tutorials/custom-fields-api.md#custom-maps) se desiderato. L’inclusione del tipo di mappa nelle tabelle seguenti è utile per determinare come mappare i dati esistenti su XDM se sono attualmente memorizzati in uno dei formati elencati di seguito.

### Parquet, Spark SQL e Java {#parquet}

| Tipo XDM | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL Stringa] | Tipo: `BYTE_ARRAY`<br>Annotazione: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Doppio] | Tipo: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Lungo] | Tipo: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Intero] | Tipo: `INT32`<br>Annotazione: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Breve] | Tipo: `INT32`<br>Annotazione: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Tipo: `INT32`<br>Annotazione: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Data] | Tipo: `INT32`<br>Annotazione: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Tipo: `INT64`<br>Annotazione: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Booleano] | Tipo: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Mappa] | `MAP`-gruppo con annotazioni<br><br>(`<key-type>` deve essere `STRING`) | `MapType`<br><br>(`keyType` deve essere `StringType`) | `java.util.Map` |

{style="table-layout:auto"}

### Scala, .NET e CosmosDB {#scala}

| Tipo XDM | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL Stringa] | `String` | `System.String` | `String` |
| [!UICONTROL Doppio] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Lungo] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Intero] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Breve] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Data] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Booleano] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Mappa] | `Map` | (N/D) | `object` |

{style="table-layout:auto"}

### MongoDB, Aerospike e Protobuf 2 {#mongo}

| Tipo XDM | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL Stringa] | `string` | `String` | `string` |
| [!UICONTROL Doppio] | `double` | `Double` | `double` |
| [!UICONTROL Lungo] | `long` | `Integer` | `int64` |
| [!UICONTROL Intero] | `int` | `Integer` | `int32` |
| [!UICONTROL Breve] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Data] | `date` | `Integer`<br>(Unix millisecondi) | `int64`<br>(Unix millisecondi) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix millisecondi) | `int64`<br>(Unix millisecondi) |
| [!UICONTROL Booleano] | `bool` | `Integer`<br>(0/1 binario) | `bool` |
| [!UICONTROL Mappa] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## Definizione dei tipi di campi XDM nell’API {#define-fields}

L’API Schema Registry consente di definire campi personalizzati tramite l’utilizzo di formati e vincoli facoltativi. Consulta la guida su [definizione dei campi personalizzati nell’API Schema Registry](../tutorials/custom-fields-api.md) per ulteriori informazioni.
