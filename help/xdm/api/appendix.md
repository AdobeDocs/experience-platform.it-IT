---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Appendice sviluppatore del Registro di sistema dello schema
topic: developer guide
translation-type: tm+mt
source-git-commit: f7c87cc86bfc5017ec5c712d05e39be5c14a7147

---


# Appendice

Questo documento fornisce informazioni supplementari relative all&#39;utilizzo dell&#39;API del Registro di sistema dello schema.

## Modalità compatibilità

Experience Data Model (XDM) è una specifica documentata pubblicamente, spinta da Adobe per migliorare l&#39;interoperabilità, l&#39;espressività e il potere delle esperienze digitali. Adobe mantiene il codice sorgente e le definizioni XDM formali in un progetto [open source su GitHub](https://github.com/adobe/xdm/). Queste definizioni sono scritte in Notazione standard XDM, utilizzando la Notazione oggetto JSON-LD (JavaScript Object Notation for Linked Data) e lo schema JSON come grammatica per la definizione degli schemi XDM.

Quando si esaminano le definizioni XDM formali nell&#39;archivio pubblico, è possibile notare che lo standard XDM è diverso da quello visualizzato in Adobe Experience Platform. Ciò che vedete in Experience Platform è denominata Modalità compatibilità e fornisce una semplice mappatura tra XDM standard e il modo in cui viene utilizzato all&#39;interno della piattaforma.

### Funzionamento della modalità di compatibilità

La modalità di compatibilità consente al modello XDM JSON-LD di funzionare con l&#39;infrastruttura dati esistente modificando i valori all&#39;interno di XDM standard mantenendo la stessa semantica. Utilizza una struttura JSON nidificata, mostrando gli schemi in un formato simile a un albero.

La differenza principale che noterete tra XDM standard e Modalità compatibilità è la rimozione del prefisso &quot;xdm:&quot; per i nomi dei campi.

Di seguito è riportato un confronto affiancato che mostra i campi relativi al compleanno (con gli attributi &quot;description&quot; rimossi) sia in XDM standard che in Modalità compatibilità. I campi Modalità compatibilità includono un riferimento al campo XDM e al relativo tipo di dati negli attributi &quot;meta:xdmField&quot; e &quot;meta:xdmType&quot;.

