---
keywords: ' Experience Platform;home;temi comuni;schema;schema;mixin;mixin;mixins;mixins;tipo di dati;tipi di dati;tipi di dati;tipo di dati;schema;tipo di dati;tipo di dati;tipo di dati;tipo di dati;schema;schemi;schema di progettazione;mappa;Mappa;'
solution: Experience Platform
title: Vincoli tipo di campo XDM
topic: overview
description: Un riferimento per i vincoli dei tipi di campo XDM, compresi gli altri formati di serializzazione a cui possono essere mappati e come definire i propri tipi di campo nell'API.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 4%

---


# Vincoli del tipo di campo XDM

I tipi di campo XDM selezionati per gli schemi limitano il tipo di dati che tali campi possono contenere. Questo documento fornisce una panoramica di ciascun tipo di campo di base, compresi gli altri formati di serializzazione a cui è possibile mappare, e come definire i propri tipi di campo nell&#39;API per applicare vincoli diversi.

## Introduzione

Prima di utilizzare questa guida, vedere le [nozioni di base della composizione dello schema](./composition.md) per un&#39;introduzione agli schemi, alle classi e ai mixin XDM.

Se si prevede di definire i propri tipi di campo, è consigliabile iniziare con la [Guida per gli sviluppatori del Registro di sistema dello schema](../api/getting-started.md) per apprendere come creare mixin e tipi di dati in cui includere i campi personalizzati.

## Mappatura di tipi XDM ad altri formati

La tabella seguente descrive la mappatura tra ciascun tipo XDM (`meta:xdmType`) e altri formati di serializzazione.

