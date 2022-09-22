---
title: Estensione Google Data Layer
description: Scopri l’estensione tag Client Data Layer di Google in Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 6%

---

# Estensione Google Data Layer (Beta)

>[!IMPORTANT]
>
>Questa estensione è attualmente in versione beta e non è stata testata completamente in produzione.

L’estensione Google Data Layer consente di utilizzare un livello dati Google nell’implementazione dei tag. L&#39;estensione può essere utilizzata in modo indipendente o simultaneo con le soluzioni Google e con open source Google [Libreria di Data Layer Helper](https://github.com/google/data-layer-helper).

La libreria Helper fornisce funzionalità simili basate su eventi all’Adobe Client Data Dayer (ACDL). Gli elementi dati, le regole e le azioni dell&#39;estensione Google Data Layer forniscono funzionalità simili a quelle presenti in [Estensione ACDL](../client-data-layer/overview.md).

## Scadenza

La versione 1.0.x dell&#39;estensione è una versione beta. Questa estensione non è stata testata completamente in produzione.

## Installazione

Per installare l’estensione, passa al catalogo delle estensioni nell’interfaccia utente Raccolta dati e seleziona **Livello dati Google**.

Una volta installata, l&#39;estensione crea o accede a un livello di dati ogni volta che la libreria di tag viene caricata sul sito web.

## Vista delle estensioni

Durante la configurazione dell&#39;estensione (durante l&#39;installazione dell&#39;estensione o selezionando **[!UICONTROL Configura]** dal catalogo delle estensioni) è necessario definire il nome del livello dati utilizzato dall&#39;estensione. Se al caricamento della libreria non è presente alcun livello di dati con il nome configurato, l&#39;estensione ne crea uno.

>[!NOTE]
>
>Non importa se il codice Google o Adobe viene caricato per primo e crea il livello dati. Entrambi i sistemi creeranno il livello dati, se non presente, o utilizzeranno il livello dati esistente.

Per impostazione predefinita, il livello dati utilizza il nome predefinito di Google `dataLayer`.

## Eventi

L’estensione ti consente di rilevare le modifiche (eventi) all’interno del livello dati. Un evento può essere uno dei seguenti:

* Assegnare tag agli eventi (ad esempio una libreria caricata)
* Eventi JavaScript
* I dati inviati al livello dati con la `event` keyword.

È importante comprendere l&#39;uso [`event` keyword](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) quando i dati vengono inviati a un livello dati Google, in modo simile all’Adobe Client Data Layer. La `event` La parola chiave modifica il comportamento del livello dati Google e pertanto il comportamento dell’estensione viene aggiornato di conseguenza.

Le sezioni seguenti delineano i diversi tipi di evento che l&#39;estensione può rilevare.

### Ascoltare tutte le push al livello dati

Se selezioni questa opzione, l&#39;estensione ascolta qualsiasi modifica apportata al livello dati.

### Ascolta i messaggi push esclusi gli eventi

Se selezioni questa opzione, l’estensione ascolta tutto ciò che viene inviato al livello dati, esclusi gli eventi.

Il listener tiene traccia dell&#39;evento push di esempio seguente:

```js
dataLayer.push({"data":"something"})
```

Il listener non tiene traccia dei seguenti eventi push di esempio:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Ascolta tutti gli eventi

Se selezioni questa opzione, l’estensione ascolta qualsiasi evento inviato al livello dati.

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

Se desideri ascoltare un evento specifico, seleziona questa opzione in modo che il listener di eventi tenga traccia di tutti gli eventi che corrispondono a una stringa specifica.

Ad esempio, l’impostazione `myEvent` quando si utilizza questa configurazione determina il tracciamento del solo evento push seguente da parte del listener:

```js
dataLayer.push({"event":"myEvent"})
```

È inoltre possibile utilizzare una stringa regex per corrispondere ai nomi degli eventi. Ad esempio, l’impostazione `myEvent\d` tiene traccia degli eventi che iniziano con `myEvent` seguita da una cifra:

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Azioni

Le sezioni seguenti descrivono le diverse azioni che l&#39;estensione può eseguire quando viene inclusa in un [regola](../../../ui/managing-resources/rules.md).

### Invia a livello dati {#push-to-data-layer}

Questa azione invia il contenuto JSON al livello di dati stesso, rendendo possibile l’utilizzo di elementi dati direttamente nei payload JSON. Nell’editor JSON fornito è possibile fare riferimento agli elementi dati utilizzando la notazione percentuale (ad esempio, `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Reimpostazione Google DL su stato calcolato

>[!NOTE]
>
>Questa azione è disponibile dalla versione 1.0.5 in avanti.

Questa azione ripristina il livello dati. Se utilizzato in una regola che elabora una modifica del livello dati di Google, il livello dati viene reimpostato sullo stato calcolato del livello dati al momento dell&#39;attivazione della regola. Se l&#39;azione viene utilizzata in una regola che non elabora una modifica del livello dati di Google, l&#39;azione svuota il livello dati.

## Elementi dati

L&#39;estensione fornisce un elemento dati univoco che accede al livello dati utilizzando una chiave (ad esempio, `page.url` in [frammento sopra](#push-to-data-layer)).

L’elemento dati può fornire uno dei seguenti elementi:

* Un valore specifico dal livello dati (ad esempio, `page.url`)
* L’intero array del livello dati (campo chiave vuoto)
* Valori da un evento del livello dati utilizzando la chiave (se `event` parola chiave utilizzata)
* L&#39;intero oggetto evento (campo chiave vuoto)

L’estensione dà sempre priorità alle informazioni sull’evento. Se si utilizza un livello dati `event` in fase di elaborazione, i valori vengono sempre letti da tale evento. Se `event` non è presente, i valori vengono letti dal livello dati direttamente.

## Informazioni aggiuntive

Ulteriori informazioni sono disponibili nella sezione [README del progetto](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) e nelle finestre di dialogo dell’elemento dati e dell’evento dell’estensione.
