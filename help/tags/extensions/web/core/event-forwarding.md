---
title: Panoramica dell’estensione Core per l’inoltro degli eventi
description: Scopri l’estensione Core per l’inoltro degli eventi in Adobe Experience Platform.
feature: Event Forwarding
exl-id: b5ee4ccf-6fa5-4472-be04-782930f07e20
source-git-commit: d41779c5897b748130b88d3886472c7908347389
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 98%

---

# Panoramica sull’estensione Core per l’inoltro degli eventi

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’estensione Core per l’inoltro degli eventi fornisce gli eventi, le condizioni e i tipi di dati predefiniti per l’inoltro di eventi in Adobe Experience Platform.

Utilizza questo riferimento per informazioni sulle opzioni disponibili quando utilizzi questa estensione per creare una regola.

## Tipi di condizione dell&#39;estensione core

In questa sezione sono descritti i tipi di condizioni disponibili nell’estensione core. Questi tipi di condizioni possono essere utilizzati con il tipo di logica regolare o d’eccezione.

### Custom Code

Specifica un codice personalizzato che deve esistere come condizione dell&#39;evento. Utilizza l&#39;editor di codice incorporato per inserire il codice personalizzato. L’inoltro degli eventi in Adobe Experience Platform supporta ES6.

1. Seleziona **[!UICONTROL Apri editor]**.
1. Digita il codice personalizzato.
1. Seleziona **[!UICONTROL Salva]**.

Per accedere al valore di un elemento dati nel codice personalizzato, utilizza il metodo `getDataElementValue`. Ad esempio, per recuperare il valore di un elemento dati denominato `productName`, scrivi quanto segue: 

```javascript
getDataElementValue('productName') 
```

#### Oggetto ruleStash

Nel codice personalizzato, è possibile utilizzare anche l’oggetto `ruleStash`.

