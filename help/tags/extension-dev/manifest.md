---
title: Manifesto dell’estensione
description: Scopri come configurare un file manifest JSON che informi Adobe Experience Platform su come utilizzare correttamente l’estensione.
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '2645'
ht-degree: 99%

---

# Manifesto dell’estensione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Nella directory di base dell’estensione è necessario creare un file denominato `extension.json`. Contiene informazioni critiche sull’estensione che consentono a Adobe Experience Platform di utilizzarla correttamente. Alcuni contenuti sono creati secondo le regole [npm per `package.json`](https://docs.npmjs.com/files/package.json).

Un esempio di `extension.json` è disponibile nell’archivio GitHub dell’[estensione Hello World](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json).

Un manifesto dell’estensione deve essere costituito dai seguenti elementi:

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome dell’estensione. Deve essere univoco rispetto a tutte le altre estensioni e deve essere conforme alle [regole relative alla denominazione](#naming-rules). **Viene usato dai tag come identificatore e non deve essere modificato dopo la pubblicazione dell’estensione.** |
| `platform` | Piattaforma per l’estensione. Al momento l’unico valore accettato è `web`. |
| `version` | Versione dell’estensione. Deve seguire il formato di controllo delle versioni [semver](https://semver.org/). È conforme al [campo npm version](https://docs.npmjs.com/files/package.json#version). |
| `displayName` | Nome leggibile dell’estensione. Verrà mostrato agli utenti di Platform. Non è necessario indicare “tag” o “Estensione”; gli utenti sapranno già che si tratta di un’estensione tag. |
| `description` | Descrizione dell’estensione. Verrà mostrato agli utenti di Platform. Se l’estensione consente agli utenti di implementare il prodotto sul loro sito web, descrivi le funzioni del prodotto. Non è necessario indicare “tag” o “Estensione”; gli utenti sapranno già che si tratta di un’estensione tag. |
| `iconPath` *(Facoltativo)* | Percorso relativo per l’icona che verrà visualizzata per l’estensione. Non può iniziare con una barra. Deve fare riferimento a un file SVG con estensione `.svg`. Il file SVG deve essere quadrato e può essere ridimensionato da Platform. |
| `author` | L’oggetto “author” deve essere strutturato nel modo seguente: <ul><li>`name`: nome dell’autore dell’estensione. In alternativa, qui è possibile utilizzare il nome della società.</li><li>`url` *(facoltativo)*: URL in cui si possono trovare ulteriori informazioni sull’autore dell’estensione.</li><li>`email` *(facoltativo)*: indirizzo e-mail dell’autore dell’estensione.</li></ul>È conforme alle regole [npm per il campo author](https://docs.npmjs.com/files/package.json#people-fields-author-contributors). |
| `exchangeUrl` *(richiesto per le estensioni pubbliche)* | URL dell’inserzione relativa all’estensione su Adobe Exchange. Deve corrispondere al pattern `https://www.adobeexchange.com/experiencecloud.details.######.html`. |
| `viewBasePath` | Percorso relativo della sottodirectory contenente tutte le viste e le relative risorse (HTML, JavaScript, CSS, immagini). Platform ospita su un server web questa directory, da cui carica i contenuti iframe. Questo campo è obbligatorio e non deve iniziare con una barra. Ad esempio, se tutte le viste sono contenute in `src/view/`, il valore di `viewBasePath` sarà `src/view/`. |
| `hostedLibFiles` *(Facoltativo)* | Molti dei nostri utenti preferiscono ospitare tutti i file relativi ai tag sul proprio server. Questo offre agli utenti una maggiore certezza sulla disponibilità dei file in fase di esecuzione e consente loro di analizzare facilmente il codice per individuare eventuali vulnerabilità di sicurezza. Se la porzione libreria dell’estensione deve caricare dei file JavaScript in fase di esecuzione, è consigliabile elencare tali file mediante questa proprietà. I file elencati saranno ospitati insieme alla libreria runtime dei tag. L’estensione può quindi caricare i file tramite un URL recuperato utilizzando il metodo [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file).<br><br>Questa opzione contiene un array con i percorsi relativi dei file libreria di terze parti che devono essere ospitati. |
| `main` *(Facoltativo)* | Percorso relativo di un modulo libreria da eseguire in fase runtime.<br><br>Questo modulo sarà sempre incluso nella libreria runtime ed eseguito. Poiché il modulo verrà sempre incluso nella libreria runtime, si consiglia di utilizzare un modulo “main” solo se è assolutamente necessario e di mantenerne minima la dimensione del codice.<br><br>Non è garantito che questo modulo sia eseguito per primo; è possibile che altri moduli vengano eseguiti prima di esso. |
| `configuration` *(Facoltativo)* | Descrive la porzione di [configurazione](./configuration.md) dell’estensione. Questa proprietà è necessaria se gli utenti dovranno fornire le impostazioni globali per l’estensione. Per informazioni dettagliate sulla struttura del campo, consulta l’[appendice](#config-object). |
| `events` *(Facoltativo)* | Array delle definizioni dei tipi di [evento](./web/event-types.md). Per informazioni sulla struttura di ciascun oggetto presente nell’array, consulta la sezione dell’appendice sulle [definizioni dei tipi](#type-definitions). |
| `conditions` *(Facoltativo)* | Array delle definizioni dei tipi di [condizione](./web/condition-types.md). Per informazioni sulla struttura di ciascun oggetto presente nell’array, consulta la sezione dell’appendice sulle [definizioni dei tipi](#type-definitions). |
| `actions` *(Facoltativo)* | Array delle definizioni dei tipi di [azione](./web/action-types.md). Per informazioni sulla struttura di ciascun oggetto presente nell’array, consulta la sezione dell’appendice sulle [definizioni dei tipi](#type-definitions). |
| `dataElements` *(Facoltativo)* | Array delle definizioni dei tipi di [elemento dati](./web/data-element-types.md). Per informazioni sulla struttura di ciascun oggetto presente nell’array, consulta la sezione dell’appendice sulle [definizioni dei tipi](#type-definitions). |
| `sharedModules` *(Facoltativo)* | Array degli oggetti di definizione dei moduli condivisi. Ciascun oggetto di modulo condiviso presente nell’array deve essere strutturato nel modo seguente: <ul><li>`name`: nome del modulo condiviso. Questo nome verrà utilizzato quando si fa riferimento a moduli condivisi da altre estensioni, come descritto in [Moduli condivisi](./web/shared.md). Questo nome non viene mai visualizzato in alcuna area dell’interfaccia utente. Deve essere univoco rispetto ai nomi di altri moduli condivisi all’interno dell’estensione e deve essere conforme alle [regole di denominazione](#naming-rules). **Viene usato dai tag come identificatore e non deve essere modificato dopo la pubblicazione dell’estensione.**</li><li>`libPath`: percorso relativo del modulo condiviso. Non può iniziare con una barra. Deve fare riferimento a un file JavaScript con estensione `.js`.</li></ul> |

## Appendice

### Regole di denominazione {#naming-rules}

Il valore di qualsiasi campo `name` all’interno di `extension.json` deve essere conforme alle regole seguenti:

* Può contenere un massimo 214 caratteri.
* Non deve iniziare con un punto o un carattere di sottolineatura.
* Non deve contenere lettere maiuscole.
* Deve contenere solo caratteri sicuri per gli URL.

Queste regole sono conformi alle regole [npm per il nome del pacchetto](https://docs.npmjs.com/files/package.json#name).

### Proprietà dell’oggetto di configurazione {#config-object}

L’oggetto di configurazione deve essere strutturato nel modo seguente:

<table>
  <thead>
    <tr>
      <th>Proprietà</th>
      <th>Descrizione</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>viewPath</code></td>
      <td>URL relativo della vista di configurazione dell’estensione. Deve essere relativo a <code>viewBasePath</code> e non deve iniziare con una barra. Deve fare riferimento a un file HTML con estensione <code>.html</code>. È possibile utilizzare suffissi per stringhe di query e identificatori di frammento (hash).</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Oggetto dello <a href="https://json-schema.org/">schema JSON</a> che descrive il formato di un oggetto valido salvato dalla vista di configurazione dell’estensione. In quanto sviluppatore della vista di configurazione, devi assicurarti che tutti gli oggetti impostazioni salvati siano conformi a questo schema. Questo schema verrà utilizzato anche per la convalida quando gli utenti tenteranno di salvare i dati tramite i servizi di Platform <br><br>Esempio di un oggetto schema:
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      È consigliabile utilizzare uno strumento come <a href="https://www.jsonschemavalidator.net/">JSON Schema validator</a> per verificare manualmente lo schema.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Facoltativo)</em></td>
      <td>Array di oggetti in cui ogni oggetto rappresenta una trasformazione da eseguire su ogni oggetto impostazioni corrispondente quando viene emesso nella libreria runtime. Per ulteriori informazioni sulle ragioni e le modalità di utilizzo di questa proprietà, consulta la sezione relativa alle <a href="#transforms">trasformazioni</a>.</td>
    </tr>
  </tbody>
</table>

### Definizioni dei tipi {#type-definitions}

La definizione di un tipo è un oggetto utilizzato per descrivere un tipo di evento, di condizione, di azione o di elemento dati. L’oggetto è costituito dai seguenti elementi:

<table>
  <thead>
    <tr>
      <th>Proprietà</th>
      <th>Descrizione</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>Nome del tipo. Deve essere un nome univoco all’interno dell’estensione. Il nome deve essere conforme alle <a href="#naming-rules">regole di denominazione</a>. <strong>Viene usato dai tag come identificatore e non deve essere modificato dopo la pubblicazione dell’estensione.</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>Testo che verrà utilizzato per rappresentare il tipo nell’interfaccia utente di Data Collection. Deve essere leggibile.</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(Facoltativo)</em></td>
      <td>Se fornito, il <code>displayName</code> verrà elencato in <code>categoryName</code> nell’interfaccia utente di Tutti i tipi con lo stesso <code>categoryName</code> saranno elencati nella stessa categoria. Ad esempio, se l’estensione ha fornito un tipo di evento <code>keyUp</code> e un tipo di evento <code>keyDown</code>, entrambi con <code>categoryName</code> impostato su <code>Keyboard</code>, entrambi i tipi di evento sono elencati nella categoria Keyboard quando l’utente seleziona una voce dall’elenco dei tipi di evento disponibili per creare una regola. Il valore di <code>categoryName</code> deve essere leggibile.</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>Percorso relativo del modulo libreria del tipo. Non può iniziare con una barra. Deve fare riferimento a un file JavaScript con estensione <code>.js</code>.</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(Facoltativo)</em></td>
      <td>URL relativo per la vista del tipo. Deve essere relativo a <code>viewBasePath</code> e non deve iniziare con una barra. Deve fare riferimento a un file HTML con estensione <code>.html</code>. È possibile utilizzare identificatori di stringhe di query e frammenti (hash). Se il modulo libreria del tipo non utilizza impostazioni configurate da un utente, è possibile escludere questa proprietà e Platform al suo posto mostrerà un segnaposto che informa che non è necessaria alcuna configurazione.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Oggetto con <a href="https://json-schema.org/">schema JSON</a> che descrive il formato di un oggetto impostazioni valido che può essere salvato dall’utente. Le impostazioni vengono generalmente configurate e salvate da un utente che utilizza l’interfaccia di Data Collection. In questi casi, la vista dell’estensione può eseguire i passaggi necessari per convalidare le impostazioni fornite dall’utente. Alcuni utenti preferiscono invece utilizzare direttamente le API dei tag senza l’ausilio di alcuna interfaccia utente. Lo scopo di questo schema è consentire a Platform di convalidare correttamente che gli oggetti impostazioni salvati dagli utenti siano in un formato compatibile con il modulo libreria che agirà in base all’oggetto impostazioni stesso in fase di esecuzione, indipendentemente dall’utilizzo o meno di un'interfaccia utente.<br><br>Esempio di oggetto schema:<br>
<pre class="JSON language-JSON hljs">
{ "$schema": "http://json-schema.org/draft-04/schema#", "type": "object", "properties": { "delay": { "type": "number", "minimum": 1 } }, "required": [ "delay" ], "additionalProperties": false }
</pre>
      È consigliabile utilizzare uno strumento come <a href="https://www.jsonschemavalidator.net/">JSON Schema validator</a> per verificare manualmente lo schema.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Facoltativo)</em></td>
      <td>Array di oggetti in cui ogni oggetto rappresenta una trasformazione da eseguire su ogni oggetto impostazioni corrispondente quando viene emesso nella libreria runtime. Per ulteriori informazioni sulle ragioni e sulle modalità di utilizzo, consulta la sezione relativa alle <a href="#transforms">trasformazioni</a>.</td>
    </tr>
  </tbody>
</table>

### Trasformazioni {#transforms}

Per alcuni casi d’uso specifici, le estensioni richiedono che gli oggetti impostazioni salvati da una vista siano trasformati da Platform prima che vengano emessi nella relativa libreria runtime dei tag. È possibile richiedere che una o più di queste trasformazioni siano effettuate impostando la proprietà `transforms` quando si imposta la definizione di un tipo all’interno di `extension.json`. La proprietà `transforms` è un array di oggetti in cui ogni oggetto rappresenta una trasformazione che deve essere eseguita.

Tutte le trasformazioni richiedono `type` e `propertyPath`. Il valore di `type` può essere `function`, `remove` o `file` e descrive il tipo di trasformazione che verrà applicata da Platform all’oggetto impostazioni. Il valore di `propertyPath` è una stringa delimitata da punti che indica ai tag dove trovare la proprietà da modificate all’interno dell’oggetto impostazioni. Di seguito è riportato un oggetto impostazioni di esempio e alcuni `propertyPath`:

```js
{
  foo: {
    bar: "A string",
    baz: [
      "A",
      "B",
      "C"
    ]
  }
}
```

* Se imposti `propertyPath` su `foo.bar`, verrà trasformato il valore `"A string"`.
* Se imposti `propertyPath` su `foo.baz[]`, verrà trasformato ciascun valore presente nell’array `baz`.
* Impostando `propertyPath` su `foo.baz` si trasforma l’array `baz`.

I percorsi delle proprietà possono utilizzare qualsiasi combinazione di array e notazione di oggetto per applicare trasformazioni dell’oggetto impostazioni a qualsiasi livello.

>[!WARNING]
>
>L’utilizzo della notazione dell’array nell’attributo `propertyPath` (ad esempio `foo.baz[]`) non è ancora supportato nello strumento sandbox dell’estensione.

Le sezioni seguenti descrivono le trasformazioni disponibili e come utilizzarle.

#### Trasformazione tramite funzione

La trasformazione tramite funzione consente di eseguire il codice scritto dagli utenti di Platform tramite un modulo libreria all’interno della libreria runtime di tag emessa.

Supponiamo di voler fornire un tipo di azione “script personalizzato”. La visualizzazione dell’azione “script personalizzato” potrebbe fornire un’area di testo in cui l’utente potrà immettere il codice. Supponiamo che un utente abbia immesso il seguente codice nell’area di testo:

`console.log('Welcome, ' + username +'. This is ZomboCom.');`

Quando l’utente salva la regola, l’oggetto impostazioni salvato dalla vista potrebbe essere simile al seguente:

```javascript
{
  foo: {
    bar: "console.log('Welcome, ' + username +'. This is ZomboCom.');"
  }
}
```

Quando una regola che utilizza questa azione viene attivata nella libreria runtime dei tag, dovrà essere eseguito il codice dell’utente per trasmettervi un nome utente.

Quando l’oggetto impostazioni viene salvato dalla vista del tipo di azione, il codice dell’utente è semplicemente una stringa. Questo va bene perché può essere correttamente serializzato da e verso JSON; tuttavia, si tratta anche di un problema perché generalmente viene emesso nella libreria runtime dei tag anche come una stringa, anziché come una funzione eseguibile. Anche se è possibile tentare di eseguire il codice all’interno del modulo libreria del tipo di azione utilizzando [`eval`](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/eval) o un [costruttore di funzione](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Function), è altamente sconsigliato a causa di [criteri per la sicurezza dei contenuti](https://developer.mozilla.org/en-US/docs/Web/Security/CSP) che potrebbero bloccare l’esecuzione.

Per ovviare a questa situazione, l’utilizzo della trasformazione tramite funzione indica a Platform di racchiudere il codice dell’utente in una funzione eseguibile quando viene emesso nella libreria runtime dei tag. Per risolvere il problema di questo esempio, definiamo la trasformazione sulla definizione del tipo in `extension.json` nel modo seguente:

```json
{
  "transforms": [
    {
      "type": "function",
      "propertyPath": "foo.bar",
      "parameters": ["username"]
    }
  ]
}
```

* `type` definisce il tipo di trasformazione da applicare all’oggetto impostazioni.
* `propertyPath` è una stringa delimitata da punti che indica a Platform dove trovare la proprietà da modificare all’interno dell’oggetto delle impostazioni.
* `parameters` è un array di nomi dei parametri da includere nella firma della funzione di wrapping.

Quando l’oggetto impostazioni viene emesso nella libreria runtime dei tag, verrà trasformato nel modo seguente:

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

Il modulo libreria può quindi richiamare la funzione contenente il codice dell’utente e trasmetterlo nell’argomento `username`.

#### Trasformazione tramite file

La trasformazione tramite file consente di emettere il codice scritto dagli utenti di Platform in un file separato dalla libreria runtime dei tag. Il file sarà ospitato accanto alla libreria runtime dei tag e, se necessario, può essere caricato dall’estensione in fase di esecuzione.

Supponiamo di voler fornire un tipo di azione “script personalizzato”. La visualizzazione del tipo di azione potrebbe fornire un’area di testo in cui l’utente può immettere alcuni codici. Supponiamo che un utente abbia immesso il seguente codice nell’area di testo:

`console.log('This is ZomboCom.');`

Quando l’utente salva la regola, l’oggetto impostazioni salvato dalla vista potrebbe essere simile al seguente:

```js
{
  foo: {
    bar: "console.log('This is ZomboCom.');"
  }
}
```

Il codice dell’utente dovrebbe essere inserito in un file separato, invece di essere incluso nella libreria runtime dei tag. Quando una regola che utilizza la nostra azione viene attivata nella libreria runtime dei tag, il codice dell’utente dovrà essere caricato aggiungendo un elemento script al corpo del documento. Per risolvere il problema di questo esempio, definiamo la trasformazione nella definizione del tipo di azione in `extension.json` nel modo seguente:

```json
{
  "transforms": [
    {
      "type": "file",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` definisce il tipo di trasformazione da applicare all’oggetto impostazioni.
* `propertyPath` è una stringa delimitata da punti che indica a Platform dove trovare la proprietà da modificare all’interno dell’oggetto delle impostazioni.

Quando l’oggetto impostazioni viene emesso nella libreria runtime dei tag, verrà trasformato nel modo seguente:

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

In questo caso, il valore di `foo.bar` è stato trasformato in un URL. L’URL esatto verrà determinato al momento della creazione della libreria. Il file riceverà sempre l’estensione `.js` e verrà distribuito utilizzando un tipo MIME orientato a JavaScript. In futuro potrebbe venir aggiunto il supporto di altri tipi MIME.

#### Trasformazione di rimozione

Per impostazione predefinita, tutte le proprietà dell’oggetto impostazioni sono emesse nella libreria runtime dei tag. Se alcune proprietà vengono utilizzate solo per la vista delle estensioni, in particolare se contengono informazioni riservate (ad esempio un token segreto), è necessario usare la trasformazione di rimozione per impedire che le informazioni vengano emesse nella libreria runtime dei tag.

Supponiamo di voler fornire un nuovo tipo di azione. La vista del tipo di azione potrebbe fornire un campo di input in cui l’utente può immettere una chiave segreta che consentirà la connessione a una API specifica. Supponiamo che un utente abbia immesso il testo seguente:

`ABCDEFG`

Quando l’utente salva la regola, l’oggetto impostazioni salvato dalla vista potrebbe essere simile al seguente:

```js
{
  foo: {
    bar: "ABCDEFG"
  }
}
```

La proprietà `bar` non dovrebbe essere inclusa nella libreria runtime dei tag. Per risolvere il problema di questo esempio, definiamo la trasformazione nella definizione del tipo di azione in `extension.json` nel modo seguente:

```json
{
  "transforms": [
    {
      "type": "remove",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` definisce il tipo di trasformazione da applicare all’oggetto impostazioni.
* `propertyPath` è una stringa delimitata da punti che indica a Platform dove trovare la proprietà da modificare all’interno dell’oggetto delle impostazioni.

Quando l’oggetto impostazioni viene emesso nella libreria runtime dei tag, verrà trasformato nel modo seguente:

```js
{
  foo: {
  }
}
```

In questo caso, il valore `foo.bar` è stato rimosso dall’oggetto delle impostazioni.
