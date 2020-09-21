---
keywords: Experience Platform;home;popular topics;schema;Schema;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;schema design;datatype;Datatype;data type;Data type;schemas;Schemas;Schema design;map;Map;
solution: Experience Platform
title: Vincoli del tipo di campo XDM
topic: overview
description: Un riferimento per i vincoli dei tipi di campo XDM, compresi gli altri formati di serializzazione a cui possono essere mappati e come definire i propri tipi di campo nell'API.
translation-type: tm+mt
source-git-commit: 19167f58fae6fac7d938deb74182d2e19960beb3
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 5%

---


# Vincoli del tipo di campo XDM

I tipi di campo XDM selezionati per gli schemi limitano il tipo di dati che tali campi possono contenere. Questo documento fornisce una panoramica di ciascun tipo di campo di base, compresi gli altri formati di serializzazione a cui è possibile mappare, e come definire i propri tipi di campo nell&#39;API per applicare vincoli diversi.

## Introduzione

Prima di utilizzare questa guida, vedere le [nozioni di base della composizione](./composition.md) dello schema per un&#39;introduzione agli schemi, alle classi e ai mixin XDM.

Se si prevede di definire i propri tipi di campo, è consigliabile iniziare con la guida [per gli sviluppatori del Registro di](../api/getting-started.md) schema per apprendere come creare mixin e tipi di dati in cui includere i campi personalizzati.

## Mappatura di tipi XDM ad altri formati

La tabella seguente descrive la mappatura tra ciascun tipo XDM (`meta:xdmType`) e altri formati di serializzazione.

