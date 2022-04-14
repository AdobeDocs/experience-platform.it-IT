---
description: Experience Platform Destination SDK utilizza i modelli Pebble e consente di trasformare i dati esportati da Experience Platform nel formato richiesto dalla destinazione.
title: Funzioni di trasformazione supportate nella Destination SDK
source-git-commit: 840404741da06ba1593b227c7d6ba459b5f43110
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 3%

---

# Funzioni di trasformazione supportate nella Destination SDK

## Panoramica {#overview}

Experience Platform Destination SDK utilizza [[!DNL Pebble] modelli](https://pebbletemplates.io/), che consente di trasformare i dati esportati da Experience Platform nel formato richiesto dalla destinazione.

L&#39;Experience Platform [!DNL Pebble] l’implementazione presenta alcune modifiche rispetto alla versione standard fornita da [!DNL Pebble]. Inoltre, oltre alle funzioni predefinite fornite da [!DNL Pebble], Adobe ha creato alcune funzioni aggiuntive utilizzabili con Destination SDK.

## Dove utilizzare {#where-to-use}

Utilizza le funzioni supportate elencate di seguito in questa pagina quando [creazione di un modello di trasformazione dei messaggi](./create-template.md) per i dati esportati da Experience Platform alla destinazione. Il modello di trasformazione del messaggio viene utilizzato nel [configurazione del server di destinazione](./server-and-template-configuration.md) per le destinazioni di streaming.

## Prerequisiti {#prerequisites}

Per comprendere i concetti e le funzioni di questa pagina di riferimento, leggere il [formato messaggio](/help/destinations/destination-sdk/message-format.md) prima il documento. Devi capire il [struttura di un profilo](/help/destinations/destination-sdk/message-format.md#profile-structure) in Experience Platform prima di poter utilizzare [!DNL Pebble] modelli per trasformare e esportare i dati.

Prima di passare alle funzioni documentate di seguito, controlla gli esempi di modelli nella sezione [Utilizzo di un linguaggio di template per le trasformazioni di identità, attributi e appartenenza ai segmenti](/help/destinations/destination-sdk/message-format.md#using-templating). Gli esempi che ci sono iniziano molto semplici e aumentano la complessità.

## Supportato [!DNL Pebble] Funzioni {#supported-functions}

Da [!DNL Pebble] sezione tag, Destination SDK supporta solo:
* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [per](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Utilizzo `for` è diverso durante l’iterazione attraverso *array* o *map* elementi in un modello. Quando si esegue l&#39;iterazione attraverso un array, è possibile ottenere l&#39;elemento direttamente. Quando si esegue l&#39;iterazione attraverso una mappa, si ottiene ogni voce mappa, che ha una coppia chiave-valore.
>
> * Per un esempio di un elemento array, considera le identità in un [identityMap](./message-format.md#identities) spazio dei nomi, in cui è possibile eseguire iterazioni attraverso elementi quali `identityMap.gaid`, `identityMap.email`o simili.
> * Per un esempio di elemento mappa, pensa [segmentMembership](./message-format.md#segment-membership).


Da [!DNL Pebble] sezione filtro, Destination SDK supporta tutte le funzioni. Un esempio ulteriore qui di seguito mostra come `date` può essere utilizzata all&#39;interno della Destination SDK.

Da [!DNL Pebble] sezione funzioni, Adobe sì *not* supportano [gamma](https://pebbletemplates.io/wiki/function/range/) funzione .

## Esempio di come `date` viene utilizzata la funzione {#date-function}

Per esemplificare come [!DNL Pebble] le funzioni sono utilizzate nella Destination SDK, vedi sotto come la funzione data ([link nella documentazione di Pebble](https://pebbletemplates.io/wiki/filter/date/)) viene utilizzato per trasformare il formato di una marca temporale.

### Caso d’uso

Vuoi cambiare il `lastQualificationTime` timestamp dal valore predefinito [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) valore esportato da Experience Platform in un altro valore preferito dalla destinazione.

### Esempio

#### Ingresso

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### Formato

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### Output

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Funzioni aggiunte dall’Adobe {#functions-added-by-adobe}

Oltre alle funzioni predefinite fornite da [!DNL Pebble], vedi di seguito le funzioni aggiuntive create da Adobe che puoi utilizzare per le esportazioni di dati.

### `addedSegments` e `removedSegments` Funzioni {#addedsegments-removedsegments-functions}

#### Caso d’uso

Puoi utilizzare queste funzioni per ottenere un elenco di segmenti che sono stati aggiunti o rimossi da un profilo.

#### Esempio

##### Ingresso

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Formato

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### Uscita

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed segments filters {#added-and-removed-segmnts-filters}

#### Use case {#use-case}

These filters are similar to `addedSegments` and `removedSegments`, described above. The only difference is that they are implemented as filters as opposed to functions.

#### Example {#example}

##### Input {#input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format {#format}

```java
added: {% for s in input.profile.segmentMembership.ups | added %}<{{s.key}}>{% endfor %};|removed: {% for s in input.profile.segmentMembership.ups | removed %}<{{s.key}}>{% endfor %};
```

##### Output {#output}

```json
added: <111111><333333>;|removed: <222222>;
```

-->

## Passaggi successivi {#next-steps}

Ora sai quale [!DNL Pebble] Le funzioni sono supportate in Destination SDK e come utilizzarle per regolare il formato dei dati esportati in base alle tue esigenze. Quindi, devi rivedere le pagine seguenti:

* [Creare e testare un modello di trasformazione dei messaggi](/help/destinations/destination-sdk/create-template.md)
* [Operazioni API per i modelli di rendering](/help/destinations/destination-sdk/render-template-api.md)