---
title: Estensione Google Data Layer
description: Scopri l’estensione tag Google Client Data Layer in Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: c61afdc2c3df98a0ef815d7cb034ba2907c52908
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 12%

---

# Estensione Google Data Layer

L’estensione Google Data Layer consente di utilizzare un livello dati Google nell’implementazione dei tag. L&#39;estensione può essere utilizzata in modo indipendente o simultaneo con le soluzioni Google e con open source di Google [Libreria helper livello dati](https://github.com/google/data-layer-helper).

La libreria helper fornisce funzionalità basate su eventi simili a quelle di Adobe Client Data Layer (ACDL). Gli elementi dati, le regole e le azioni dell’estensione Google Data Layer forniscono funzionalità simili a quelle della [Estensione ACDL](../client-data-layer/overview.md).

## Installazione

Per installare l’estensione, passa al catalogo delle estensioni nell’interfaccia utente di Data Collection e seleziona **[!UICONTROL Google Data Layer]**.

Una volta installata, l’estensione crea o accede a un livello dati a ogni caricamento della libreria Tag di Adobe Experience Platform.

## Vista dell’estensione

La configurazione dell’estensione può essere utilizzata per definire il nome del livello dati utilizzato dall’estensione. Se al momento del caricamento dei tag Adobe Experience Platform non è presente alcun livello di dati con il nome configurato, l’estensione ne crea uno.

Il nome predefinito del livello dati è il nome predefinito di Google `dataLayer`.

>[!NOTE]
>
>Non importa se il codice Google o Adobe viene caricato per primo e crea il livello dati. Entrambi i sistemi si comportano allo stesso modo: crea il livello dati se non è presente o utilizza il livello dati esistente.

## Eventi

>[!NOTE]
>
>La parola _evento_ viene sovraccaricato quando un livello dati basato su eventi viene utilizzato nei tag di Adobe Experience Platform. _Eventi_ può essere:
> - Eventi tag Adobe Experience Platform (libreria caricata e così via).
> - Eventi JavaScript.
> - Dati inviati al livello dati con _evento_ parola chiave.

L’estensione consente di ascoltare le modifiche sul livello dati.

>[!NOTE]
>
>È importante comprendere l&#39;uso del _evento_ parola chiave quando i dati vengono inviati a un livello dati di Google, in modo simile a Adobe Client Data Layer. Il _evento_ parola chiave modifica il comportamento del livello dati di Google e quindi di questa estensione.\
> Leggi la documentazione di Google o fai ricerche se non sei sicuro su questo punto.

### Tipi di evento Google

Google supporta due metodi per trasmettere gli eventi: Google Tag Manager, che utilizza `push()` e Google Analytics 4, utilizzando il `gtag()` metodo.

Le versioni di Google Data Layer precedenti alla 1.2.1 supportavano solo gli eventi creati da `push()`, come illustrato negli esempi di codice di questa pagina.

Le versioni 1.2.1 e successive supportano gli eventi creati con `gtag()`.  Questo è facoltativo e può essere abilitato nella finestra di dialogo di configurazione dell’estensione.

Per ulteriori informazioni su `push()` e `gtag()` eventi, consulta [Documentazione di Google](https://developers.google.com/analytics/devguides/collection/ga4/reference/events?client_type=gtag).  Le informazioni sono fornite anche nelle finestre di dialogo di configurazione e regola dell’estensione.

### Ascolta tutti i push al livello dati

Se selezioni questa opzione, il listener di eventi ascolta qualsiasi modifica apportata al livello dati.

### Ascolto di push con esclusione di eventi

Se selezioni questa opzione, il listener di eventi ascolta qualsiasi invio di dati al livello dati, esclusi gli eventi.

Il listener tiene traccia degli eventi push di esempio seguenti:

```js
dataLayer.push({"data":"something"})
```

Il listener non tiene traccia degli eventi push di esempio seguenti:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Ascolta tutti gli eventi

Se selezioni questa opzione, il listener di eventi ascolta qualsiasi evento inviato al livello dati.

Il listener tiene traccia degli eventi push di esempio seguenti:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

Il listener non tiene traccia dell’evento push di esempio seguente:

```js
dataLayer.push({"data":"something"})
```

### Ascolta un evento specifico

Se specifichi un evento, il listener di eventi tiene traccia di tutti gli eventi che corrispondono a una stringa specifica.

Ad esempio, l’impostazione `myEvent` quando si utilizza questa configurazione determina il tracciamento del solo evento push seguente da parte del listener:

```js
dataLayer.push({"event":"myEvent"})
```

È possibile utilizzare un regex (ECMAScript / JavaScript) per far corrispondere i nomi degli eventi.

Ad esempio, impostando &#39;myEvent\d&#39; si tiene traccia di `myEvent` con una cifra (\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Azioni

### Invia a livello dati {#push-to-data-layer}

L’estensione fornisce due azioni per inviare JSON al livello dati: un campo di testo libero per creare manualmente il JSON da inviare e, dalla versione 1.2.0, una finestra di dialogo con più campi chiave-valore.

#### JSON per testo libero

L’azione testo libero consente di utilizzare gli elementi dati direttamente nel JSON. All’interno dell’editor JSON, è necessario fare riferimento agli elementi dati utilizzando la notazione percentuale. Ad esempio, `%dataElementName%`.

```json
{
  "page": {
    "url": "%url%",
    "previous_url": "%previous_url%",
    "concatenated_values": "static string %dataElement%"
  }
}
```

#### Multifield chiave-valore

La nuova finestra di dialogo a più campi chiave-valore è un’interfaccia più intuitiva che consente di configurare un push senza scrivere manualmente JSON.

### Ripristino di Google DL allo stato calcolato

L’estensione fornisce un’azione per ripristinare il livello dati. Se utilizzato in una regola che elabora una modifica del livello dati di Google, il livello dati viene reimpostato sullo stato calcolato del livello dati nel momento in cui la regola è stata attivata. Se l’azione viene utilizzata in una regola che non elabora una modifica del livello dati di Google, l’azione svuota il livello dati.

## Elementi dati

L’elemento dati fornito può essere utilizzato durante l’esecuzione di una regola attivata da una modifica del livello dati di Google (evento push) o in una regola non correlata, ad esempio Library Loaded. Nel primo caso, l’elemento dati restituisce un valore tratto dallo stato calcolato al momento della modifica del livello dati. In quest’ultimo caso, viene utilizzato lo stato calcolato al momento dell’esecuzione della regola.

Un interruttore consente di selezionare se l’elemento dati deve restituire valori dall’intero stato calcolato o solo dalle informazioni sull’evento (se utilizzato in una regola attivata da una modifica del livello dati).

L’elemento dati può quindi restituire:

- Campo vuoto: stato calcolato del livello dati.
- Campo con chiave (come page.previous_url nell’esempio precedente): valore della chiave nell’oggetto evento o nello stato calcolato.

## Informazioni aggiuntive

L’elemento dati e le finestre di dialogo degli eventi dell’estensione contengono informazioni di utilizzo ed esempi dettagliati.

Ulteriori informazioni generali sono disponibili nella [LEGGIMI progetto](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