<table>
  <th>XDM standard</th>
  <th>Modalità compatibilità</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:bornDate": { "title": "Data di nascita", "tipo": "string", "format": "date", }, "xdm:bornDayAndMonth": { "title": "Data di nascita", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear": { "title": "Anno di nascita", "tipo": "integer", "Minimum": 1, "massimo": 32767 }
      </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "bornDate": { "title": "Data di nascita", "tipo": "string", "format": "date", "meta:xdmField": "xdm:BirDate", "meta:xdmType": "date" }, "bornDayAndMonth": { "title": "Data di nascita", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:bornDayAndMonth", "meta:xdmType": "string" }, "bornYear": { "title": "Anno di nascita", "tipo": "integer", "Minimum": 1, "massimo": 32767, "meta:xdmField": "xdm:bornYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### Perché è necessaria la modalità di compatibilità?

Adobe Experience Platform è progettato per lavorare con più soluzioni e servizi, ognuno con le proprie problematiche e limitazioni tecniche (ad esempio, il modo in cui determinate tecnologie gestiscono caratteri speciali). Per superare questi limiti, è stata sviluppata la Modalità di compatibilità.

La maggior parte dei servizi Experience Platform, tra cui Catalog, Data Lake e Real-time Customer Profile, utilizza la modalità di compatibilità al posto di XDM standard. Anche l&#39;API del Registro di sistema dello schema utilizza la modalità di compatibilità e gli esempi in questo documento vengono visualizzati utilizzando la modalità di compatibilità.

Vale la pena sapere che una mappatura viene eseguita tra XDM standard e il modo in cui viene gestita in Experience Platform, ma non deve influenzare l&#39;utilizzo dei servizi della piattaforma.

Il progetto open source è disponibile, ma quando si tratta di interagire con le risorse attraverso il Registro di sistema dello schema, gli esempi di API in questo documento forniscono le procedure ottimali che si dovrebbero conoscere e seguire.

## Definizione dei tipi di campo XDM nell&#39;API {#field-types}

Gli schemi XDM sono definiti utilizzando gli standard dello schema JSON e i tipi di campo di base, con vincoli aggiuntivi per i nomi di campo applicati da Experience Platform. XDM consente di definire ulteriori tipi di campi mediante l&#39;uso di formati e vincoli facoltativi. I tipi di campo XDM sono esposti dall&#39;attributo a livello di campo `meta:xdmType`.

>[!NOTE] è `meta:xdmType` un valore generato dal sistema e pertanto non è necessario aggiungere questa proprietà al JSON per il campo. Come procedura ottimale si consiglia di utilizzare tipi di schema JSON (come stringa e numero intero) con i vincoli min/max appropriati, come definito nella tabella seguente.

La tabella seguente delinea la formattazione appropriata per definire i tipi di campi scalari e i tipi di campi più specifici utilizzando le proprietà facoltative. Ulteriori informazioni sulle proprietà facoltative e sulle parole chiave specifiche per i tipi sono disponibili nella documentazione [sullo schema](https://json-schema.org/understanding-json-schema/reference/type.html)JSON.

Per iniziare, trovate il tipo di campo desiderato e utilizzate il codice di esempio fornito per creare la richiesta API.

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
    <td>number</td>
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
    <td>date</td>
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
    <td>UNA 'mappa' NON DEVE definire alcuna proprietà. DEVE definire un singolo schema "AdditionalProperties" per descrivere il tipo di valori contenuti nella 'map'. Una 'mappa' in XDM può contenere un solo tipo di dati. I valori possono essere una qualsiasi definizione di schema XDM valida, inclusa una matrice o un oggetto, o come riferimento a un altro schema (tramite $ref).<br/><br/>Campo mappa con valori di tipo 'stringa':
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


## Mappatura di tipi XDM ad altri formati

La tabella seguente descrive la mappatura tra &quot;meta:xdmType&quot; e altri formati di serializzazione.

| XDM Type<br>(meta:xdmType) | JSON<br>(Schema JSON) | Parquet<br>(tipo/annotazione) | SQL Spark | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Stringa | System.String | Stringa | string | Stringa | string |
| number | type:number | DOPPIO | DoubleType | java.lang.Double | Doppio | System.Double | Numero | double | Doppio | double |
| long | tipo:<br>numero intero massimo:2^53+1<br>minimo:-2^53+1 | INT64 | LongType | java.lang.Long | Long | System.Int64 | Numero | long | Intero | int64 |
| int | tipo:<br>numero intero massimo:2^31<br>minimo:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Numero | int | Intero | int32 |
| short | tipo:<br>numero intero massimo:2^15<br>minimo:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Breve | System.Int16 | Numero | int | Intero | int32 |
| byte | tipo:<br>numero intero massimo:2^7<br>minimo:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Numero | int | Intero | int32 |
| booleano | type:boolean | BOOLEANO | BooleanType | java.lang.Boolean | Booleano | System.Boolean | Booleano | boe | Intero | Intero | boe |
| date | type:<br>stringformat:date<br>(RFC 3339, sezione 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Stringa | date | Integer<br>(unix millis) | int64<br>(unix millis) |
| data-ora | type:<br>stringformat:date-time<br>(RFC 3339, sezione 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Stringa | timestamp | Integer<br>(unix millis) | int64<br>(unix millis) |
| map | object | MAP annotated group<br><br>&lt;<span>key_type</span>> DEVE essere STRING<br><br>&lt;<span>value_type</span>> tipo di valori mappa | MapType<br><br>&quot;keyType&quot; DEVE essere StringType<br><br>&quot;valueType&quot; è il tipo di valori della mappa. | java.util.Map | Mappa | --- | object | object | map | map&lt;<span>key_type, value_type</span>> |
