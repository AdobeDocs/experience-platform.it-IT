---
title: Riferimento oggetto satellite
description: Scopri l’oggetto _satellite lato client e le varie funzioni che consente di eseguire con esso nei tag.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 79%

---

# Documentazione per gli oggetti Satellite

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Questo documento funge da riferimento per l’oggetto `_satellite` lato client e le varie funzioni che è possibile eseguire con esso.

## `track`

**Codice**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**Esempio**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` attiva tutte le regole utilizzando il tipo di evento Direct Call configurato con l’identificatore specificato dall’estensione tag Core. L&#39;esempio precedente attiva tutte le regole utilizzando un tipo di evento Call Direct in cui l&#39;identificativo configurato è `contact_submit`. Inoltre, viene trasmesso un oggetto facoltativo contenente le relative informazioni. L&#39;oggetto dettaglio è accessibile immettendo `%event.detail%` all&#39;interno di un campo di testo in una condizione o in un&#39;azione oppure `event.detail` all&#39;interno dell&#39;editor di codice in una condizione o in un&#39;azione di codice personalizzato.

## `getVar`

**Codice**

```javascript
_satellite.getVar(name: string) => *
```

**Esempio**

```javascript
var product = _satellite.getVar('product');
```

Nell’esempio fornito, se esiste un elemento dati con un nome corrispondente, verrà restituito il suo valore. Se non esiste alcun elemento di dati corrispondente, eseguirà una verifica per vedere se in precedenza è stata impostata una variabile personalizzata con un nome corrispondente utilizzando `_satellite.setVar()`. Se si trova una variabile personalizzata corrispondente, verrà restituito il relativo valore.

>[!NOTE]
>
>È possibile utilizzare la percentuale (`%`) per fare riferimento alle variabili per molti campi del modulo nell’implementazione del tag, riducendo la necessità di chiamare `_satellite.getVar()`. Ad esempio, utilizzando `%product%` accederà al valore dell’elemento dati del prodotto o della variabile personalizzata.

Quando un evento attiva una regola, puoi trasmettere la regola corrispondente `event` oggetto in `_satellite.getVar()` così:

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

## `setVar`

**Codice**

```javascript
_satellite.setVar(name: string, value: *)
```

**Esempio**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` imposta una variabile personalizzata con un nome e un valore specifici. In seguito è possibile accedere al valore della variabile utilizzando `_satellite.getVar()`.

Se lo desideri, puoi impostare più variabili contemporaneamente trasmettendo un oggetto in cui le chiavi sono nomi di variabili e i valori sono i rispettivi valori delle variabili.

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**Codice**

```javascript
_satellite.getVisitorId() => Object
```

**Esempio**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

Se l&#39;estensione [!DNL Adobe Experience Cloud ID] è installata nella proprietà, questo metodo restituisce l&#39;istanza ID visitatore. Per ulteriori informazioni, consulta la [documentazione del servizio Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).

## `logger`

**Codice**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**Esempio**

```javascript
_satellite.logger.error('No product ID found.');
```

L’oggetto `logger` consente di registrare un messaggio nella console del browser. Il messaggio viene visualizzato solo se l’utente ha abilitato il debug dei tag (chiamando `_satellite.setDebug(true)` o utilizzando un’estensione del browser adeguata).

### Registrazione degli avvisi di funzioni deprecate

```javascript
_satellite.logger.deprecation(message: string)
```

**Esempio**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

Registra un avviso nella console del browser. Il messaggio viene visualizzato indipendentemente dal fatto che l’utente abbia abilitato o meno il debug del tag.

## `cookie` {#cookie}