| XDM Type<br>(meta:xdmType) | JSON<br>(schema JSON) | Parquet<br>(tipo/annotazione) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Stringa | System.String | Stringa | string | Stringa | string |
| numero | type:number | DOPPIO | DoubleType | java.lang.Double | Doppio | System.Double | Numero | double | Doppio | double |
| long | tipo:integer<br>massimo:2^53+1<br>minimo:-2^53+1 | INT64 | LongType | java.lang.Long | Long | System.Int64 | Numero | long | Intero | int64 |
| int | type:integer<br>massima:2^31<br>minima:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Numero | int | Intero | int32 |
| short | tipo:integer<br>massimo:2^15<br>minimo:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Breve | System.Int16 | Numero | int | Intero | int32 |
| byte | tipo:integer<br>massimo:2^7<br>minimo:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Numero | int | Intero | int32 |
| booleano | type:boolean | BOOLEANO | BooleanType | java.lang.Boolean | Booleano | System.Boolean | Booleano | boe | Intero | Intero | boe |
| data | type:string<br>format:date<br>(RFC 3339, sezione 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Stringa | data | Integer<br>(unix millis) | int64<br>(unix millis) |
| data-ora | type:string<br>format:date-time<br>(RFC 3339, sezione 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Stringa | timestamp | Integer<br>(unix millis) | int64<br>(unix millis) |
| map | object | MAP annotated group<br><br>&lt;<span>key_type</span>>> DEVE essere STRING<br><br>&lt;<span>value_type</span>> tipo di valori mappa | MapType<br><br>&quot;keyType&quot; DEVE essere StringType<br><br>&quot;valueType&quot; è il tipo di valori della mappa. | java.util.Map | Mappa | — | object | object | map | map&lt;<span>key_type, value_type</span> |

## Definizione dei tipi di campo XDM nell&#39;API {#define-fields}

Gli schemi XDM sono definiti utilizzando gli standard [JSON Schema](https://json-schema.org/) e i tipi di campo di base, con vincoli aggiuntivi per i nomi di campo applicati da [!DNL Experience Platform]. L&#39; [API del Registro di sistema dello schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) consente di definire ulteriori tipi di campi mediante l&#39;uso di formati e vincoli facoltativi. I tipi di campo XDM sono esposti dall&#39;attributo a livello di campo `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` è un valore generato dal sistema e pertanto non è necessario aggiungere questa proprietà al JSON per il campo. Come procedura ottimale si consiglia di utilizzare tipi di schema JSON (come stringa e numero intero) con i vincoli min/max appropriati, come definito nella tabella seguente.

La tabella seguente delinea la formattazione appropriata per definire i tipi di campi scalari e i tipi di campi più specifici utilizzando le proprietà facoltative. Ulteriori informazioni sulle proprietà facoltative e sulle parole chiave specifiche per i tipi sono disponibili tramite la [documentazione sullo schema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Per iniziare, trova il tipo di campo desiderato e utilizza il codice di esempio fornito per creare la richiesta API per la creazione di un mixin](../api/mixins.md#create) o [creazione di un tipo di dati](../api/data-types.md#create).[

<table>
  <tr>
    <th>Tipo desiderato<br/>(meta:xdmType)</th>
    <th>JSON<br/>(schema JSON)</th>
    <th>Esempio di codice</th>
  </tr>
  <tr>
    <td>string</td>
    <td>type: string<br/><br/><strong>Proprietà facoltative:</strong><br/>
      <ul>
        <li>pattern</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
            "type": "string",
            "pattern": "^[A-Z]{2}$",
            "maxLength": 2
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type: formato stringa<br/>: uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "uri"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: string)</td>
    <td>type: string<br/><br/><strong>Proprietà facoltativa:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>Specificate le etichette delle opzioni rivolte al cliente utilizzando "meta:enum":
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
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>numero</td>
    <td>type: numero<br/>minimo: ±2,23×10^308<br/>massimo: ±1,80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "number"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>type: integer<br/>massimo:2^53+1<br>minimo:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimo": -9007199254740992,
          "massima": 9007199254740992
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type: integer<br/>massimo:2^31<br>minimo:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimo": -2147483648,
          "massima": 2147483648
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>type: integer<br/>massimo:2^15<br>minimo:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimo": -32768,
          "massima": 32768
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type: integer<br/>massimo:2^7<br>minimo:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimo": -128,
          "massima": 128
          }
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
        "sampleField": {
          "type": "boolean",
          "default": false
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>data</td>
    <td>type: formato stringa<br/>: date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "date",
          "esempi": ["2004-10-23"]
        }
      </pre>
      Data come definita da <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, sezione 5.6</a>, dove "data completa" = data-anno intero "-" data-mese "-" data-giorno (AAAA-MM-GG)
    </td>
  </tr>
  <tr>
    <td>data-ora</td>
    <td>type: formato stringa<br/>: data-ora</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "data-ora",
          "esempi": ["2004-10-23T12:00:00-06:00"]
        }
      </pre>
      Data-ora come definita da <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, sezione 5.6</a>, dove "date-time" = data-ora completa "T" a tempo pieno:<br/>(AAAA-MM-GG'T'HH:MM:SS.SSSSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>type: array</td>
    <td>items.type può essere definito utilizzando qualsiasi tipo scalare:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      </pre>
      Array di oggetti definiti da un altro schema:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "items": {
            "$ref": "id"
          }
        }
      </pre>
      Dove "id" è il {id} dello schema di riferimento.
    </td>
  </tr>
  <tr>
    <td>object</td>
    <td>type: object</td>
    <td>proprietà.{field}.type può essere definito utilizzando qualsiasi tipo scalare:
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
        }
      </pre>
      Campo di tipo "oggetto" definito da uno schema di riferimento:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "$ref": "id"
        }
      </pre>
      Dove "id" è il {id} dello schema di riferimento.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>type: oggetto<br/><br/><strong>Nota:</strong><br/>L'utilizzo del tipo di dati 'map' è riservato all'utilizzo dello schema del settore e del fornitore e non è disponibile per l'uso nei campi definiti dal tenant. Viene utilizzato negli schemi standard quando i dati sono rappresentati come chiavi che corrispondono a un certo valore, o quando le chiavi non possono essere incluse in uno schema statico e devono essere trattate come valori di dati.</td>
    <td>UNA 'mappa' NON DEVE definire alcuna proprietà. DEVE definire un singolo schema "[!UICONTROL AdditionalProperties]" per descrivere il tipo di valori contenuti nella 'map'. Una 'mappa' in XDM può contenere un solo tipo di dati. I valori possono essere una qualsiasi definizione di schema XDM valida, inclusa una matrice o un oggetto, o come riferimento a un altro schema (tramite $ref).<br/><br/>Campo mappa con valori di tipo 'stringa':
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "AdditionalProperties":{
            "type": "string"
          }
        }
      </pre>
    Mappa campo con valori che costituiscono un array di stringhe:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "AdditionalProperties":{
            "type": "array",
            "items": {
              "type": "string"
            }
          }
        }
      </pre>
    Campo mappa che fa riferimento a un altro schema:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "AdditionalProperties":{
            "$ref": "id"
          }
        }
      </pre>
      Dove "id" è il {id} dello schema di riferimento.
    </td>
  </tr>
</table>
