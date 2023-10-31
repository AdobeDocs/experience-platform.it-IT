---
description: Experienci Platform Destination SDK utilizza i modelli Pebble, che consentono di trasformare i dati esportati da Experienci Platform nel formato richiesto dalla destinazione.
title: Funzioni di trasformazione supportate in Destination SDK
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 2%

---

# Funzioni di trasformazione supportate in Destination SDK

Experience Platform utilizzi Destination SDK [[!DNL Pebble] modelli](https://pebbletemplates.io/), che consente di trasformare i dati esportati da Experienci Platform nel formato richiesto dalla destinazione.

L’Experience Platform [!DNL Pebble] presenta alcune modifiche rispetto alla versione preconfigurata fornita da [!DNL Pebble]. Inoltre, oltre alle funzioni pronte all’uso fornite da [!DNL Pebble], Adobe ha creato alcune funzioni aggiuntive che è possibile utilizzare con Destination SDK.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Dove utilizzare {#where-to-use}

Utilizza le funzioni supportate elencate di seguito in questa pagina quando [creazione di un modello di trasformazione dei messaggi](../../testing-api/streaming-destinations/create-template.md) per i dati esportati da Experienci Platform nella destinazione.

Il modello di trasformazione del messaggio viene utilizzato nel [configurazione del server di destinazione](templating-specs.md) per le destinazioni di streaming.

## Prerequisiti {#prerequisites}

Per comprendere i concetti e le funzioni di questa pagina di riferimento, leggere [formato del messaggio](message-format.md) documento. È necessario comprendere [struttura di un profilo](message-format.md#profile-structure) nell’Experience Platform prima di poter utilizzare [!DNL Pebble] i modelli da trasformare e i dati esportati.

Prima di passare alle funzioni descritte di seguito, consulta gli esempi di modelli disponibili nella sezione. [Utilizzo di un linguaggio per modelli per le trasformazioni di identità, attributi e appartenenza a un pubblico](message-format.md#using-templating). Gli esempi qui presenti iniziano con una struttura molto semplice e aumentano di complessità.

## Supportato [!DNL Pebble] funzioni {#supported-functions}

Dalla sezione [!DNL Pebble] sezione tag, Destination SDK supporta solo:

* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [per](https://pebbletemplates.io/wiki/tag/for/)
* [se](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Utilizzo di `for` è diverso quando si esegue l’iterazione *array* o *mappa* elementi in un modello. Quando esegui l’iterazione attraverso un array, puoi ottenere direttamente l’elemento. Quando si esegue l&#39;iterazione di una mappa, si ottiene ogni voce della mappa che ha una coppia chiave-valore.
>
> * Per un esempio di un elemento array, pensa alle identità in un [identityMap](message-format.md#identities) spazio dei nomi, in cui è possibile eseguire iterazioni tra elementi quali `identityMap.gaid`, `identityMap.email`, o simili.
> * Per un esempio di un elemento mappa, pensa a [segmentMembership](message-format.md#segment-membership).

Dalla sezione [!DNL Pebble] filtro, la Destination SDK supporta tutte le funzioni. Un esempio più avanti mostra come `date` può essere utilizzata all&#39;interno di Destination SDK.

Dalla sezione [!DNL Pebble] funzioni, l’Adobe esegue *non* supportare [intervallo](https://pebbletemplates.io/wiki/function/range/) funzione.

## Esempio di come `date` viene utilizzata la funzione {#date-function}

Per esemplificare come [!DNL Pebble] le funzioni vengono utilizzate nella Destination SDK, vedi di seguito come funziona la data ([collegamento nella documentazione di Pebble](https://pebbletemplates.io/wiki/filter/date/)) viene utilizzato per trasformare il formato di una marca temporale.

### Caso d’uso

Si desidera modificare il `lastQualificationTime` timestamp dal valore predefinito [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) valore esportato da Experienci Platform in un altro valore preferito dalla destinazione.

### Esempio

#### Input

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

## Funzioni aggiunte da Adobe {#functions-added-by-adobe}

Oltre alle funzioni predefinite fornite da [!DNL Pebble], vedi di seguito le funzioni aggiuntive create da Adobe che puoi utilizzare per le esportazioni di dati.

### `addedSegments` e `removedSegments` funzioni {#addedsegments-removedsegments-functions}

#### Caso d’uso

Queste funzioni possono essere utilizzate per ottenere un elenco dei tipi di pubblico che sono stati aggiunti o rimossi da un profilo.

#### Esempio

##### Input

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

##### Output

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed audiences filters {#added-and-removed-segmnts-filters}

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

Ora sai quale [!DNL Pebble] Le funzioni di sono supportate in Destination SDK e come utilizzarle per regolare il formato dei dati esportati in base alle tue esigenze. Quindi, controlla le pagine seguenti:

* [Creare e testare un modello di trasformazione dei messaggi](../../testing-api/streaming-destinations/create-template.md)
* [Operazioni API del modello di rendering](../../testing-api/streaming-destinations/render-template-api.md)