`_satellite.cookie` contiene funzioni per la lettura e la scrittura di cookie. Questa è una copia esposta della libreria js-cookie di terze parti. Per informazioni sull’utilizzo più avanzato di questa libreria, consulta la sezione [documentazione di js-cookie](https://www.npmjs.com/package/js-cookie#basic-usage).

### Impostare un cookie {#cookie-set}

Per impostare un cookie, utilizza `_satellite.cookie.set()`.

**Codice**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>Nel vecchio [`setCookie`](#setCookie) metodo di impostazione dei cookie, il terzo argomento (facoltativo) di questa chiamata di funzione era un numero intero che indicava il tempo di scadenza del cookie in giorni. In questo nuovo metodo, un oggetto &quot;attributes&quot; viene accettato come terzo argomento. Per impostare una scadenza per un cookie utilizzando il nuovo metodo, devi fornire un `expires` nell&#39;oggetto attributes e impostarla sul valore desiderato. Questo è dimostrato nell’esempio seguente.

**Esempio**

La seguente chiamata di funzione scrive un cookie che scade tra una settimana.

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### Recuperare un cookie {#cookie-get}

Per recuperare un cookie, utilizza `_satellite.cookie.get()`.

**Codice**

```javascript
_satellite.cookie.get(name: string) => string
```

**Esempio**

La seguente chiamata di funzione legge un cookie impostato in precedenza.

```javascript
var product = _satellite.cookie.get('product');
```

### Rimuovere un cookie {#cookie-remove}

Per rimuovere un cookie, utilizza `_satellite.cookie.remove()`.

**Codice**

```javascript
_satellite.cookie.remove(name: string)
```

**Esempio**

La seguente chiamata di funzione rimuove un cookie impostato in precedenza.

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**Codice**

```javascript
_satellite.buildInfo
```

Questo oggetto contiene informazioni sulla build dell’attuale libreria di runtime dei tag. L&#39;oggetto contiene le proprietà seguenti:

### `turbineVersion`

Fornisce la versione di [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizzata all’interno della libreria corrente.

### `turbineBuildDate`

La data di creazione della versione di [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizzata all&#39;interno del contenitore in formato ISO 8601.

### `buildDate`

La data di creazione della libreria corrente in formato ISO 8601.

Questo esempio illustra i valori dell&#39;oggetto:

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

Questo oggetto contiene informazioni sull’ambiente in cui è distribuita la libreria runtime corrente di tag.

**Codice**

```javascript
_satellite.environment
```

L&#39;oggetto contiene le proprietà seguenti:

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID dell’ambiente. |
| `stage` | L&#39;ambiente per il quale è stata generata la libreria. I valori possibili sono `development`, `staging`, e `production`. |

## `notify`

>[!NOTE]
>
>Questo metodo è stato dichiarato obsoleto. Utilizza piuttosto `_satellite.logger.log()`.

**Codice**

```javascript
_satellite.notify(message: string[, level: number])
```

**Esempio**

```javascript
_satellite.notify('Hello world!');
```

`notify` registra un messaggio nella console del browser. Il messaggio viene visualizzato solo se l’utente ha abilitato il debug dei tag (chiamando `_satellite.setDebug(true)` o utilizzando un’estensione del browser adeguata).

È possibile trasmettere un livello di registrazione facoltativo che influisca sullo stile e sul filtraggio del messaggio registrato. I livelli supportati sono i seguenti:

3: messaggi informativi.

4: messaggi di avviso.

5: messaggi di errore.

Se non definisci un livello di registrazione o non trasmetti altri valori di livello, il messaggio sarà registrato come messaggio regolare.

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>Questo metodo è stato dichiarato obsoleto. Utilizza piuttosto [`_satellite.cookie.set()`](#cookie-set).

**Codice**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**Esempio**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

Questa operazione imposta un cookie nel browser dell’utente. Il cookie persiste per il numero di giorni specificati.

## `readCookie`

>[!IMPORTANT]
>
>Questo metodo è stato dichiarato obsoleto. Utilizza piuttosto [`_satellite.cookie.get()`](#cookie-get).

**Codice**

```javascript
_satellite.readCookie(name: string) => string
```

**Esempio**

```javascript
var product = _satellite.readCookie('product');
```

Legge un cookie dal browser dell’utente.

## `removeCookie`

>[!NOTE]
>
>Questo metodo è stato dichiarato obsoleto. Utilizza piuttosto [`_satellite.cookie.remove()`](#cookie-remove).

**Codice**

```javascript
_satellite.removeCookie(name: string)
```

**Esempio**

```javascript
_satellite.removeCookie('product');
```

Rimuove un cookie dal browser dell’utente.

## Funzioni di debug

Non è possibile accedere alle seguenti funzioni dal codice di produzione. Queste sono intese solo a scopo di debug e cambiano nel tempo in base alle esigenze.

### `container`

**Codice**

```javascript
_satellite._container
```

**Esempio**

>[!IMPORTANT]
>
>Questa funzione non è accessibile dal codice di produzione. La funzione è intesa solo a scopo di debug e cambia nel tempo in base alle esigenze.

### `monitor`

**Codice**

```javascript
_satellite._monitors
```

**Esempio**

>[!IMPORTANT]
>
>Questa funzione non è accessibile dal codice di produzione. La funzione è intesa solo a scopo di debug e cambia nel tempo in base alle esigenze.

**Esempio**

Nella pagina web in cui è in esecuzione una libreria di tag, aggiungi uno snippet di codice all’HTML. In genere, il codice viene inserito nell’elemento `<head>` prima dell’elemento `<script>` che carica la libreria di tag. Questo consente al monitoraggio di rilevare i primi eventi di sistema che si verificano nella libreria di tag. Esempio:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

Nel primo elemento di script, poiché la libreria dei tag non è ancora stata caricata, viene creato l’oggetto `_satellite` iniziale e viene inizializzato un array su `_satellite._monitors`. Lo script aggiunge quindi un oggetto di monitoraggio a tale array. L’oggetto di monitoraggio può specificare i metodi seguenti, che verranno successivamente chiamati dalla libreria dei tag:

### `ruleTriggered`

Questa funzione viene chiamata dopo che un evento attiva una regola, ma prima dell’elaborazione delle condizioni e azioni della regola. L&#39;oggetto evento trasmesso a `ruleTriggered` contiene informazioni sulla regola attivata.

### `ruleCompleted`

Questa funzione viene chiamata dopo che una regola è stata completamente elaborata. In altre parole, l’evento si è verificato, tutte le condizioni sono state trasmesse e tutte le azioni sono state eseguite. L’oggetto evento trasmesso a `ruleCompleted` contiene informazioni sulla regola attivata.

### `ruleConditionFailed`

Questa funzione viene chiamata dopo l’attivazione di una regola per la quale una condizione ha avuto esito negativo. L&#39;oggetto evento trasmesso a `ruleConditionFailed` contiene informazioni sulla regola attivata e sula condizione che ha avuto esito negativo.

Se si chiama `ruleTriggered`, poco dopo sarà chiamato `ruleCompleted` oppure `ruleConditionFailed`.

>[!NOTE]
>
>Un monitoraggio non deve necessariamente specificare tutti e tre i metodi (`ruleTriggered`, `ruleCompleted` e `ruleConditionFailed`). I tag in Adobe Experience Platform funzionano con tutti i metodi supportati forniti dal monitoraggio.

### Verifica del monitoraggio

L&#39;esempio precedente specifica tutti e tre i metodi nel monitoraggio. Quando questi vengono chiamati, il monitoraggio disporrà di informazioni pertinenti. Per eseguire il test, imposta due regole nella libreria di tag:

1. Una regola con un evento di clic e una condizione di browser che trasmette solo se il browser è [!DNL Chrome].
1. Una regola con un evento di clic e una condizione di browser che trasmette solo se il browser è [!DNL Firefox].

Se apri la pagina in [!DNL Chrome], apri la console del browser e fai clic sulla pagina, la console visualizza quanto segue:

![](../../images/debug.png)

Puoi aggiungere agli handler hook o informazioni supplementari, se necessario.