| XDM Type<br>(meta:xdmType) | JSON<br>(Schema JSON) | Parquet<br>(tipo/annotazione) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Stringa | System.String | Stringa | string | Stringa | string |
| numero | type:number | DOPPIO | DoubleType | java.lang.Double | Doppio | System.Double | Numero | double | Doppio | double |
| long | tipo:<br>numero intero massimo:2^53+1<br>minimo:-2^53+1 | INT64 | LongType | java.lang.Long | Long | System.Int64 | Numero | long | Intero | int64 |
| int | tipo:<br>numero intero massimo:2^31<br>minimo:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Numero | int | Intero | int32 |
| short | tipo:<br>numero intero massimo:2^15<br>minimo:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Breve | System.Int16 | Numero | int | Intero | int32 |
| byte | tipo:<br>numero intero massimo:2^7<br>minimo:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Numero | int | Intero | int32 |
| booleano | type:boolean | BOOLEANO | BooleanType | java.lang.Boolean | Booleano | System.Boolean | Booleano | boe | Intero | Intero | boe |
| data | type:<br>stringformat:date<br>(RFC 3339, sezione 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Stringa | data | Integer<br>(unix millis) | int64<br>(unix millis) |
| data-ora | type:<br>stringformat:date-time<br>(RFC 3339, sezione 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Stringa | timestamp | Integer<br>(unix millis) | int64<br>(unix millis) |
| map | object | MAP annotated group<br><br>&lt;<span>key_type</span>> DEVE essere STRING<br><br>&lt;<span>value_type</span>> tipo di valori mappa | MapType<br><br>&quot;keyType&quot; DEVE essere StringType<br><br>&quot;valueType&quot; è il tipo di valori della mappa. | java.util.Map | Mappa | --- | object | object | map | map&lt;<span>key_type, value_type</span>> |

## Definizione dei tipi di campo XDM nell&#39;API

Gli schemi XDM sono definiti utilizzando gli standard [JSON Schema](https://json-schema.org/) e i tipi di campo di base, con vincoli aggiuntivi per i nomi di campo che vengono applicati da [!DNL Experience Platform]. L&#39;API [del Registro di sistema dello](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) schema consente di definire ulteriori tipi di campi mediante l&#39;uso di formati e vincoli facoltativi. I tipi di campo XDM sono esposti dall&#39;attributo a livello di campo `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` è un valore generato dal sistema e pertanto non è necessario aggiungere questa proprietà al JSON per il campo. Come procedura ottimale si consiglia di utilizzare tipi di schema JSON (come stringa e numero intero) con i vincoli min/max appropriati, come definito nella tabella seguente.

La tabella seguente delinea la formattazione appropriata per definire i tipi di campi scalari e i tipi di campi più specifici utilizzando le proprietà facoltative. Ulteriori informazioni sulle proprietà facoltative e sulle parole chiave specifiche per i tipi sono disponibili nella documentazione [sullo schema](https://json-schema.org/understanding-json-schema/reference/type.html)JSON.

Per iniziare, trova il tipo di campo desiderato e utilizza il codice di esempio fornito per creare la richiesta API per [creare un mixin](../api/create-mixin.md) o [creare un tipo](../api/create-data-type.md)di dati.

<table>
  <tr>
    <th>Tipo<br/>desiderato (meta:xdmType)</th>
    <th>JSON<br/>(Schema JSON)</th>
    <th>Esempio di codice</th>
  </tr>
  <tr>
    <td>string</td>
    <td>type: Proprietà<br/><br/><strong>stringOptional:</strong><br/>
      <ul>
        <li>pattern</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type: formato<br/>stringa: uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: string)</td>
    <td>type: Proprietà<br/><br/><strong>stringOptional:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>Specificate le etichette delle opzioni rivolte al cliente utilizzando "meta:enum":
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "enum": [ "value1", "value2", "value3" ], "meta:enum": { "value1": "Valore 1", "valore2": "Valore 2", "valore3": "Value 3" }, "default": "value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>numero</td>
    <td>type: numero<br/>minimo: ±2,23×10^308<br/>massimo: ±1,80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>type: massimo<br/>intero:2^53+1<br>minimo:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "Minimum": -9007199254740992, "massimo": 9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type: massimo<br/>intero:2^31<br>minimo:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "Minimum": -2147483648, "massimo": 2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>type: massimo<br/>intero:2^15<br>minimo:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "Minimum": -32768, "massimo": 32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type: massimo<br/>intero:2^7<br>minimo:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "Minimum": -128, "massimo": 128 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>booleano</td>
    <td><br/>type: boolean<br/>{true, false}<br/><br/><strong>Proprietà facoltativa:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "boolean", "default": false }
      </pre>
    </td>
  </tr>
  <tr>
    <td>data</td>
    <td>type: formato<br/>stringa: date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "date", "example": ["2004-10-23"] }
      </pre>
      Data come definita dalla <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, sezione 5.6</a>, dove "data completa" = data-intero "-" data-mese "-" data-giorno (AAAA-MM-GG)
    </td>
  </tr>
  <tr>
    <td>data-ora</td>
    <td>type: formato<br/>stringa: data-ora</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "data-ora", "esempi": ["2004-10-23T12:00:00-06:00"] }
      </pre>
      Data-ora, come definito dalla <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, sezione 5.6</a>, dove "data-ora" = data completa "T" a tempo pieno:<br/>(AAAA-MM-GG'T'HH:MM:SS.SSSSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>type: array</td>
    <td>items.type può essere definito utilizzando qualsiasi tipo scalare:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "type": "string" }
      </pre>
      Array di oggetti definiti da un altro schema:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "$ref": "id" }
      </pre>
      Dove "id" è il {id} dello schema di riferimento.
    </td>
  </tr>
  <tr>
    <td>object</td>
    <td>type: object</td>
    <td>proprietà.{field}.type può essere definito utilizzando qualsiasi tipo scalare:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "properties": { "field1": { "type": "string" }, "field2": { "type": "number" } }
      </pre>
      Campo di tipo "oggetto" definito da uno schema di riferimento:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "$ref": "id" }
      </pre>
      Dove "id" è il {id} dello schema di riferimento.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>type:<br/><br/><strong>objectNota:</strong><br/>l'utilizzo del tipo di dati 'map' è riservato all'utilizzo dello schema del settore e del fornitore e non è disponibile per l'uso nei campi definiti dal tenant. Viene utilizzato negli schemi standard quando i dati sono rappresentati come chiavi che corrispondono a un certo valore, o quando le chiavi non possono essere incluse in uno schema statico e devono essere trattate come valori di dati.</td>
    <td>UNA 'mappa' NON DEVE definire alcuna proprietà. DEVE definire un singolo schema "[!UICONTROL AdditionalProperties]" per descrivere il tipo di valori contenuti nella 'map'. Una 'mappa' in XDM può contenere un solo tipo di dati. I valori possono essere una qualsiasi definizione di schema XDM valida, inclusa una matrice o un oggetto, o come riferimento a un altro schema (tramite $ref).<br/><br/>Campo mappa con valori di tipo 'stringa':
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "AdditionalProperties":{ "type": "string" }
      </pre>
    Mappa campo con valori che costituiscono un array di stringhe:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "AdditionalProperties":{ "type": "array", "items": { "type": "string" } } }
      </pre>
    Campo mappa che fa riferimento a un altro schema:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "AdditionalProperties":{ "$ref": "id" }
      </pre>
      Dove "id" è il {id} dello schema di riferimento.
    </td>
  </tr>
</table>