```javascript
arc.ruleStash: Object<string, *>`
```

```javascript
utils.logger.log(context.arc.ruleStash);
```

L’oggetto `ruleStash` raccoglie ogni risultato dai moduli di azione.

Ogni estensione dispone di un proprio namespace. Ad esempio, se l’estensione è denominata `send-beacon`, tutti i risultati delle azioni `send-beacon` vengono memorizzati nel namespace `ruleStash['send-beacon']`.

Il namespace è univoco per ciascuna estensione e ha il valore `undefined` all’inizio.

Il namespace verrà sovrascritto con il risultato restituito da ogni azione. Non avviene nulla di particolare. Ad esempio, per un’estensione `transform` contenente le due azioni `generate-fullname` e `generate-fulladdress`, aggiungi entrambe le azioni a una regola.

Se il risultato dell’azione `generate-fullname` è `Firstname Lastname`, allora dopo il completamento dell’azione verrà visualizzato il seguente stash della regola:

```js
{
  transform: 'Firstname Lastname`
}
```

Se il risultato dell’azione `generate-address` è `3900 Adobe Way`, allora dopo il completamento dell’azione verrà visualizzato il seguente stash della regola:

```js
{
  transform: '3900 Adobe Way`
}
```

Tieni presente che `Firstname Lastname` non esiste più nello stash della regola. L’azione `generate-address`, infatti, lo ha sovrascritto con i dati dell’indirizzo.

Se desideri memorizzare i risultati di entrambe le azioni all’interno del namespace `transform` nell’oggetto `ruleStash`, puoi scrivere il modulo di azione in modo simile all’esempio seguente:

```javascript
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;
  if (!transformRuleStash) {
    transformRuleStash = {};
  }
  transformRuleStash.fullName = 'Firstname Lastname';
  return transformRuleStash;
}
```

La prima volta che questa azione viene eseguita, l’oggetto `ruleStash` è `undefined` e viene inizializzato con un oggetto vuoto. Alla successiva esecuzione dell’azione, l’oggetto `ruleStash` viene restituito dall’azione in cui era stato precedentemente richiamato. L’utilizzo di un oggetto come `ruleStash` consente di aggiungere nuovi dati senza perdere quelli precedentemente impostati da altre azioni dell’estensione.

In questo caso, devi fare attenzione a restituire sempre lo stash completo della regola dell’estensione. Se restituisci solo un valore (ad esempio 5), lo stash della regola apparirà nel modo seguente:

```js
{
  transform: 5
}
```

### Confronto dei valori {#value-comparison}

Confronta due valori per determinare se questa condizione restituisce true.

Se disponi di una regola con più condizioni, è possibile che questa condizione restituisca true, ma la regola non viene comunque attivata perché le altre condizioni restituiscono false o una delle eccezioni restituisce true.

1. Immetti un valore.
1. Seleziona l&#39;operatore. Per ulteriori dettagli, consulta l&#39;elenco degli operatori di confronto dei valori.
1. Immetti un altro valore per il confronto.

Sono disponibili i seguenti operatori di confronto dei valori:

**Equal:** La condizione restituisce true se i due valori sono uguali utilizzando un confronto non rigoroso (in JavaScript, == operator). I valori possono essere di qualsiasi tipo. Quando digiti una parola come _true_, _false_, _null_ o _undefined_ in un campo value, la parola viene confrontata come stringa e non viene convertita nel relativo equivalente JavaScript.

**Does Not Equal:** La condizione restituisce true se i due valori non sono equalizzati con un confronto non rigoroso (in JavaScript il != operatore). I valori possono essere di qualsiasi tipo. Quando digiti una parola come _true_, _false_, _null_ o _undefined_ in un campo value, la parola viene confrontata come stringa e non viene convertita nel relativo equivalente JavaScript.

**Contains:** La condizione restituisce true se il primo valore contiene il secondo valore. I numeri vengono convertiti in stringhe. Qualsiasi valore diverso da un numero o una stringa fa sì che la condizione restituisca false.

**Does Not Contain:** La condizione restituisce true se il primo valore non contiene il secondo valore. I numeri vengono convertiti in stringhe. Qualsiasi valore diverso da un numero o una stringa fa sì che la condizione restituisca true.

**Starts With:** La condizione restituisce true se il primo valore inizia con il secondo valore. I numeri vengono convertiti in stringhe. Qualsiasi valore diverso da un numero o una stringa fa sì che la condizione restituisca false.

**Does Not Start With:** La condizione restituisce true se il primo valore non inizia con il secondo valore. I numeri vengono convertiti in stringhe. Se utilizzi un valore diverso da un numero o una stringa, la condizione restituisce true.

**Ends With:** La condizione restituisce true se il primo valore termina con il secondo valore. I numeri vengono convertiti in stringhe. Qualsiasi valore diverso da un numero o una stringa fa sì che la condizione restituisca false.

**Does Not End With:** La condizione restituisce true se il primo valore non termina con il secondo valore. I numeri vengono convertiti in stringhe. Se utilizzi un valore diverso da un numero o una stringa, la condizione restituisce true.

**Matches Regex:** La condizione restituisce true se il primo valore corrisponde all&#39;espressione regolare. I numeri vengono convertiti in stringhe. Qualsiasi valore diverso da un numero o una stringa fa sì che la condizione restituisca false.

**Does Not Match Regex:** La condizione restituisce true se il primo valore non corrisponde all&#39;espressione regolare. I numeri vengono convertiti in stringhe. Se utilizzi un valore diverso da un numero o una stringa, la condizione restituisce true.

**Is Less Than:** La condizione restituisce true se il primo valore è minore del secondo valore. Le stringhe che rappresentano i numeri sono convertite in numeri. Qualsiasi valore diverso da un numero o una stringa convertibile fa sì che la condizione restituisca false.

**Is Less Than Or Equal To:** La condizione restituisce true se il primo valore è minore o uguale al secondo valore. Le stringhe che rappresentano i numeri sono convertite in numeri. Qualsiasi valore diverso da un numero o una stringa convertibile fa sì che la condizione restituisca false.

**Is Greater Than:** La condizione restituisce true se il primo valore è maggiore del secondo valore. Le stringhe che rappresentano i numeri sono convertite in numeri. Qualsiasi valore diverso da un numero o una stringa convertibile fa sì che la condizione restituisca false.

**Is Greater Than Or Equal To:** La condizione restituisce true se il primo valore è maggiore o uguale al secondo valore. Le stringhe che rappresentano i numeri sono convertite in numeri. Qualsiasi valore diverso da un numero o una stringa convertibile fa sì che la condizione restituisca false.

**Is True:** La condizione restituisce true se il valore è booleano con il valore true. Il valore fornito non viene convertito in booleano se è di qualsiasi altro tipo. Un valore diverso da un valore booleano con valore true restituisce false.

**Is Truthy:** La condizione restituisce true se il valore è true dopo essere stato convertito in booleano. Consulta la [documentazione Truthy di MDN](https://developer.mozilla.org/it-IT/docs/Glossary/Truthy) per esempi di valori truthy.

**Is False:** La condizione restituisce true se il valore è booleano con il valore di false. Il valore fornito non viene convertito in booleano se è di qualsiasi altro tipo. Se un valore diverso da un valore booleano con valore false restituisce false, restituisce false.

**Is Falsy:** La condizione restituisce true se il valore è false dopo essere stato convertito in booleano. Consulta la [documentazione Falsy di MDN](https://developer.mozilla.org/it-IT/docs/Glossary/Falsy) per esempi di valori falsy.



## Tipi di azione dell&#39;estensione core

In questa sezione sono descritti i tipi di azioni disponibili nell&#39;estensione core.

### Codice personalizzato

Fornisci il codice che viene eseguito dopo l&#39;attivazione dell&#39;evento e le condizioni vengono valutate. L’inoltro degli eventi in Adobe Experience Platform supporta ES6.

1. Denomina il codice dell&#39;azione.
1. Seleziona **[!UICONTROL Apri editor]**.
1. Modifica il codice, quindi seleziona **[!UICONTROL Salva]**.

Per accedere al valore di un elemento dati nel codice personalizzato, utilizza il metodo `getDataElementValue`. Ad esempio, per recuperare il valore di un elemento dati denominato `productName`, scrivi quanto segue: 

```javascript
getDataElementValue('productName') 
```

Le azioni di inoltro eventi vengono eseguite in sequenza. È inoltre possibile che il codice personalizzato in un&#39;azione restituisca un valore che può essere utilizzato in un&#39;azione successiva. Il valore restituito può provenire dal codice all&#39;interno di tale azione, oppure dal corpo della risposta di una chiamata effettuata a una sorgente esterna. Per fare riferimento ai dati di un&#39;azione eseguita in precedenza all&#39;interno di una singola regola in cui viene utilizzata l’estensione Core, crea un elemento dati di tipo `Path` e utilizza il percorso seguente per fare riferimento al valore di una variabile denominata `productCategory` definita nel codice personalizzato all&#39;interno dell&#39;estensione Core:

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## Tipi di elementi di dati dell’estensione Core

I tipi di elementi dati sono determinati dall&#39;estensione. Non vi sono limiti ai tipi che è possibile creare.

Nelle sezioni seguenti sono descritti i tipi di elementi dati disponibili nell&#39;estensione Core. Altre estensioni utilizzano altri tipi di elementi dati.

### Custom Code

Per inserire nell’interfaccia utente un codice JavaScript personalizzato, fai clic su **[!UICONTROL Apri editor]** e inserisci il codice nella finestra dell’editor.

Nella finestra dell&#39;editor è necessaria un&#39;istruzione return per indicare il valore da utilizzare come valore dell&#39;elemento dati. Se non viene inclusa un&#39;istruzione return oppure viene restituito il valore `null` o `undefined`, il valore predefinito dell&#39;elemento dati è `null` o `undefined`.

Per accedere al valore di un elemento dati nel codice personalizzato, utilizza il metodo `getDataElementValue`. Ad esempio, per recuperare il valore di un elemento dati denominato `productName`, scrivi quanto segue: 

```javascript
getDataElementValue('productName') 
```

**Esempio:**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### Path

È possibile fare riferimento al percorso di una coppia chiave-valore in un evento inviato a Adobe Experience Platform Edge Network utilizzando il tipo di elemento dati Percorso.

Per fare riferimento all&#39;intero oggetto di un evento, immetti `arc` come percorso. L&#39;acronimo `arc` sta per Adobe Resource Context e rappresenta il percorso di livello principale per un evento inviato ad Adobe Experience Platform Edge Network.

Ad esempio, data la chiamata `interact` dal client a Edge Network, dalla console del browser è visibile la seguente richiesta:

```javascript
"events": [ 
        { 
             "xdm": { 
                    "page": { 
                            "btnHover": false, 
                            "pageName": "We Travel Home Page", 
                            "siteSection": "Landing Page" 
                     }] 
```

Per immettere un percorso che faccia riferimento a `pageName`, nel campo Percorso immetti quanto segue:

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>La chiamata `interact` dal client contiene `events`, ma per l’inoltro degli eventi è necessario `event`. L’inoltro di eventi, infatti, controlla ogni evento singolarmente e non come batch di più eventi come visualizzato sul client.
