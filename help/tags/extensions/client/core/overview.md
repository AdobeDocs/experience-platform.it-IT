---
title: Panoramica dell’estensione Core
description: Scopri l’estensione tag Core in Adobe Experience Platform.
exl-id: 841f32ad-a6a8-49fb-a131-ef4faab47187
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '5482'
ht-degree: 83%

---

# Panoramica dell’estensione Core

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’estensione tag Core è l’estensione predefinita rilasciata con Adobe Experience Platform.

Questo documento descrive le opzioni disponibili quando si utilizza l’estensione Core per creare una regola.

## Tipi di eventi dell&#39;estensione core {#core-extension-event-types}

In questo capitolo sono descritti i tipi di evento disponibili nell&#39;estensione core. Per informazioni sulle opzioni che possono essere impostate per diversi tipi di eventi, vedi la sezione [Opzioni](#options).

### Eventi basati su browser

#### Tab Blur

L’evento tab-blur attiva l’azione quando una scheda perde lo stato attivo. Non sono disponibili impostazioni per questo tipo di evento.

#### Tab Focus

L’evento tab-focus attiva l’azione quando una scheda diventa attiva. Non sono disponibili impostazioni per questo tipo di evento.

### Modulo

#### Blur

L’evento blur attiva l’azione quando un modulo perde lo stato attivo. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

#### Focus

L’evento focus attiva l’azione quando un modulo diventa attivo. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

#### Submit

L’evento submit attiva l’azione quando un modulo viene inviato. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

### Eventi controllati dalla tastiera

#### Key Press

L’evento viene attivato quando viene premuto un tasto. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

### Eventi basati su file multimediali

#### Media Ended

L’evento viene attivato al termine del contenuto multimediale. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

#### Media-Loaded Data

L’evento viene attivato quando vengono caricati dati di file multimediali. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

#### Media Pause

L’evento si attiva quando il contenuto multimediale viene messo in pausa. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

#### Media Play

L’evento si attiva durante la riproduzione del contenuto multimediale. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

#### Media Stalled

L’evento si attiva se il contenuto multimediale si arresta. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

#### Tempo di riproduzione file multimediale

L’evento si attiva se il contenuto multimediale viene riprodotto per un periodo di tempo specificato. Per attivare l’evento è necessario specificare la durata della riproduzione del file multimediale. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).


#### Volume del file multimediale modificato

L’evento si attiva se il volume viene alzato o abbassato. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

### Eventi orientati ai dispositivi mobili

#### Orientation Change

L’evento si attiva se cambia l’orientamento del dispositivo. Per attivare l’evento è necessario specificare la durata di modifica dell’orientamento. Non sono disponibili impostazioni per questo tipo di evento.

#### Zoom Change

L’evento si attiva se l’utente utilizza la funzione zoom. Non sono disponibili impostazioni per questo tipo di evento.

### Eventi controllati dal mouse

#### Click

L’evento si attiva se l’utente seleziona l’elemento specificato (facendo clic). Facoltativamente, puoi specificare valori di proprietà che devono risultare true per l&#39;elemento prima che l&#39;evento venga attivato.

Se l’elemento è un tag di ancoraggio (`<a>`) per collegare il contenuto, puoi anche specificare se posticipare la navigazione per un periodo di tempo. Questo può essere utile se la regola richiede un tempo supplementare per essere eseguita e non viene normalmente completata prima che venga eseguita la navigazione nelle pagine.

>[!WARNING]
>
>Quest’opzione deve essere utilizzata con estrema cautela a causa delle potenziali conseguenze negative che provoca all’esperienza utente se utilizzata in modo errato.

Quando utilizzi il ritardo dei collegamenti, Platform impedisce al browser di spostarsi fuori dalla pagina. Successivamente, esegue un reindirizzamento JavaScript alla destinazione originale dopo il timeout specificato. Ciò è particolarmente pericoloso se il markup della pagina contiene tag `<a>` la cui funzionalità prevista non fa uscire l’utente dalla pagina. Se non è possibile risolvere il problema in altro modo, è necessario essere estremamente precisi nella definizione del selettore, in modo che questo evento venga attivato esattamente dove necessario e in nessun altro punto.

Il valore predefinito del ritardo del collegamento è 100 millisecondi. Tieni presente che i tag attenderanno sempre il tempo specificato e non sarà in alcun modo collegato all’esecuzione delle azioni della regola. È possibile che il ritardo obblighi l’utente ad aspettare più tempo del necessario e che il ritardo non sia sufficiente per il completamento di tutte le azioni della regola. I ritardi più lunghi forniscono più tempo per l’esecuzione delle regole, ma peggiorano anche l’esperienza utente.

