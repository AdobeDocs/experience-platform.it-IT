---
solution: Experience Platform
title: Panoramica di Profile Query Language (PQL)
description: Questa guida fornisce una panoramica generale di PQL, illustrando le linee guida per la formattazione e fornendo espressioni PQL di esempio.
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 3%

---

# [!DNL Profile Query Language] (PQL) panoramica

[!DNL Profile Query Language] (PQL) è un linguaggio di query conforme a [!DNL Experience Data Model] (XDM) progettato per supportare la definizione e l&#39;esecuzione di query di segmentazione per dati [!DNL Real-Time Customer Profile].

Questa guida fornisce una panoramica generale di PQL, illustrando le linee guida per la formattazione e fornendo espressioni PQL di esempio.

## Formattazione query PQL

Le query PQL hanno la seguente firma:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

Il parametro di input può essere un semplice valore primitivo, ad esempio booleano o stringa, oppure un tipo più complesso, ad esempio un oggetto, un array o una mappa.

Esistono tre modi diversi per fare riferimento ai parametri di input all’interno del corpo di un’espressione PQL:

### Riferimento implicito al primo parametro

Nell&#39;esempio seguente, poiché il primo parametro è sempre nel contesto, è possibile fare riferimento direttamente a una proprietà (`homeAddress`).

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Riferimento esplicito al primo parametro

Nell&#39;esempio seguente, `$1` fa riferimento al primo parametro. Di conseguenza, `$2` farebbe riferimento al secondo parametro e così via.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Utilizzo di variabili denominate, utilizzando la notazione lambda

Nell&#39;esempio seguente, `Profile` è un nome di variabile, che può essere scelto dall&#39;autore della query.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Valori letterali PQL

PQL fornisce supporto per i seguenti tipi letterali:

| Letterale | Definizione | Esempio |
| ------- | ---------- | ------- |
| Stringa | Tipo di dati costituito da caratteri racchiusi tra virgolette doppie. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booleano | Tipo di dati true o false. | `true`, `false` |
| Intero | Tipo di dati che rappresenta un numero intero. Può essere positivo, negativo o zero. | `-201`, `0`, `412` |
| Doppio | Tipo di dati che rappresenta qualsiasi numero reale. Può essere positivo, negativo o zero. | `-51.24`, `3.14`, `0.6942058` |
| Data | Tipo di dati che può essere utilizzato per creare date basate su parametri di anno, mese e giorno come valori interi. È formattato come `date(year, month, day)` | `date(2020, 3, 14)` |
| Array | Tipo di dati composto da un gruppo di altri valori letterali. Utilizza parentesi quadre per raggruppare e virgole per delimitare tra valori diversi. <br> **Nota:** non è possibile accedere direttamente alle proprietà degli elementi all&#39;interno di un array. Pertanto, se è necessario accedere a una proprietà all&#39;interno di un array, il metodo supportato è `select X from array where X.item = ...`. <br> PQL riserva la parola `xEvent` per fare riferimento a un array di eventi esperienza collegati a un profilo. | `[1, 4, 7]`, `["US", "CA"]` |
| Riferimenti temporali relativi | Parole riservate che possono essere utilizzate per creare riferimenti a marche temporali e intervalli di tempo. <ul><li>oggi, ieri, domani</li><li>questo, ultimo, prossimo</li><li>prima, dopo, da</li><li>millisecondo/i, secondo/i, minuto/i, ora/i, giorno/i, settimana/e, mese/i, anno/i, decennio/i, secolo/secoli, millennio/millenni</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |

## Funzioni PQL

La tabella seguente illustra le diverse categorie di funzioni di PQL supportate, inclusi i collegamenti a ulteriore documentazione per ulteriori informazioni.

| Categoria | Definizione |
| -------- | ---------- |
| Booleano | Utilizzato per implementare l’algebra booleana in PQL. Ulteriori informazioni su queste funzioni sono disponibili nel [documento sulle funzioni booleane](./boolean-functions.md). |
| Confronto | Utilizzato per confrontare tra diversi elementi di PQL. Ulteriori informazioni su queste funzioni sono disponibili nel documento [funzioni di confronto](./comparison-functions.md). |
| Array, elenco e set | Utilizzato per interagire con array, elenchi e set. Ulteriori informazioni su queste funzioni sono disponibili nel documento [array, list e set functions](./array-functions.md). |
| Mappa | Utilizzato per interagire con le mappe. Ulteriori informazioni su queste funzioni sono disponibili nel documento [funzioni mappa](./map-functions.md). |
| Stringa | Utilizzato per interagire con le stringhe. Ulteriori informazioni su queste funzioni sono disponibili nel documento [funzioni stringa](./string-functions.md). |
| Oggetto | Utilizzato per interagire con gli oggetti. Ulteriori informazioni su queste funzioni sono disponibili nel documento [funzioni oggetto](./object-functions.md). |
| Aritmetica | Utilizzato per eseguire operazioni aritmetiche di base sugli elementi di PQL. Ulteriori informazioni su queste funzioni sono disponibili nel [documento sulle funzioni aritmetiche](./arithmetic-functions.md) |
| Aggregazione | Utilizzato per combinare i risultati di un array in un singolo risultato. Ulteriori informazioni sulle funzioni di aggregazione sono disponibili nel documento [funzioni di aggregazione](./aggregation-functions.md). |
| Data e ora | Utilizzato insieme a oggetti data, ora e datetime. Ulteriori informazioni su queste funzioni sono disponibili nel documento [funzioni data/ora](./datetime-functions.md). |
| Filtro | Utilizzato per filtrare i dati all’interno di array. Ulteriori informazioni su queste funzioni sono disponibili nel documento [funzioni filtro](./filter-functions.md). |
| Quantificatori logici | Utilizzato per affermare le condizioni all’interno di un array. Ulteriori informazioni sono disponibili nel [documento sui quantificatori logici](./logical-quantifiers.md). |
| Varie | Le funzioni che non rientrano in nessuna delle categorie precedenti sono disponibili nel [documento funzioni varie](./misc-functions.md). |

## Passaggi successivi

Dopo aver appreso come utilizzare [!DNL Profile Query Language], è possibile utilizzare PQL per creare e modificare le definizioni dei segmenti. Per ulteriori informazioni sulla segmentazione, consulta la [panoramica sulla segmentazione](../home.md).
