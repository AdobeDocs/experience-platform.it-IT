---
title: Estensione Adobe Client Data Layer
description: Scopri l’estensione per tag Adobe Client Data Layer in Adobe Experience Platform.
exl-id: c4d1b4d3-4b51-4701-be2e-31b08e109bf6
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 91%

---

# Estensione Adobe Client Data Layer

Questa documentazione fornisce esempi e best practice sull’utilizzo dell’estensione Adobe Client Data Layer.

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## Installazione

Per installare l’estensione, passa al catalogo delle estensioni nell’interfaccia utente di Experience Platform o nell’interfaccia utente di Data Collection e seleziona Adobe Client Data Layer.

![Visualizzazione dell’estensione ACDL nel catalogo](./images/catalog.png)

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## Visualizzazione dell’estensione

Per impostazione predefinita, lo script ACDL crea un nuovo livello dati con il nome della variabile `adobeDataLayer`. Se necessario, è possibile modificare questo nome nella visualizzazione dell’estensione. Al caricamento dei tag viene creata un’istanza del nome impostato.

>[!NOTE]
>
>Quando si modifica il nome dell’oggetto, viene comunque creata un&#39;istanza dell’oggetto originale `adobeDataLayer`, che viene quindi duplicata con il nuovo nome della variabile selezionato.

## Eventi

L’estensione permette di ascoltare gli eventi sul livello dati. Sono disponibili i seguenti eventi:

### Ascolta tutte le modifiche di dati

Se selezioni questa opzione, il listener di eventi ascolta qualsiasi modifica apportata al livello dati.

>[!IMPORTANT]
>
>Il push degli eventi non modifica il livello dati stesso.

Il listener tiene traccia degli eventi push di esempio seguenti:

* ` adobeDataLayer.push({"data":"something"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

Il listener non tiene traccia dell’evento push di esempio seguente:

* ` adobeDataLayer.push({"event":"myevent"})`

### Ascolta tutti gli eventi

Se selezioni questa opzione, il listener di eventi ascolta qualsiasi evento inviato al livello dati.

Il listener tiene traccia degli eventi push di esempio seguenti:

* ` adobeDataLayer.push({"event":"myevent"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

Il listener non tiene traccia dell’evento push di esempio seguente:

* ` adobeDataLayer.push({"data":"something"}) `

### Ascolta un evento specifico

Se specifichi un evento, il listener di eventi tiene traccia di tutti gli eventi che corrispondono a una stringa specifica.

Ad esempio, l’impostazione `myEvent` quando si utilizza questa configurazione determina il tracciamento del solo evento push seguente da parte del listener:

* `adobeDataLayer.push({"event":"myEvent"})`

Puoi anche modificare l’ambito del listener di eventi. Di seguito sono riepilogate le diverse opzioni:

* `all`: questa è l’opzione predefinita e attiva la regola ogni volta che la condizione selezionata sopra è stata soddisfatta in passato o verrà inviata in futuro. Questa è l’opzione più sicura se utilizzi un’implementazione asincrona.
* `future`: questa opzione attiva la regola solo quando i nuovi eventi push che corrispondono alla condizione vengono inviati al livello dati.
* `past`: questa opzione attiva la regola solo per i vecchi eventi push che corrispondono alla condizione. I nuovi push che corrispondono alla condizione vengono ignorati e non attivano più la regola.

## Azioni

Le sezioni seguenti descrivono le azioni supportate dall’estensione.

### Ripristina livello dati

L’estensione consente di reimpostare la lunghezza del livello dati, che può essere utile per mantenere una dimensione limitata per un’applicazione a pagina singola.

Tuttavia, attualmente non è possibile rimuovere completamente le informazioni impostate in precedenza durante i metodi push.

L’azione **Ripristina e imposta stato calcolato** copia l’ultimo stato calcolato, svuota l’oggetto livello dati e invia nuovamente l’ultimo stato.

### Invia a livello dati

L’estensione fornisce un’azione per inviare contenuti JSON al livello dati stesso. Questa azione consente di utilizzare elementi dati direttamente nel codice JSON. All’interno dell’editor JSON, è necessario fare riferimento agli elementi dati utilizzando la notazione percentuale (ad esempio, `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

## Elementi dati

Le sezioni seguenti descrivono i tipi di elementi dati univoci forniti dall’estensione.

### Stato calcolato

L’elemento dati Stato calcolato del livello dati può restituire uno di due elementi, a seconda di come lo configuri:

* Stato completo del livello dati: per impostazione predefinita, viene restituito lo stato calcolato completo del livello dati.
* Un percorso specifico: puoi specificare il percorso da restituire nel livello dati. I percorsi vengono specificati utilizzando la notazione del punto (ad esempio, `data.foo`).

### Dimensioni livello dati

Questo elemento dati restituisce le dimensioni del livello dati. La dimensione del livello dati è rappresentata dal numero di elementi inviati a questo oggetto.

Dato il seguente elenco di eventi push, questo elemento dati restituisce il numero intero `2`:

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
