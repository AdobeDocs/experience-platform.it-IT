---
title: Estensione Google Data Layer
description: Scopri l’estensione tag Client Data Layer di Google in Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 9c608f69f6ba219f9cb4e938a77bd4838158d42c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 13%

---

# Estensione Google Data Layer

L’estensione Google Data Layer consente di utilizzare un livello dati Google nell’implementazione dei tag. L&#39;estensione può essere utilizzata in modo indipendente o simultaneo con le soluzioni Google e con open source Google [Libreria di Data Layer Helper](https://github.com/google/data-layer-helper).

La libreria Helper fornisce funzionalità simili basate su eventi all’Adobe Client Data Dayer (ACDL). Gli elementi dati, le regole e le azioni dell&#39;estensione Google Data Layer forniscono funzionalità simili a quelle presenti in [Estensione ACDL](../client-data-layer/overview.md).

## Scadenza

La versione 1.2.x è una versione beta tardiva che è in uso in produzione.

## Installazione

Per installare l’estensione, passa al catalogo delle estensioni nell’interfaccia utente Raccolta dati e seleziona **[!UICONTROL Livello dati Google]**.

Una volta installata, l’estensione crea o accede a un livello di dati a ogni caricamento della libreria dei tag di Adobe Experience Platform.

## Vista delle estensioni

La configurazione dell&#39;estensione può essere utilizzata per definire il nome del livello dati utilizzato dall&#39;estensione. Se non è presente alcun livello di dati con il nome configurato al caricamento di Adobe Experience Platform Tags, l’estensione ne crea uno.

Il nome predefinito del livello dati è il nome predefinito di Google `dataLayer`.

>[!NOTE]
>
>Non importa se il codice Google o Adobe viene caricato per primo e crea il livello dati. Entrambi i sistemi si comportano allo stesso modo: crea il livello dati se non è presente o utilizza il livello dati esistente.

## Eventi

>[!NOTE]
>
>La parola _event_ viene sovraccaricato quando in Adobe Experience Platform Tags viene utilizzato un livello dati basato su eventi. _Eventi_ può essere:
> - Eventi Adobe Experience Platform Tags (Libreria caricata e così via).
> - Eventi JavaScript.
> - I dati inviati al livello dati con la _event_ keyword.


L’estensione ti offre la possibilità di ascoltare le modifiche apportate al livello dati.

>[!NOTE]
>
>È importante comprendere l&#39;uso _event_ parola chiave quando i dati vengono inviati a un livello di dati Google, in modo simile a Adobe Client Data Layer. La _event_ La parola chiave modifica il comportamento del livello dati Google e quindi questa estensione.\
> Leggi la documentazione Google o fai ricerche se non sei sicuro su questo punto.

### Ascoltare tutte le push al livello dati

Se selezioni questa opzione, il listener di eventi ascolta qualsiasi modifica apportata al livello dati.

### Ascolta i messaggi push esclusi gli eventi

Se selezioni questa opzione, il listener di eventi ascolta qualsiasi push di dati al livello dati, esclusi gli eventi.

Il listener tiene traccia degli eventi push di esempio seguenti:

```js
dataLayer.push({"data":"something"})
```

Il listener non tiene traccia dei seguenti eventi push di esempio:

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

Ad esempio, l&#39;impostazione &#39;myEvent\d&#39; viene tracciata `myEvent` con una cifra (\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Azioni

### Invia a livello dati {#push-to-data-layer}

L’estensione fornisce due azioni per inviare JSON al livello dati; un campo di testo libero per creare manualmente il JSON da inviare e, dalla versione 1.2.0, una finestra di dialogo multicampo chiave-valore.

#### Testo libero JSON

L’azione testo libero consente di utilizzare gli elementi dati direttamente nel JSON. All’interno dell’editor JSON, è necessario fare riferimento agli elementi dati utilizzando la notazione percentuale. Ad esempio: `%dataElementName%`.

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

#### Campo multiplo chiave-valore

La nuova finestra di dialogo a più campi chiave-valore è un’interfaccia più semplice da usare che consente di configurare un push senza scrivere manualmente JSON.

### Reimpostazione Google DL su stato calcolato

L’estensione fornisce un’azione per reimpostare il livello dati. Se utilizzato in una regola che elabora una modifica del livello dati di Google, il livello dati viene reimpostato sullo stato calcolato del livello dati al momento dell&#39;attivazione della regola. Se l&#39;azione viene utilizzata in una regola che non elabora una modifica del livello dati di Google, l&#39;azione svuota il livello dati.

## Elementi dati

L&#39;elemento dati fornito può essere utilizzato durante l&#39;esecuzione di una regola attivata da una modifica del livello dati di Google (evento push) o in una regola non correlata come Library Loaded. Nel primo caso, l&#39;elemento dati restituisce un valore tratto dallo stato calcolato al momento della modifica del livello dati. In quest&#39;ultimo caso, viene utilizzato lo stato calcolato al momento dell&#39;esecuzione della regola.

Un interruttore consente di selezionare se l’elemento dati deve restituire valori dall’intero stato calcolato o solo dalle informazioni sull’evento (se utilizzato in una regola attivata da una modifica del livello dati).

L’elemento dati può pertanto restituire:

- Campo vuoto: stato calcolato del livello dati.
- Campo con chiave (ad esempio page.previous_url nell’esempio precedente): valore della chiave nell&#39;oggetto evento o nello stato calcolato.

## Informazioni aggiuntive

Le finestre di dialogo dell&#39;elemento dati e dell&#39;evento dell&#39;estensione contengono informazioni di utilizzo ed esempi dettagliati.

Ulteriori informazioni generali sono disponibili nella sezione [README del progetto](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
