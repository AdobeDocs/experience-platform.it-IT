---
title: Elementi dati
description: Gli elementi dati sono i blocchi costitutivi per il dizionario dati (o mappa dati). Utilizza elementi dati per raccogliere, organizzare e distribuire dati in tutta la tecnologia marketing e pubblicitaria.
source-git-commit: 010e05968f1d7ad5675b0f0af43d9cfcc1f3a2ff
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 78%

---

# Elementi dati

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Gli elementi dati sono i blocchi costitutivi per il dizionario dati (o mappa dati). Utilizza elementi dati per raccogliere, organizzare e distribuire dati in tutta la tecnologia marketing e pubblicitaria.

Un singolo elemento dati è una variabile il cui valore può essere mappato alle stringhe di query, agli URL, ai valori dei cookie, alle variabili JavaScript e così via. È possibile fare riferimento a questo valore in base al nome della variabile in Adobe Experience Platform. Questa raccolta di elementi dati diventa il dizionario dati definiti che è possibile utilizzare per creare le regole (eventi, condizioni e azioni). Questo dizionario dati viene condiviso tra i tag per l&#39;utilizzo con qualsiasi estensione aggiunta alla proprietà.

>[!IMPORTANT]
>
>Le modifiche diventano effettive solo dopo la loro [pubblicazione](../publishing/overview.md).

Durante la creazione di regole è possibile utilizzare gli elementi dati il più possibile per consolidare la definizione dei dati dinamici e migliorare l&#39;efficienza dei processi di gestione dei tag. Puoi definire le regole dati una volta e poi utilizzarle in più posizioni.

Il concetto di elementi dati riutilizzabili è molto potente e dovrebbe essere utilizzato come best practice.

Ad esempio, se esiste un modo particolare con cui fai riferimento a nomi di pagina o ID prodotto o acquisisci informazioni dai parametri delle stringhe query da un collegamento di marketing affiliato o da [!DNL AdWords] e così via, puoi creare un dizionario dati (elementi dati) ottenendo informazioni dalla sua origine e quindi utilizzarli in varie regole di tag.

Utilizzando il nome della pagina come esempio, supponi di utilizzare uno schema specifico per il nome della pagina facendo riferimento a un livello di dati, un elemento `document.title` o un tag titolo all&#39;interno del sito Web. I tag in Adobe Experience Platform ti consentono di creare un elemento dati come singolo punto di riferimento per quel particolare punto di dati. Puoi quindi utilizzare questo elemento dati in qualsiasi regola che debba fare riferimento al nome della pagina. Se per qualche motivo decidi di cambiare il modo in cui si fa riferimento al nome della pagina (ad esempio, finora hai fatto riferimento a `document.title`, ma adesso vuoi farlo a un particolare livello di dati), non è necessario cambiare molte regole diverse per modificare tale riferimento. È sufficiente modificare il riferimento una volta nell&#39;elemento dati e tutte le regole che fanno riferimento a tale elemento dati vengono aggiornate automaticamente.

>[!NOTE]
>
>Se in una regola non viene fatto riferimento a un elemento dati, esso non viene caricato su alcuna pagina, se non specificamente chiamato nello script personalizzato.

Gli elementi dati sono compilati con dati quando sono utilizzati in regole o se vengono chiamati manualmente in uno script. A un livello avanzato:

1. [Crea un elemento dati](#create-a-data-element), se non lo hai già fatto.
1. Utilizza l&#39;elemento dati in una [regola](./rules.md) o in uno script personalizzato.

## Uso degli elementi dati

### Nelle regole

Puoi utilizzare elementi dati nell&#39;interfaccia di modifica delle regole utilizzando la casella di ricerca per trovare il nome dell&#39;elemento dati.

### Nello script personalizzato

Puoi utilizzare gli elementi dati negli script personalizzati utilizzando la sintassi dell&#39;oggetto `_satellite`:

`_satellite.getVar('data element name');`

## Creare un elemento dati {#create-a-data-element}

Gli elementi dati sono i blocchi di creazione per le regole. Gli elementi dati consentono di creare un dizionario dati (o mappa dati) degli elementi comunemente utilizzati su una pagina, indipendentemente da dove si trovano (stringhe, URL o valori cookie) per qualsiasi oggetto contenuto sul sito.

1. Da una pagina Proprietà, apri la scheda [!UICONTROL Elementi dati], quindi seleziona **[!UICONTROL Crea nuovo elemento dati]**.
1. Denomina l&#39;elemento dati.
1. Seleziona un&#39;estensione e digita.

   I tipi di elementi dati disponibili sono determinati dall&#39;estensione. Per informazioni sui tipi disponibili con l&#39;estensione tag core, consulta [Tipi di elementi dati](data-elements.md#types-of-data-elements).

1. Fornisci tutte le informazioni necessarie sul tipo scelto nei campi forniti.
1. (Facoltativo) Immetti un valore predefinito.

   Se non si seleziona questa opzione, non è presente alcun valore predefinito. La maggior parte degli utenti può lasciare l’impostazione predefinita. Vari sistemi trattano in modo diverso una variabile vuota. Alcuni utenti scelgono di inserire qualcosa tipo “none” o “n/a”, per coerenza nei rapporti nelle situazioni in cui l’elemento dati non restituisce un valore.

1. Seleziona se imporre un valore minuscolo e se rimuovere interruzioni di riga e spazi.
1. Seleziona una durata.

   Le scelte disponibili sono:

   * None
      * Il valore non è memorizzato.
   * Page view
      * Il valore viene tenuto in una variabile JavaScript fino a quando la pagina viene aggiornata o viene caricata una nuova pagina.
      * Può essere creato e impostato negli script utilizzando la sintassi dell&#39;oggetto `_satellite`:

         `_satellite.setVar('data_element_name')`
   * Session
      * I valori rimangono memorizzati nella memoria della sessione del browser fino alla chiusura della scheda del browser.
      * Disponibile tramite visita del sito.
   * Visitor
      * Il valore viene memorizzato indefinitamente nell&#39;archivio locale del browser.

1. Seleziona **[!UICONTROL Salva]**.

Quando crei o modifichi elementi, puoi salvarli e generarli nella [libreria attiva](../publishing/libraries.md#active-library). In questo modo la tua libreria viene salvata immediatamente e viene eseguita una build. Viene visualizzato lo stato della build. Puoi anche creare una nuova libreria dal menu a discesa [!UICONTROL Libreria attiva] .

## Tipi di elementi dati {#types-of-data-elements}

I tipi di elementi dati sono determinati dall&#39;estensione. Non vi sono limiti ai tipi che è possibile creare.

Nelle sezioni seguenti sono descritti i tipi di elementi dati disponibili nell&#39;estensione Core. Altre estensioni utilizzano altri tipi di elementi dati.

### Cookie

A qualsiasi cookie di dominio può essere fatto riferimento nel campo del nome del cookie.

#### Esempio:

`cookieName`

### Custom Code

Per inserire nell’interfaccia utente un codice JavaScript personalizzato, fai clic su [!UICONTROL Apri editor] e inserisci il codice nella finestra dell’editor.

Nella finestra dell&#39;editor è necessaria un&#39;istruzione return per indicare quale valore deve essere impostato come valore dell&#39;elemento dati. Se non è inclusa un’istruzione return, l’elemento dati viene risolto con `undefined`. In questo modo viene attivato il fallback per cercare un valore memorizzato e quindi un valore predefinito, qualora non sia presente alcun valore memorizzato.

**Esempio:**

```text
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Il codice personalizzato può accettare l’oggetto `event` dalla regola chiamante come argomento. Questo consente al codice di leggere il valore qui.

**Esempio:**

```text
// `event` is the default object provided by the rule
var eventType = event.$type;
return eventType; // if this data element is called from a "DOM Ready" event, then `core.dom-ready` is returned
```

Puoi utilizzarlo negli script personalizzati con la sintassi dell’oggetto `_satellite`:

`_satellite.getVar('data element name', event);`

Quando utilizzi la notazione `%..%` , devi solo specificare il nome dell’elemento dati. Non c’è bisogno di specificare `event`.

`%data element name%`

### DOM attribute

Qualsiasi valore di elemento può essere recuperato, ad esempio un tag div o H1.

#### Esempio:

CSS Selector Chain:

`id#dc logo img`

Ottieni il valore di:

`src`

### Variabile JavaScript

È possibile fare riferimento a qualsiasi oggetto o variabile JavaScript disponibile utilizzando il campo path.

Se desideri raccogliere variabili JavaScript o proprietà di oggetto nel markup e utilizzarle con una qualsiasi delle tue estensioni o regole, puoi utilizzare elementi dati per acquisire questi valori. In questo modo, puoi fare riferimento all’elemento dati in tutte le tue regole e, se l’origine dei dati dovesse cambiare, devi solo modificare il riferimento all’origine (l’elemento dati) in un’unica posizione nell’interfaccia utente Raccolta dati.

Ad esempio, supponiamo che il markup contenga una variabile JavaScript denominata `Page_Name`, come segue:

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Quando crei l’elemento dati, devi fornire il percorso di tale variabile.

Se utilizzi un oggetto raccolta dati come parte del livello dati, è sufficiente utilizzare la notazione del punto nel percorso per fare riferimento all&#39;oggetto e alla proprietà che desideri acquisire nell&#39;elemento dati, come `_myData.pageName`, o `digitalData.pageName`, ecc.

#### Esempio:

`window.document.title`

### Local storage

Immetti il nome dell’elemento di archiviazione locale nel campo [!UICONTROL Nome elemento di archiviazione locale].

La memorizzazione locale offre ai browser un modo per memorizzare informazioni da pagina a pagina ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). L&#39;archiviazione locale funziona molto come i cookie, ma è molto più grande e flessibile.

Utilizza il campo fornito per specificare il valore creato per un elemento di archiviazione locale, ad esempio `lastProductViewed.`

### Informazioni pagina

Utilizza questi punti dati per acquisire informazioni di pagina da utilizzare nella logica della regola o per inviare informazioni a [!DNL Analytics] sistemi di tracciamento esterni.

Puoi selezionare uno dei seguenti attributi di pagina da utilizzare nell&#39;elemento dati:

* URL
* Hostname
* Pathname
* Protocol
* Referrer
* Title

### Query String Parameter

Specifica un parametro URL singolo nel campo [!UICONTROL Parametro URL].

È necessaria solo la sezione name ed eventuali designatori speciali come “?” o “=” devono essere omessi.

#### Esempio:

`contentType`

### Numero casuale

Utilizza questo elemento dati per generare un numero casuale. Spesso viene utilizzato per campionare dati o creare ID, ad esempio un Hit ID. Il numero casuale può essere usato per oscurare o alterare i dati sensibili. Alcuni esempi possono includere:

* Generare un Hit ID
* Concatenare il numero a un token utente o a una marca temporale per garantire l&#39;univocità
* Eseguire un hash unidirezionale sui dati PII
* Decidere in modo casuale quando visualizzare una richiesta sondaggio sul sito

Specifica i valori minimo e massimo per il numero casuale.

**Valori predefiniti:**

Minimo: 0

Massimo: 1000000000

### Session storage

Immetti il nome dell’elemento di archiviazione sessione nel campo [!UICONTROL Nome elemento di archiviazione sessione]

L&#39;archiviazione della sessione è simile all&#39;archiviazione locale, fatta eccezione per i dati che vengono eliminati al termine della sessione, mentre l&#39;archiviazione locale o un cookie potrebbero conservare i dati.

### Comportamento dei visitatori

Simile a Informazioni pagina, questo elemento dati utilizza tipi di comportamento comuni per arricchire la logica all’interno di regole o altre soluzioni Platform.

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
* Se si tratta della pagina di destinazione della visita, compila una metrica [!DNL Analytics]
* Mostra una nuova offerta al visitatore dopo X conteggi delle sessioni
* Visualizza una newsletter registrata se si tratta di un nuovo visitatore

## Elementi dati incorporati

È necessario creare un elemento dati personalizzato nell’interfaccia utente Raccolta dati se in precedenza si utilizzava uno dei seguenti elementi dati:

* URI
* Protocollo
* Hostname
