---
title: Estensione Google Data Layer
description: Scopri l’estensione tag Google Client Data Layer in Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 6%

---

# Estensione Google Data Layer (Beta)

>[!IMPORTANT]
>
>Questa estensione è attualmente in versione beta e non è stata completamente testata in produzione.

L’estensione Google Data Layer consente di utilizzare un livello dati Google nell’implementazione dei tag. L&#39;estensione può essere utilizzata in modo indipendente o simultaneo con le soluzioni Google e con open source di Google [Libreria helper livello dati](https://github.com/google/data-layer-helper).

La libreria helper offre funzionalità basate su eventi simili a quelle di Adobe Client Data Dayer (ACDL). Gli elementi dati, le regole e le azioni dell’estensione Google Data Layer forniscono funzionalità simili a quelle della [Estensione ACDL](../client-data-layer/overview.md).

## Maturità

La versione 1.0.x dell&#39;estensione è una versione beta. Questa estensione non è stata completamente testata in produzione.

## Installazione

Per installare l’estensione, passa al catalogo delle estensioni nell’interfaccia utente di Experience Platform o nell’interfaccia utente di Data Collection e seleziona **Google Data Layer**.

Una volta installata, l’estensione crea o accede a un livello dati ogni volta che la libreria di tag viene caricata sul sito web.

## Vista dell’estensione

Durante la configurazione dell&#39;estensione (durante l&#39;installazione dell&#39;estensione o selezionando **[!UICONTROL Configura]** dal catalogo delle estensioni) è necessario definire il nome del livello dati utilizzato dall’estensione. Se al momento del caricamento della libreria non è presente alcun livello di dati con il nome configurato, l’estensione ne crea uno.

>[!NOTE]
>
>Non importa se il codice Google o Adobe viene caricato per primo e crea il livello dati. Entrambi i sistemi creeranno il livello dati se non presente, oppure utilizzeranno il livello dati esistente.

Per impostazione predefinita, il livello dati utilizza il nome predefinito di Google `dataLayer`.

## Eventi

L’estensione consente di ascoltare le modifiche (eventi) all’interno del livello dati. Un evento può essere uno dei seguenti:

* Assegnare tag agli eventi (ad esempio, una libreria in fase di caricamento)
* Eventi JavaScript
* Dati inviati al livello dati con `event` parola chiave.

È importante comprendere l&#39;uso del [`event` parola chiave](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) quando i dati vengono inviati a un livello dati di Google, in modo simile a Adobe Client Data Layer. Il `event` la parola chiave cambia il comportamento di Google data layer e, di conseguenza, il comportamento dell’estensione viene aggiornato di conseguenza.

Le sezioni seguenti descrivono i diversi tipi di eventi che l’estensione può intercettare.

### Ascolta tutti i push al livello dati

Se selezioni questa opzione, l’estensione ascolta qualsiasi modifica apportata al livello dati.

### Ascolto di push con esclusione di eventi

Se selezioni questa opzione, l’estensione resta in ascolto di qualsiasi elemento inviato al livello dati, esclusi gli eventi.

Il listener tiene traccia dell’evento push di esempio seguente:

```js
dataLayer.push({"data":"something"})
```

Il listener non tiene traccia degli eventi push di esempio seguenti:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Ascolta tutti gli eventi

Se selezioni questa opzione, l’estensione rimane in ascolto di qualsiasi evento inviato al livello dati.

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

Se desideri ascoltare un evento specifico, seleziona questa opzione affinché il listener di eventi tenga traccia di tutti gli eventi che corrispondono a una stringa specifica.

Ad esempio, l’impostazione `myEvent` quando si utilizza questa configurazione determina il tracciamento del solo evento push seguente da parte del listener:

```js
dataLayer.push({"event":"myEvent"})
```

Puoi anche utilizzare una stringa regex per far corrispondere i nomi degli eventi. Ad esempio, l&#39;impostazione `myEvent\d` tiene traccia degli eventi che iniziano con `myEvent` seguito da una cifra:

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Azioni

Le sezioni seguenti descrivono le diverse azioni che l’estensione può eseguire quando inclusa in un [regola](../../../ui/managing-resources/rules.md).

### Invia a livello dati {#push-to-data-layer}

Questa azione invia il contenuto JSON al livello dati stesso, rendendo possibile utilizzare gli elementi dati direttamente nei payload JSON. All’interno dell’editor JSON fornito, puoi fare riferimento agli elementi dati utilizzando la notazione percentuale (ad esempio, `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Ripristino di Google DL allo stato calcolato

>[!NOTE]
>
>Questa azione è disponibile dalla versione 1.0.5 in poi.

Questa azione ripristina il livello dati. Se utilizzato in una regola che elabora una modifica del livello dati di Google, il livello dati viene reimpostato sullo stato calcolato del livello dati nel momento in cui la regola è stata attivata. Se l’azione viene utilizzata in una regola che non elabora una modifica del livello dati di Google, l’azione svuota il livello dati.

## Elementi dati

L’estensione fornisce un elemento dati univoco che accede al livello dati utilizzando una chiave (ad esempio, `page.url` nel [frammento sopra](#push-to-data-layer)).

L’elemento dati può fornire uno dei seguenti elementi:

* Un valore specifico dal livello dati (ad esempio, `page.url`)
* L’intero array di livello dati (campo chiave vuoto)
* Valori da un evento di livello dati utilizzando la chiave (se `event` parola chiave utilizzata)
* L’intero oggetto evento (campo chiave vuoto)

L&#39;estensione dà sempre la priorità alle informazioni sull&#39;evento. Se un livello dati `event` è in fase di elaborazione, i valori vengono sempre letti da tale evento. Se un `event` non è presente, i valori vengono letti direttamente dal livello dati.

## Informazioni aggiuntive

Ulteriori informazioni sono disponibili nella sezione [LEGGIMI progetto](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) e nelle finestre di dialogo degli eventi e degli elementi dati dell’estensione.
