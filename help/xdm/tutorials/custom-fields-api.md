---
title: Definire i campi XDM nell’API del Registro di sistema dello schema
description: Scopri come definire campi diversi durante la creazione di risorse personalizzate Experience Data Model (XDM) nell’API del Registro di sistema dello schema.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 536657f11a50ea493736296780dd57f41dfefeae
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Definire i campi XDM nell’API del Registro di sistema dello schema

Tutti i campi Experience Data Model (XDM) sono definiti utilizzando lo standard [Schema JSON](https://json-schema.org/) vincoli applicabili al tipo di campo, con vincoli aggiuntivi per i nomi di campo applicati da Adobe Experience Platform. L’API del Registro di sistema dello schema consente di definire campi personalizzati negli schemi mediante l’uso di formati e vincoli facoltativi. I tipi di campo XDM sono esposti dall’attributo a livello di campo, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` è un valore generato dal sistema e pertanto non è necessario aggiungere questa proprietà al JSON per il campo quando si utilizza l’API (tranne quando [creazione di tipi di mappa personalizzati](#maps)). Si consiglia di utilizzare i tipi di schema JSON (ad esempio `string` e `integer`) con i vincoli minimi/massimi appropriati, come definito nella tabella seguente.

La tabella seguente delinea la formattazione appropriata per definire diversi tipi di campi, compresi quelli con proprietà facoltative. Ulteriori informazioni sulle proprietà facoltative e sulle parole chiave specifiche per tipo sono disponibili tramite [Documentazione dello schema JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Per iniziare, trova il tipo di campo desiderato e utilizza il codice di esempio fornito per generare la richiesta API per [creazione di un gruppo di campi](../api/field-groups.md#create) o [creazione di un tipo di dati](../api/data-types.md#create).

<table style="table-layout:auto">
  <tr>
    <th>Tipo XDM</th>
    <th>Optional properties</th>
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
    <td>An array of basic scalar types (e.g. strings):
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "array",
  "items": {
    "type": "string"
  }
}</pre>
      An array of objects defined by another schema:<br/>
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
    <td>Un campo di tipo mappa è essenzialmente un campo di tipo oggetto con un set di chiavi non vincolato. Like objects, maps have a <code>type</code> value of <code>object</code>, but their <code>meta:xdmType</code> is explicitly set to <code>map</code>.<br><br>Una mappa <strong>non deve</strong> definire le proprietà. It <strong>deve</strong> definire un singolo <code>additionalProperties</code> schema per descrivere il tipo di valori contenuti nella mappa (ogni mappa può contenere un solo tipo di dati). The <code>type</code> value must be either <code>string</code> or <code>integer</code>.<br/><br/>A map field with string-type values:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "meta:xdmType": "map", "additionalProperties":{ "type": "string" } }</pre>
    Per ulteriori informazioni sulla creazione di tipi di mappa personalizzati in XDM, consulta la sezione seguente.
    </td>
  </tr>
</table>

## Creazione di tipi di mappa personalizzati {#maps}

Per supportare in modo efficiente i dati &quot;simili a mappe&quot; in XDM, gli oggetti possono essere annotati con un `meta:xdmType` impostato su `map` per chiarire che un oggetto deve essere gestito come se il set di chiavi non fosse vincolato. I dati acquisiti nei campi mappa devono utilizzare le chiavi stringa e solo i valori stringa o interi (come determinato da `additionalProperties.type`).

XDM pone le seguenti restrizioni all&#39;utilizzo di questo hint di archiviazione:

* I tipi di mappa DEVONO essere di tipo `object`.
* I tipi di mappa NON DEVONO avere proprietà definite (in altre parole, definiscono oggetti &quot;vuoti&quot;).
* I tipi di mappa DEVONO includere `additionalProperties.type` campo che descrive i valori che possono essere inseriti all&#39;interno della mappa, `string` o `integer`.

Assicurati di utilizzare i campi di tipo mappa solo quando è assolutamente necessario, in quanto presentano i seguenti svantaggi prestazionali:

* Il tempo di risposta da Adobe Experience Platform Query Service degrada da tre secondi a dieci secondi per 100 milioni di record.
* Le mappe devono avere meno di 16 chiavi, altrimenti rischiano un ulteriore deterioramento.

L’interfaccia utente di Platform presenta inoltre delle limitazioni nell’estrazione delle chiavi dei campi di tipo mappa. Mentre i campi di tipo oggetto possono essere espansi, le mappe vengono visualizzate come un singolo campo.

## Passaggi successivi

Questa guida illustra come definire diversi tipi di campi nell’API. Per ulteriori informazioni sulla formattazione dei tipi di campo XDM, consulta la guida [Vincoli del tipo di campo XDM](../schema/field-constraints.md).
