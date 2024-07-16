---
description: Experience Platform Destination SDK utilizza i modelli Pebble, che consentono di trasformare i dati esportati da Experience Platform nel formato richiesto dalla destinazione.
title: Funzioni di trasformazione supportate in Destination SDK
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# Funzioni di trasformazione supportate in Destination SDK

Experience Platform Destination SDK utilizza [[!DNL Pebble] modelli](https://pebbletemplates.io/), che consentono di trasformare i dati esportati da Experience Platform nel formato richiesto dalla destinazione.

L&#39;implementazione di Experience Platform [!DNL Pebble] presenta alcune modifiche rispetto alla versione preconfigurata fornita da [!DNL Pebble]. Inoltre, oltre alle funzioni predefinite fornite da [!DNL Pebble], Adobe ha creato alcune funzioni aggiuntive che è possibile utilizzare con Destination SDK.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Dove utilizzare {#where-to-use}

Utilizza le funzioni supportate elencate di seguito in questa pagina quando [crei un modello di trasformazione dei messaggi](../../testing-api/streaming-destinations/create-template.md) per i dati esportati da Experience Platform nella tua destinazione.

Il modello di trasformazione dei messaggi viene utilizzato nella [configurazione del server di destinazione](templating-specs.md) per le destinazioni di streaming.

## Prerequisiti {#prerequisites}

Per comprendere i concetti e le funzioni di questa pagina di riferimento, leggere prima il documento [message format](message-format.md). È necessario conoscere la struttura [ di un profilo](message-format.md#profile-structure) in Experience Platform prima di poter utilizzare i modelli [!DNL Pebble] per trasformare e i dati esportati.

Prima di passare alle funzioni descritte di seguito, esaminare gli esempi di modelli nella sezione [Utilizzo di un linguaggio di modelli per le trasformazioni di identità, attributi e appartenenza a un pubblico](message-format.md#using-templating). Gli esempi qui presenti iniziano con una struttura molto semplice e aumentano di complessità.

## Funzioni [!DNL Pebble] supportate {#supported-functions}

Dalla sezione dei tag [!DNL Pebble], Destination SDK supporta solo:

* [filtro](https://pebbletemplates.io/wiki/tag/filter/)
* [per](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>L&#39;utilizzo di `for` è diverso quando si esegue l&#39;iterazione tra gli elementi *array* o *map* in un modello. Quando esegui l’iterazione attraverso un array, puoi ottenere direttamente l’elemento. Quando si esegue l&#39;iterazione di una mappa, si ottiene ogni voce della mappa che ha una coppia chiave-valore.
>
> * Per un esempio di elemento array, considera le identità in uno spazio dei nomi [identityMap](message-format.md#identities), dove è possibile eseguire iterazioni tra elementi come `identityMap.gaid`, `identityMap.email` o simili.
> * Per un esempio di elemento mappa, pensa a [segmentMembership](message-format.md#segment-membership).

Dalla sezione del filtro [!DNL Pebble], Destination SDK supporta tutte le funzioni. Un esempio più avanti mostra come la funzione `date` può essere utilizzata all&#39;interno di Destination SDK.

Dalla sezione delle funzioni [!DNL Pebble], Adobe non supporta *not* la funzione [range](https://pebbletemplates.io/wiki/function/range/).

## Esempio di utilizzo della funzione `date` {#date-function}

Per esemplificare l&#39;utilizzo di [!DNL Pebble] funzioni in Destination SDK, vedere di seguito come viene utilizzata la funzione data ([link nella documentazione di Pebble](https://pebbletemplates.io/wiki/filter/date/)) per trasformare il formato di una marca temporale.

### Caso d’uso

Si desidera modificare il timestamp `lastQualificationTime` dal valore predefinito [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) che Experience Platform esporta in un altro valore preferito dalla destinazione.

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

Oltre alle funzioni predefinite fornite da [!DNL Pebble], vedere di seguito le funzioni aggiuntive create da Adobe che è possibile utilizzare per le esportazioni di dati.

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

Ora si sa quali funzioni di [!DNL Pebble] sono supportate in Destination SDK e come utilizzarle per adattare il formato dei dati esportati alle proprie esigenze. Quindi, controlla le pagine seguenti:

* [Creare e testare un modello di trasformazione dei messaggi](../../testing-api/streaming-destinations/create-template.md)
* [Operazioni API del modello di rendering](../../testing-api/streaming-destinations/render-template-api.md)
