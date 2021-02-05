---
keywords: Experience Platform ;home;argomenti più comuni;PQL;pql;lingua query profilo
solution: Experience Platform
title: Panoramica della lingua query profilo (PQL, Profile Query Language)
topic: developer guide
description: Questa guida fornisce una panoramica generale del linguaggio PQL, con linee guida per la formattazione e con espressioni PQL di esempio.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---


# [!DNL Profile Query Language] Panoramica (PQL)

[!DNL Profile Query Language] (PQL) è un linguaggio di query conforme a  [!DNL Experience Data Model] (XDM) progettato per supportare la definizione e l&#39;esecuzione di query di segmentazione per  [!DNL Real-time Customer Profile] i dati.

Questa guida fornisce una panoramica generale del linguaggio PQL, con linee guida per la formattazione e con espressioni PQL di esempio.

## Formattazione query PQL

Le query PQL hanno la firma seguente:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

Il parametro di input può essere un semplice carattere primitivo, ad esempio un valore booleano o una stringa, oppure un tipo più complesso, ad esempio un oggetto, un array o una mappa.

Esistono tre modi diversi per fare riferimento ai parametri di input all&#39;interno del corpo di un&#39;espressione PQL:

### Riferimento implicito al primo parametro

Nell&#39;esempio seguente, poiché il primo parametro è sempre contestuale, è possibile farvi direttamente riferimento da una proprietà (`homeAddress`).

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Riferimento esplicito al primo parametro

Nell&#39;esempio seguente, `$1` fa riferimento al primo parametro. Di conseguenza, `$2` fa riferimento al secondo parametro, ecc.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Utilizzo di variabili denominate, utilizzando la notazione lambda

Nell&#39;esempio seguente, `Profile` è un nome di variabile, che può essere scelto dall&#39;autore della query.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Valori letterali PQL

PQL supporta i seguenti tipi letterali:

| Letterale | Definizione | Esempio |
| ------- | ---------- | ------- |
| Stringa | Un tipo di dati composto da caratteri racchiusi tra virgolette doppie. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booleano | Tipo di dati vero o falso. | `true`, `false` |
| Intero | Tipo di dati che rappresenta un numero intero. Può essere positivo, negativo o zero. | `-201`,  `0`,  `412` |
| Doppio | Un tipo di dati che rappresenta qualsiasi numero reale. Può essere positivo, negativo o zero. | `-51.24`,  `3.14`,  `0.6942058` |
| Data | Tipo di dati che può essere utilizzato per creare date basate su anno, mese e giorno come parametri interi. È formattato come `date(year, month, day)` | `date(2020, 3, 14)` |
| Matrice | Tipo di dati composto da un gruppo di altri valori letterali. Utilizza parentesi quadre per raggruppare e virgole per delimitare valori diversi. <br> **Nota:** non è possibile accedere direttamente alle proprietà degli elementi all&#39;interno di una matrice. Pertanto, se è necessario accedere a una proprietà all&#39;interno di un array, il metodo supportato è `select X from array where X.item = ...`. <br> PQL si riserva la parola  `xEvent` per fare riferimento a una serie di eventi esperienza collegati a un profilo. | `[1, 4, 7]`,  `["US", "CA"]` |
| Riferimenti temporali relativi | Parole riservate che possono essere utilizzate per creare riferimenti di marca temporale e di intervallo di tempo. <ul><li>oggi, oggi, ieri, domani</li><li>questo, ultimo, successivo</li><li>prima, dopo</li><li>millisecondi, secondi, minuti, ore, giorni, settimane, mesi, anni, decennio/i, secoli/i</li></ul> | `X.timestamp occurs before today`,  `X.timestamp occurs last month`,  `X.timestamp occurs <= 3 days before now` |


## Funzioni PQL

Nella tabella seguente sono illustrate le diverse categorie di funzioni PQL supportate, compresi i collegamenti verso ulteriori informazioni.

| Categoria | Definizione |
| -------- | ---------- |
| Booleano | Utilizzato per implementare l&#39;algebra booleana in PQL. Ulteriori informazioni su queste funzioni sono disponibili nel documento [funzioni booleane](./boolean-functions.md). |
| Confronto | Utilizzato per confrontare tra diversi elementi PQL. Ulteriori informazioni su queste funzioni sono reperibili nel documento [funzioni di confronto](./comparison-functions.md). |
| Array, list e set | Utilizzato per interagire con array, elenchi e set. Ulteriori informazioni su queste funzioni si trovano nella [matrice, elenco e funzioni impostate document](./array-functions.md). |
| Mappa | Utilizzato per interagire con le mappe. Ulteriori informazioni su queste funzioni sono reperibili nel documento [Mappa funzioni](./map-functions.md). |
| Stringa | Utilizzato per interagire con le stringhe. Ulteriori informazioni su queste funzioni sono reperibili nel documento [funzioni stringa](./string-functions.md). |
| Oggetto | Utilizzato per interagire con gli oggetti. Ulteriori informazioni su queste funzioni sono reperibili nel documento [funzioni oggetto](./object-functions.md). |
| Aritmetica | Utilizzato per eseguire l&#39;aritmetica di base sugli elementi PQL. Ulteriori informazioni su queste funzioni sono reperibili nel documento [funzioni aritmetiche](./arithmetic-functions.md) |
| Aggregazione | Utilizzato per combinare i risultati di un array in un singolo risultato. Ulteriori informazioni sulle funzioni di aggregazione sono disponibili nel documento [funzioni di aggregazione](./aggregation-functions.md). |
| Data e ora | Utilizzato insieme agli oggetti data, ora e data/ora. Ulteriori informazioni su queste funzioni sono reperibili nel [documento delle funzioni data/ora](./datetime-functions.md). |
| Filtro | Utilizzato per filtrare i dati all&#39;interno di array. Ulteriori informazioni su queste funzioni sono reperibili nel documento [delle funzioni filtro](./filter-functions.md). |
| Quantificatori logici | Utilizzato per asserire condizioni all&#39;interno di un array. Ulteriori informazioni sono disponibili nel documento [quantificatori logici](./logical-quantifiers.md). |
| Varie | Le funzioni che non rientrano in nessuna delle categorie di cui sopra si trovano nel documento [funzioni varie](./misc-functions.md). |

## Passaggi successivi

Ora che hai imparato a utilizzare [!DNL Profile Query Language], puoi usare PQL per creare e modificare i segmenti. Per ulteriori informazioni sulla segmentazione, leggere la [panoramica sulla segmentazione](../home.md).