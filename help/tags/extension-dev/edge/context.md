---
title: Contesto nei moduli di estensione Edge
description: Scopri l’oggetto di contesto e il ruolo che svolge nell’interazione con i moduli libreria nelle estensioni tag di proprietà edge.
exl-id: 04e4e369-687e-4b46-9d24-18a97a218555
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 97%

---

# Contesto nei moduli di estensione edge

>[!NOTE]
>
> Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

A tutti i moduli libreria nelle estensioni edge viene fornito un oggetto `context` quando vengono eseguiti. Questo documento descrive le proprietà fornite dall&#39;oggetto `context` e il ruolo che svolgono nei moduli libreria.

## Contesto della richiesta Adobe (arc)

La proprietà `arc` è un oggetto che fornisce informazioni sull&#39;evento che attiva la regola. Le sezioni seguenti descrivono le varie sotto-proprietà contenute in questo oggetto.

### [!DNL event]

L’oggetto `event` rappresenta l’evento che ha attivato la regola e contiene i seguenti valori:

```js
logger.log(context.arc.event);
```

| Proprietà | Descrizione |
| --- | --- |
| `xdm` | L&#39;oggetto XDM dell&#39;evento. |
| `data` | Livello dati personalizzato. |

### [!DNL request]

Da non confondere con una richiesta del dispositivo client, `request` è un oggetto leggermente modificato proveniente da Adobe Experience Platform Edge Network.

```js
logger.log(context.arc.request)
```

L&#39;oggetto `request` ha due proprietà di livello principale: `body` e `head`. La proprietà `body` contiene informazioni su Experience Data Model (XDM) e può essere esaminata in Adobe Experience Platform Debugger quando si passa a **[!UICONTROL Launch]** e si seleziona la scheda **[!UICONTROL Edge Trace]**.

### [!DNL ruleStash] {#rulestash}

`ruleStash` è un oggetto che raccoglierà ogni risultato dai moduli di azione.

```js
logger.log(context.arc.ruleStash);
```

Ogni estensione dispone di un proprio namespace. Ad esempio, se l&#39;estensione ha il nome `send-beacon`, tutti i risultati delle azioni `send-beacon` saranno memorizzati nello spazio nomi `ruleStash['send-beacon']`.

Lo spazio nomi è univoco per ciascuna estensione e all&#39;inizio ha un valore `undefined`.

Lo spazio nomi viene sovrascritto con il risultato restituito da ogni azione. Ad esempio, si consideri un&#39;estensione `transform` contenente due azioni: `generate-fullname` e `generate-fulladdress`. Queste due azioni vengono poi aggiunte a una regola.

Se il risultato dell&#39;azione `generate-fullname` è `Firstname Lastname`, dopo il completamento dell&#39;azione verrà visualizzato lo stash della regola:

```js
{
  transform: 'Firstname Lastname'
}
```

Se il risultato dell&#39;azione `generate-address` è `3900 Adobe Way`, dopo il completamento dell&#39;azione verrà visualizzato lo stash della regola:

```js
{
  transform: '3900 Adobe Way'
}
```

Si noti che &quot;Nome Cognome&quot; non esiste più all&#39;interno dello stash della regola, perché l&#39;azione `generate-address` lo ha sovrascritto con un nuovo valore.

Se vuoi che `ruleStash` memorizzi i risultati di entrambe le azioni all&#39;interno dello spazio nomi `transform`, puoi scrivere il modulo di azione in modo simile all&#39;esempio seguente:

```js
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;

  if (!transformRuleStash) {
    transformRuleStash = {};
  }

  transformRuleStash.fullName = 'Firstname Lastname';

  return transformRuleStash;
}
```

La prima volta che questa azione viene eseguita, `ruleStash` inizia come `undefined` e viene quindi inizializzata come oggetto vuoto. La volta successiva in cui viene eseguita l&#39;azione, riceve `ruleStash` restituito quando l&#39;azione era stata precedentemente chiamata. L&#39;utilizzo di un oggetto come `ruleStash` consente di aggiungere nuovi dati senza perdere i dati precedentemente impostati da altre azioni dell&#39;estensione.

>[!NOTE]
>
>Quando si utilizza questa strategia, è necessario fare attenzione a restituire sempre lo stash della regola di estensione completa. Se invece si restituisce solo un valore, questo sovrascriverà tutte le altre proprietà eventualmente impostate.

## Utilità

La proprietà `utils` rappresenta un oggetto che fornisce utility specifiche per il runtime tag.

### [!DNL logger]

L’utility `logger` consente di registrare i messaggi che verranno visualizzati durante le sessioni di debug con [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

```js
context.utils.logger.error('Error!');
```

Il registratore dispone dei seguenti metodi, dove `message` è il messaggio da registrare:

| Metodo | Descrizione |
| --- | --- |
| `log(message)` | registra un messaggio nella console. |
| `info(message)` | registra un messaggio informativo nella console. |
| `warn(message)` | registra un messaggio di avvertenza nella console. |
| `error(message)` | registra un messaggio di errore nella console. |
| `debug(message)` | Registra un messaggio di debug nella console. Visibile solo se la registrazione `verbose` è abilitata nella console del browser. |

### [!DNL fetch]

Questa utility implementa l’[API Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API). Puoi utilizzare la funzione per effettuare richieste agli endpoint di terze parti.

```js
context.utils.fetch('http://example.com/movies.json')
  .then(response => response.json())
```

### [!DNL getBuildInfo]

Questa utility restituisce un oggetto contenente informazioni sulla build della libreria runtime corrente di tag.

```js
logger.log(context.utils.getBuildInfo().turbineBuildDate);
```

L’oggetto contiene i valori seguenti:

| Proprietà | Descrizione |
| --- | --- |
| `turbineVersion` | La versione di [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) utilizzata all&#39;interno della libreria corrente. |
| `turbineBuildDate` | La data di creazione della versione di [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) utilizzata all&#39;interno del contenitore in formato ISO 8601. |
| `buildDate` | La data di creazione della libreria corrente in formato ISO 8601. |
| `environment` | L&#39;ambiente per il quale è stata generata la libreria. I valori possibili includono `development`, `staging` e `production.` |

Di seguito è riportato un oggetto `getBuildInfo` di esempio per dimostrare i valori restituiti:

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

Questa utility restituisce l’ultimo oggetto `settings` salvato dalla vista di [configurazione dell’estensione](../configuration.md).

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

Questa utility restituisce l’oggetto `settings` più recente salvato dalla vista del modulo libreria corrispondente.

```js
logger.log(context.utils.getSettings());
```

### [!DNL getRule]

Questa utility restituisce un oggetto contenente informazioni sulla regola che attiva il modulo.

```js
logger.log(context.utils.getRule());
```

L’oggetto conterrà i seguenti valori:

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID della regola |
| `name` | Nome della regola |