Per attivare il ritardo è necessario fornire sia l’elemento selezionato che attiva l’evento, sia la quantità specifica di tempo prima che l’evento venga attivato.

Per ulteriori informazioni sulle opzioni avanzate, consulta la sezione [Opzioni](#options).

#### Hover

L’evento si attiva se l’utente passa col cursore sopra un elemento specificato. Inoltre, devi configurare se la regola viene attivata immediatamente o dopo un numero specificato di millisecondi. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

### Altri eventi

#### Custom Event

L’evento si attiva se si verifica un tipo di evento personalizzato. Le funzioni JavaScript denominate definite altrove nel codebase possono essere utilizzate come tipo di evento personalizzato. Specifica il nome del tipo di evento personalizzato, quindi configura le altre impostazioni come descritto nella sezione [Opzioni](#options) di seguito.

#### Data Element Changed

L’evento si attiva se un elemento dati specificato cambia. È necessario specificare un nome per l’elemento dati. Puoi selezionare l’elemento dati digitandone il nome nel campo di testo o selezionando l’icona dell’elemento dati sul lato destro del campo di testo e scegliendo da un elenco fornito all’interno della finestra di dialogo visualizzata.

#### Direct Call {#direct-call-event}

Un evento di chiamata diretta bypassa i sistemi di rilevamento degli eventi e di ricerca. Le regole di chiamata diretta sono ideali per le situazioni in cui desideri comunicare al sistema esattamente ciò che sta accadendo. Inoltre, sono ideali quando il sistema non è in grado di rilevare un evento nel DOM.

Quando definisci un evento di chiamata diretta, devi specificare una stringa che fungerà da identificatore dell’evento. Se un [attiva azione di chiamata diretta](#direct-call-action) contenente lo stesso identificatore viene attivato, verranno eseguite tutte le regole di evento di chiamata diretta in ascolto di tale identificatore.

![Schermata di un evento Direct Call nell’interfaccia utente di Data Collection](../../../images/extensions/client/core/direct-call-event.png)

#### Element Exists

L’evento si attiva se è presente un elemento specificato. Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

#### Enters Viewport

Attiva l’evento se l’utente immette un riquadro di visualizzazione specificato. Devi fornire un selettore CSS come criterio per eseguire il targeting degli elementi corrispondenti. È inoltre necessario configurare se la regola viene attivata immediatamente o dopo un numero specificato di millisecondi e se l’evento deve essere attivato ogni volta che si verifica o solo la prima volta.

Per ulteriori informazioni sulle impostazioni personalizzabili degli eventi, consulta la sezione [Opzioni](#options).

#### History Change

L’evento viene attivato se si verifica un evento pushState o hashchange. Non sono disponibili impostazioni per questo tipo di evento.

#### Tempo trascorso sulla pagina

L’evento viene attivato se l’utente rimane sulla pagina per un numero specificato di secondi. Specifica quanti secondi devono trascorrere prima che l’evento venga attivato.

### Eventi di caricamento pagina

#### DOM Ready

L’evento viene attivato quando il DOM è pronto e l’utente può interagire con la pagina. Non sono disponibili impostazioni per questo tipo di evento.

#### Library Loaded (Page Top) (Libreria caricata (Inizio pagina)) {#library-loaded-page-top}

L’evento viene attivato non appena viene caricata la libreria di tag. Non sono disponibili impostazioni per questo tipo di evento.

#### Page Bottom {#page-bottom}

L’evento viene attivato una volta chiamato `_satellite.pageBottom();`. Quando la libreria di tag viene caricata in modo asincrono, questo tipo di evento non deve essere utilizzato. Non sono disponibili impostazioni per questo tipo di evento.

#### Window Loaded

L’evento si attiva quando onLoad viene chiamato dal browser e la pagina è stata completamente caricata. Non sono disponibili impostazioni per questo tipo di evento.

### Opzioni {#options}

Ogni tipo di evento modulo utilizza le impostazioni seguenti:

#### Specific Elements \| Any Element

* Se selezioni **[!UICONTROL Elementi specifici]**, vengono visualizzate le opzioni per selezionare gli elementi e i valori della proprietà.
* Se selezioni **[!UICONTROL Qualsiasi elemento]**, non vi sono ulteriori opzioni necessarie per limitare gli elementi.

#### Elements matching the CSS selector

Inserisci il selettore CSS che identifica gli elementi che attivano l&#39;evento.

#### And having certain property values

Se selezioni questa opzione, diventano disponibili i seguenti parametri:

* `property=value`

  Specifica il valore della proprietà

* Regex

  Attiva se `property=value` è un&#39;espressione regolare.

* Add

  Aggiungi un&#39;altra coppia `property=value`.

#### Advanced options (Bubbling)

* Esegui questa regola anche quando l&#39;evento ha origine da un elemento discendente
* Consenti l&#39;esecuzione di questa regola anche se l&#39;evento ha già attivato una regola riferita a un elemento discendente
* Una volta eseguita la regola, impedisci all&#39;evento di attivare elementi di targeting di regole

## Tipi di condizione dell&#39;estensione core

In questa sezione sono descritti i tipi di condizioni disponibili nell’estensione core. Questi tipi di condizioni possono essere utilizzati con il tipo di logica regolare o d’eccezione.

### Dati

#### Cookie

Specifica il nome e il valore del cookie che devono esistere affinché un evento attivi un&#39;azione.

1. Specifica un nome per il cookie.
1. Inserisci il valore che deve esistere nel cookie se desideri che l&#39;evento attivi un&#39;azione.
1. (Facoltativo) Se si tratta di un&#39;espressione regolare, abilita Regex.

#### Custom Code

Specifica un codice personalizzato che deve esistere come condizione dell&#39;evento.

>[!NOTE]
>
>JavaScript ES6+ è ora supportato nel codice personalizzato. Alcuni browser meno recenti non supportano ES6+. Per comprendere l’impatto dell’utilizzo delle funzioni ES6+, esegui il test su tutti i browser web che dovrebbero essere supportati.

Utilizza l&#39;editor di codice incorporato per inserire il codice personalizzato:

1. Seleziona **[!UICONTROL Apri editor]**.
1. Digita il codice personalizzato.
1. Seleziona **[!UICONTROL Salva]**.

Una variabile denominata `event` sarà automaticamente disponibile; potrai fare riferimento a essa all&#39;interno del codice personalizzato. L&#39;oggetto `event` conterrà informazioni utili sull&#39;evento che ha attivato la regola. Il modo più semplice per determinare quali dati evento sono disponibili è accedere `event` alla console dall&#39;interno del codice personalizzato:

```javascript
console.log(event);
return true;
```

Esegui la regola in un browser ed esamina l&#39;oggetto evento registrato nella console del browser. Una volta raccolte le informazioni disponibili è possibile usarle per prendere decisioni programmatiche all’interno del codice personalizzato.

*Sequenza delle condizioni*

Quando l’opzione &quot;Esegui componenti regola in sequenza&quot; dalle impostazioni di proprietà è abilitata, è possibile che i componenti regola successivi siano in attesa mentre la condizione esegue un’attività asincrona.

Quando la condizione restituisce una [promessa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), la condizione successiva nella regola non viene eseguita finché la promessa restituita non è risolta. Se la promessa viene rifiutata, i tag considerano tale condizione come non riuscita e non verranno eseguite ulteriori condizioni o azioni da quella regola.

Esempio di condizione che restituisce una promessa:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

#### Confronto dei valori {#value-comparison}

Confronta due valori per determinare se questa condizione restituisce true.

Se disponi di una regola con più condizioni, è possibile che questa condizione restituisca true, ma la regola non viene comunque attivata perché le altre condizioni restituiscono false o una delle eccezioni restituisce true.

1. Immetti un valore.
1. Seleziona l&#39;operatore. Per ulteriori dettagli, consulta l&#39;elenco degli operatori di confronto dei valori.
1. (Se necessario) Seleziona se il confronto deve non essere sensibile alle maiuscole/minuscole.
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

**Is Truthy:** La condizione restituisce true se il valore è true dopo essere stato convertito in booleano. Per esempi di valori truthy consulta [documentazione Truthy di MDN](https://developer.mozilla.org/it-IT/docs/Glossary/Truthy).

**Is False:** La condizione restituisce true se il valore è booleano con il valore di false. Il valore fornito non viene convertito in booleano se è di qualsiasi altro tipo. Se un valore diverso da un valore booleano con valore false restituisce false, restituisce false.

**Is Falsy:** La condizione restituisce true se il valore è false dopo essere stato convertito in booleano. Per esempi di valori falsy consulta [documentazione Falsy di MDN](https://developer.mozilla.org/it-IT/docs/Glossary/Falsy).

#### Variable

Specifica il nome e il valore della variabile JavaScript esistenti affinché un evento attivi un&#39;azione.

1. Specifica il nome della variabile JavaScript.
1. Specifica il valore della variabile che deve esistere come condizione per l&#39;evento.
1. (Facoltativo) Se si tratta di un&#39;espressione regolare, abilita Regex.

### Coinvolgimento

#### Landing Page

Specifica la pagina a cui l&#39;utente deve accedere per attivare l&#39;evento.

1. Specifica la pagina di destinazione.
1. (Facoltativo) Se si tratta di un&#39;espressione regolare, abilita Regex.

#### New/Returning Visitor

Specifica se il visitatore deve essere un nuovo visitatore o un visitatore di ritorno per attivare un&#39;azione.

Seleziona una delle seguenti opzioni:

* New Visitor
* Returning Visitor

#### Page Views

Configura il numero di volte in cui il visitatore deve visualizzare la pagina prima che l&#39;azione venga attivata.

1. Seleziona se il numero di visualizzazioni di pagina deve essere maggiore di, uguale o inferiore al valore specificato.
1. Specifica il numero di visualizzazioni di pagina che determinano se la condizione è soddisfatta.
1. Configura quando le visualizzazioni di pagina vengono conteggiate selezionando una delle seguenti opzioni:
   * Lifetime
   * Current Session

#### Sessions

Attiva l&#39;azione se il numero di sessioni dell&#39;utente soddisfa i criteri specificati.

1. Seleziona se il numero di sessioni deve essere maggiore di, uguale o inferiore al valore specificato.
1. Specifica il numero di sessioni che determinano se la condizione è soddisfatta.

#### Time On Site

Attiva l&#39;azione se il numero di sessioni dell&#39;utente soddisfa i criteri specificati.

Configura per quanto tempo il visitatore deve trovarsi sul sito prima che l&#39;azione venga attivata.

1. Seleziona se il numero di minuti sul sito deve essere maggiore di, uguale o inferiore al valore specificato.
1. Specifica il numero di minuti che determinano se la condizione è soddisfatta.

#### Traffic Source

Attiva l&#39;azione se il numero di sessioni dell&#39;utente soddisfa i criteri specificati.

Specifica l&#39;origine del traffico del visitatore che deve essere true per attivare l&#39;azione.

1. Specificate l&#39;origine del traffico.
1. (Facoltativo) Se si tratta di un&#39;espressione regolare, abilita Regex.

### Tecnologia

#### Browser

Seleziona il browser che il visitatore deve usare per attivare l&#39;azione.

Seleziona uno o più browser seguenti:

* Chrome
* Firefox
* Internet Explorer/Edge
* Internet Explorer Mobile
* Mobile Safari
* OmniWeb
* Opera
* Opera Mini
* Opera Mobile
* Safari

#### Device Type

Seleziona il tipo di dispositivo che il visitatore deve usare per attivare l&#39;azione.

Seleziona uno o più dei seguenti tipi di dispositivi:

* Android
* Blackberry
* Desktop
* iPad
* iPhone
* iPod
* Nokia
* Windows Phone

#### Operating System

Seleziona il sistema operativo che il visitatore deve utilizzare per attivare l&#39;azione.

Seleziona uno o più dei seguenti sistemi operativi:

* Android
* Blackberry
* iOS
* Linux
* MacOS
* Maemo
* Symbian OS
* Unix
* Windows

#### Screen Resolution

Seleziona la risoluzione dello schermo che i visitatori devono usare sui propri dispositivi per attivare l&#39;azione.

1. Seleziona se la larghezza della risoluzione dello schermo del dispositivo del visitatore deve essere maggiore di, uguale o inferiore al valore specificato.
1. Specifica il numero di pixel richiesti per la larghezza della risoluzione dello schermo.
1. Seleziona se l&#39;altezza della risoluzione dello schermo del dispositivo del visitatore deve essere maggiore di, uguale o inferiore al valore specificato.
1. Specifica il numero di pixel necessari per l&#39;altezza della risoluzione dello schermo.

#### Window Size

Seleziona la dimensione della finestra che i visitatori devono usare sui propri dispositivi per attivare l&#39;azione.

1. Seleziona se la larghezza della finestra del dispositivo del visitatore deve essere maggiore di, uguale o inferiore al valore specificato.
1. Specifica il numero di pixel richiesti per la larghezza della finestra.
1. Seleziona se l&#39;altezza della finestra del dispositivo del visitatore deve essere maggiore di, uguale o inferiore al valore specificato.
1. Specifica il numero di pixel necessari per l&#39;altezza della finestra.

### URL

#### Dominio

Specifica il dominio del visitatore.

#### Hash

Specifica uno o più pattern di hash che devono esistere nell&#39;URL.

>[!NOTE]
>
>I pattern di hash multipli sono collegati da un operatore OR.

1. Specifica il pattern di hash.
1. (Facoltativo) Se si tratta di un&#39;espressione regolare, abilita Regex.
1. Aggiungi altri pattern di hash.

#### Path And Quest String

Specifica uno o più percorsi che devono esistere nell’URL. Questo include il percorso e la stringa query.

>[!NOTE]
>
>Più percorsi sono collegati da un operatore OR.

1. Specifica il percorso.
1. (Facoltativo) Se si tratta di un&#39;espressione regolare, abilita Regex.
1. Aggiungi altri percorsi.

#### Path Without Query String

Specifica uno o più percorsi che devono esistere nell’URL. Questo include il percorso ma non la stringa query.

>[!NOTE]
>
>Più percorsi sono collegati da un operatore OR.

1. Specifica il percorso.
1. (Facoltativo) Se si tratta di un&#39;espressione regolare, abilita Regex.
1. Aggiungi altri percorsi.

#### Protocol

Specifica il protocollo utilizzato nell&#39;URL.

Seleziona una delle seguenti opzioni:

* HTTP
* HTTPS

#### Query String Parameter

Specifica il parametro URL utilizzato nell&#39;URL.

1. Specifica il nome di un parametro URL.
1. Specifica il valore utilizzato per il parametro URL.
1. (Facoltativo) Se si tratta di un&#39;espressione regolare, abilita Regex.

#### Subdomain

Specifica uno o più domini che devono esistere nell&#39;URL.

>[!NOTE]
>
>Più domini secondari sono collegati da un operatore OR.

1. Specifica il sottodominio.
1. (Facoltativo) Se si tratta di un&#39;espressione regolare, abilita Regex.
1. Aggiungi altri domini.

### Altro

#### Date Range

Specifica un intervallo di date. Scegli la data e l&#39;ora in cui si verifica l&#39;evento, la data in cui si è verificato prima e il fuso orario.

#### Max Frequency

Specifica il numero massimo di volte che la condizione restituisce true. Puoi scegliere una delle opzioni seguenti:

* Page view
* Sessions
* Visitor
* Seconds
* Minutes
* Days
* Weeks
* Months

Se la condizione di frequenza massima per sessione è pari a 1, vengono confrontati questi due elementi `localStorage`. Se `visitorTracking.sessionCount` è maggiore del valore di `maxFrequency.session`, la condizione di campionamento è true. Se i due valori sono uguali, la condizione è false.

`sessionCount` è un elemento `visitorTracking`, pertanto affinché la condizione di campionamento funzioni deve essere abilitata l’API visitatore.

#### Sampling

Specifica la percentuale di tempo restituita dalla condizione.

## Tipi di azione dell&#39;estensione core

In questa sezione sono descritti i tipi di azioni disponibili nell&#39;estensione core.

### Custom Code

>[!NOTE]
>
>JavaScript ES6+ è ora supportato nel codice personalizzato. Alcuni browser meno recenti non supportano ES6+. Per comprendere l’impatto dell’utilizzo delle funzioni ES6+, esegui il test su tutti i browser web che dovrebbero essere supportati.

Fornisci il codice che viene eseguito dopo l&#39;attivazione dell&#39;evento e le condizioni vengono valutate.

1. Denomina il codice dell&#39;azione.
1. Seleziona la lingua utilizzata per definire l&#39;azione:
   * JavaScript
   * HTML
1. Seleziona se eseguire il codice dell&#39;azione a livello globale.
1. Seleziona **[!UICONTROL Apri editor]**.
1. Modifica il codice, quindi seleziona **[!UICONTROL Salva]**.

Quando JavaScript è selezionato come linguaggio, sarà automaticamente disponibile una variabile denominata `event` a cui è possibile fare riferimento all&#39;interno del codice personalizzato. L&#39;oggetto `event` conterrà informazioni utili sull&#39;evento che ha attivato la regola. Il modo più semplice per determinare quali dati evento sono disponibili è accedere `event` alla console dall&#39;interno del codice personalizzato:

```javascript
console.log(event);
```

Esegui la regola in un browser ed esamina l&#39;oggetto evento registrato nella console del browser. Dopo aver compreso le informazioni disponibili, potrai utilizzarle per le decisioni programmate all&#39;interno del codice personalizzato, inviare una parte dell&#39;oggetto `event` a un server e così via.

### Elaborazione azione Custom Code

L’estensione Core, disponibile per tutti gli utenti di Adobe Experience Platform, contiene un’azione Custom Code per l’esecuzione di JavaScript o HTML fornito dall’utente. Spesso è utile che gli utenti possano capire in che modo vengono elaborate le regole con le azioni Custom Code.

#### Regole che utilizzano gli eventi Inizio pagina o Fine pagina

Il codice da azioni personalizzate è incorporato nella libreria di tag principale. Il codice viene scritto nel documento utilizzando document.write. Se una regola include più azioni Custom Code, il codice viene scritto nell&#39;ordine configurato nella regola.

#### Regole che utilizzano un evento diverso da Inizio pagina o Fine pagina

Un codice da azioni personalizzate viene caricato dal server e scritto sul documento utilizzando [Postscribe](https://github.com/krux/postscribe). Se una regola include più azioni Custom Code, il codice viene caricato in parallelo dal server, ma scritto nell&#39;ordine configurato nella regola.

L&#39;utilizzo di a document.write dopo il caricamento di una pagina comporterebbe in genere problemi, ma non si tratta di un problema per il codice fornito tramite azioni Custom Code. Puoi utilizzare document.write nelle azioni Custom Code indipendentemente da quando verrà eseguito il codice.

#### Convalida Custom Code

La convalida utilizzata nell’editor di codice tag è progettata per individuare eventuali problemi nel codice scritto dallo sviluppatore. Un codice che è passato attraverso un processo di minimizzazione, come il codice AppMeasurement.js scaricato dal Code Manager, potrebbe essere falsamente segnalato come problematico dal validatore, che di solito può essere ignorato.

#### Sequenza delle azioni

Quando l’opzione &quot;Esegui componenti regola in sequenza&quot; dalle impostazioni di proprietà è abilitata, è possibile che i componenti regola successivi siano in attesa mentre l’azione esegue un’attività asincrona.  Questo avviene diversamente per i codici personalizzati JavaScript e HTML.

*JavaScript*

Quando si crea un’azione di codice personalizzato JavaScript, è possibile restituire una [promessa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) dall’azione. L’azione successiva nella regola viene eseguita solo quando la promessa restituita è stata risolta. Se la promessa viene rifiutata, le azioni successive della regola non vengono eseguite.

>[!NOTE]
>
>Questo avviene solo quando il codice JavaScript non è impostato per l’esecuzione a livello globale. Se esegui l’azione del codice personalizzato nell’ambito globale, i tag intenderanno la promessa risolta immediatamente e passeranno all’elemento successivo nella coda di elaborazione.

Esempio di azione di un codice personalizzato JavaScript che restituisce una promessa:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

*HTML*

Quando si crea un’azione di codice personalizzato HTML, una funzione denominata `onCustomCodeSuccess()` è disponibile per l’uso all’interno del codice personalizzato. È possibile chiamare questa funzione per indicare che il codice personalizzato è stato completato e che i tag possono continuare l’esecuzione delle azioni successive. Se invece per qualche motivo il codice personalizzato genera un errore, è possibile chiamare `onCustomCodeFailure()`. In questo modo i tag non eseguiranno le azioni successive da quella regola.

Un esempio di azione di un codice personalizzato HTML che utilizza i nuovi callback:

```html
<script>
setTimeout(function() {
  if (new Date().getDay() === 5) {
    onCustomCodeSuccess();
  } else {
    onCustomCodeFailure();
  }
}, 1000);
</script>
```

### Attiva chiamata diretta {#direct-call-action}

Questa azione attiva tutte le regole che utilizzano un [evento di chiamata diretta](#direct-call-event). Durante la configurazione dell’azione, devi fornire la stringa di identificazione per l’evento di chiamata diretta che desideri attivare. Facoltativamente, puoi anche trasmettere i dati all’evento di chiamata diretta tramite una `detail` oggetto, che può contenere un set personalizzato di coppie chiave-valore.

![Schermata di un’azione Trigger Direct Call nell’interfaccia utente di Data Collection](../../../images/extensions/client/core/direct-call-action.png)

L’azione viene mappata direttamente su [`track` metodo](../../../ui/client-side/satellite-object.md#track) nel `satellite` , accessibile tramite codice lato client.

## Tipi di elementi di dati dell’estensione Core

I tipi di elementi dati sono determinati dall&#39;estensione. Non vi sono limiti ai tipi che è possibile creare.

Nelle sezioni seguenti sono descritti i tipi di elementi dati disponibili nell&#39;estensione Core. Altre estensioni utilizzano altri tipi di elementi dati.

### Cookie

A qualsiasi cookie di dominio può essere fatto riferimento nel campo del nome del cookie.

#### Esempio:

`cookieName`

### Costante

Qualsiasi valore di stringa costante a cui è possibile fare riferimento in azioni o condizioni.

#### Esempio:

`string`

### Custom Code

>[!NOTE]
>
>JavaScript ES6+ è ora supportato nel codice personalizzato. Alcuni browser meno recenti non supportano ES6+. Per comprendere l’impatto dell’utilizzo delle funzioni ES6+, esegui il test su tutti i browser web che dovrebbero essere supportati.

JavaScript personalizzato può essere inserito nell&#39;interfaccia utente facendo clic su Open Editor e inserendo il codice nella finestra dell’editor.

Nella finestra dell&#39;editor è necessaria un&#39;istruzione return per indicare il valore da utilizzare come valore dell&#39;elemento dati. Se un&#39;istruzione return non è inclusa o il valore `null` o `undefined` viene restituito, il valore predefinito dell&#39;elemento dati sarà utilizzato come valore dell&#39;elemento dati.

**Esempio:**

```javascript
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Se l&#39;elemento dati del codice personalizzato viene recuperato come parte di un&#39;esecuzione di una regola, una variabile chiamata `event` diventa automaticamente disponibile; potrai fare riferimento a essa all&#39;interno del codice personalizzato. L&#39;oggetto `event` conterrà informazioni utili sull&#39;evento che ha attivato la regola. Il modo più semplice per determinare quali dati evento sono disponibili è accedere `event` alla console dall&#39;interno del codice personalizzato:

```javascript
console.log(event);
return true;
```

Esegui la regola in un browser ed esamina l&#39;oggetto evento registrato nella console del browser. Una volta comprese le informazioni disponibili in base alle varie regole che possono utilizzare l&#39;elemento dati, potrai utilizzarle per le decisioni di programmazione all&#39;interno del codice personalizzato o restituire un elemento dell&#39;oggetto `event` come valore dell&#39;elemento dati.

### DOM attribute

Qualsiasi valore di elemento può essere recuperato, ad esempio un tag div o H1.

#### Esempio:

CSS Selector Chain:

`id#dc logo img`

Ottieni il valore di:

`src`

### Variabile JavaScript

È possibile fare riferimento a qualsiasi oggetto o variabile JavaScript disponibile utilizzando il campo path.

Gli elementi dati di tag possono essere utilizzati per acquisire le variabili JavaScript di markup o le proprietà degli oggetti. Questi valori possono quindi essere utilizzati all’interno di estensioni o regole personalizzate mediante riferimento agli elementi dati dei tag. Se l’origine dei dati cambia, è necessario solo aggiornare il riferimento all’origine.

Nell’esempio seguente, il markup contiene una variabile JavaScript denominata `Page_Name`.

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Quando crei l&#39;elemento dati , fornisci semplicemente il percorso di tale variabile.

Se utilizzi un oggetto raccolta dati come parte del livello dati, utilizza la notazione del punto nel percorso per fare riferimento all&#39;oggetto e alla proprietà che desideri acquisire nell&#39;elemento dati, come `_myData.pageName`, o `digitalData.pageName`e così via.

#### Esempio:

`window.document.title`

### Local storage

Immetti il nome dell&#39;elemento di memorizzazione locale nel campo Local Storage Item Name.

La memorizzazione locale offre ai browser un modo per memorizzare informazioni da pagina a pagina ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). La memorizzazione locale funziona in modo simile ai cookie, ma è molto più grande e flessibile.

Utilizza il campo fornito per specificare il valore creato per un elemento di archiviazione locale, ad esempio `lastProductViewed.`

### Oggetti uniti

Seleziona più elementi dati che forniranno ciascuno un oggetto. Questi oggetti verranno uniti in profondità (in modo ricorsivo) per produrre un nuovo oggetto. Gli oggetti di origine non verranno modificati. Se una proprietà viene trovata nella stessa posizione su più oggetti sorgente, verrà utilizzato il valore di quest&#39;ultimo oggetto. Se il valore di una proprietà di origine è `undefined`, non sostituisce un valore di un oggetto sorgente precedente. Se si trovano array nella stessa posizione su più oggetti sorgente, gli array vengono concatenati.

Ad esempio, supponiamo di selezionare un elemento dati che fornisce il seguente oggetto:

```
{
  "sport": {
    "name": "tennis"
  },
  "dessert": "ice cream",
  "fruits": [
    "apple",
    "banana"
  ]
}
```

Supponiamo di selezionare anche un altro elemento dati che fornisce il seguente oggetto:

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": undefined,
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "cherry",
    "duku"
  ]
}
```

Il risultato dell&#39;elemento dati Oggetti uniti è il seguente oggetto:

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": "ice cream",
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "apple",
    "banana",
    "cherry",
    "duku"
  ]
}
```

### Informazioni pagina

Usa questi punti dati per acquisire informazioni di pagina da utilizzare nella logica della regola o per inviare informazioni ad Analytics o a sistemi di tracciamento esterni.

Puoi selezionare uno dei seguenti attributi di pagina da utilizzare nell&#39;elemento dati:

* URL
* Hostname
* Pathname
* Protocol
* Referrer
* Title

### Query String Parameter

Specifica un parametro URL singolo nel campo URL Parameter.

È necessaria solo la sezione name ed eventuali designatori speciali come &quot;?&quot; o “=” devono essere omessi.

#### Esempio:

`contentType`

### Numero casuale

Utilizza questo elemento dati per generare un numero casuale. Viene spesso utilizzato per campionare dati o creare ID, ad esempio un Hit ID. Il numero casuale può essere usato per oscurare o conservare i dati sensibili. Alcuni esempi possono includere:

* Generare un Hit ID
* Concatenare il numero a un token utente o a una marca temporale per garantire l&#39;univocità
* Eseguire un hash unidirezionale sui dati PII
* Decidere in modo casuale quando visualizzare una richiesta sondaggio sul sito

Specifica i valori minimo e massimo per il numero casuale.

**Valori predefiniti:**

Minimo: 0

Massimo: 1000000000

### Session storage

Immetti il nome dell&#39;elemento di archiviazione sessione nel campo Session Storage Item Name.

L&#39;archiviazione della sessione è simile all&#39;archiviazione locale, fatta eccezione per i dati che vengono eliminati al termine della sessione, mentre l&#39;archiviazione locale o un cookie potrebbero conservare i dati.

### Comportamento dei visitatori

Simile a Informazioni pagina, questo elemento dati utilizza tipi di comportamento comuni per arricchire una logica all’interno di regole e altre soluzioni Platform.

Seleziona uno dei seguenti attributi di comportamento dei visitatori:

* Landing page
* Traffic source
* Minutes on site
* Session count
* Session page view count
* Lifetime page view count
* Is new visitor

Alcuni casi d&#39;uso comuni includono:

* Mostra un sondaggio dopo che un visitatore è stato sul sito per cinque minuti
* Se si tratta della pagina di destinazione della visita, compila una metrica Analytics
* Mostra una nuova offerta al visitatore dopo X conteggi delle sessioni
* Visualizza una newsletter per la prima volta, se si tratta di un nuovo visitatore

### Valore condizionale

Un wrapper per [Value Comparison](#value-comparison-value-comparison) condizione. In base al risultato del confronto, restituirà uno dei due valori disponibili nel modulo. Può quindi gestire &quot;If... Allora... Altrimenti...&quot; senza la necessità di ulteriori regole.

### Ambiente di runtime

Consente di selezionare una delle seguenti variabili:

* Fase dell’ambiente - Restituisce `_satellite.environment.stage` differenziare gli ambienti di sviluppo/staging/produzione.
* Data build libreria - Restituisce `turbine.buildInfo.buildDate` che contiene lo stesso valore come `_satellite.buildInfo.buildDate`.
* Nome proprietà - Restituisce `_satellite.property.name` per ottenere il nome della proprietà Launch.
* ID proprietà - Restituisce `_satellite.property.id` per ottenere l’ID della proprietà Launch
* Nome regola - Restituisce `event.$rule.name` contenente il nome della regola eseguita.
* ID regola - Restituisce `event.$rule.id` contenente l’ID della regola eseguita.
* Tipo evento - Restituisce `event.$type` contenente il tipo di evento che ha attivato la regola.
* Payload dei dettagli dell’evento - Restituisce `event.detail` contenente il payload di un evento personalizzato o di una regola di chiamata diretta.
* Identificatore di chiamata diretta - Restituisce `event.identifier` contenente l’identificatore di una regola di chiamata diretta.

### Attributi dispositivo

Restituisce uno dei seguenti attributi del dispositivo visitatore:

* Dimensioni finestra browser
* Dimensioni dello schermo

### Strumenti JavaScript

È un wrapper per le operazioni JavaScript più comuni. Riceve un elemento dati come input. Restituisce il risultato di una delle seguenti trasformazioni del valore dell’elemento dati:

* Manipolazione di base delle stringhe (replace, substring, regex match, first and last index, split, slice)
* Operazioni di base sull&#39;array (slice, join, pop, shift)
* Operazioni universali di base (sezione, lunghezza)