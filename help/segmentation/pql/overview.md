---
keywords: Experience Platform;home;argomenti popolari;PQL;pql;linguaggio di query profilo
solution: Experience Platform
title: Panoramica di PQL (Profile Query Language)
topic-legacy: developer guide
description: Questa guida fornisce una panoramica generale di PQL, comprensiva delle linee guida per la formattazione e della fornitura di espressioni PQL di esempio.
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---

# [!DNL Profile Query Language] Panoramica (PQL)

[!DNL Profile Query Language] (PQL) è un [!DNL Experience Data Model] Linguaggio di query conforme a (XDM) progettato per supportare la definizione e l’esecuzione di query di segmentazione per [!DNL Real-Time Customer Profile] dati.

Questa guida fornisce una panoramica generale di PQL, comprensiva delle linee guida per la formattazione e della fornitura di espressioni PQL di esempio.

## Formattazione query PQL

Le query PQL dispongono della firma seguente:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

Il parametro di input può essere un primitivo semplice, ad esempio un valore booleano o una stringa, o un tipo più complesso, ad esempio un oggetto, un array o una mappa.

Esistono tre modi diversi per fare riferimento ai parametri di input all’interno del corpo di un’espressione PQL:

### Riferimento implicito al primo parametro

Nell&#39;esempio seguente, poiché il primo parametro è sempre nel contesto, un riferimento a una proprietà (`homeAddress`) può essere effettuata direttamente su di essa.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Riferimento esplicito al primo parametro

Nell’esempio seguente: `$1` fa riferimento al primo parametro. Di conseguenza, `$2` fa riferimento al secondo parametro, ecc.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Utilizzo di variabili denominate, utilizzando la notazione lambda

Nell’esempio seguente: `Profile` è un nome di variabile, che può essere scelto dall’autore della query.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Valori letterali PQL

PQL supporta i seguenti tipi letterali:

| Letterale | Definizione | Esempio |
| ------- | ---------- | ------- |
| Stringa | Tipo di dati composto da caratteri racchiusi tra virgolette doppie. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booleano | Tipo di dati vero o falso. | `true`, `false` |
| Intero | Tipo di dati che rappresenta un numero intero. Può essere positivo, negativo o zero. | `-201`, `0`, `412` |
| Doppio | Tipo di dati che rappresenta qualsiasi numero reale. Può essere positivo, negativo o zero. | `-51.24`, `3.14`, `0.6942058` |
| Data | Tipo di dati che può essere utilizzato per creare date basate su anno, mese e giorno come parametri interi. È formattato come `date(year, month, day)` | `date(2020, 3, 14)` |
| Array | Tipo di dati composto da un gruppo di altri valori letterali. Utilizza parentesi quadre per raggruppare e virgole per delimitare valori diversi. <br> **Nota:** Non è possibile accedere direttamente alle proprietà degli elementi all&#39;interno di una matrice. Pertanto, se è necessario accedere a una proprietà all&#39;interno di una matrice, il metodo supportato è `select X from array where X.item = ...`. <br> PQL riserva la parola `xEvent` per fare riferimento a una matrice di eventi di esperienza collegati a un profilo. | `[1, 4, 7]`, `["US", "CA"]` |
| Riferimenti temporali relativi | Parole riservate che possono essere utilizzate per creare riferimenti a marca temporale e a intervalli di tempo. <ul><li>ora, oggi, ieri, domani</li><li>questo, ultimo, successivo</li><li>prima, dopo,</li><li>millisecondi, secondo(i), minuto(i), ora(i), giorno(i), settimana(i), mese(i), anno(i), decennio(i), secolo/secoli, millennio/millenni</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## Funzioni PQL

La tabella seguente illustra le diverse categorie di funzioni PQL supportate, compresi i collegamenti a ulteriori informazioni.

| Categoria | Definizione |
| -------- | ---------- |
| Booleano | Utilizzato per implementare l’algebra booleana in PQL. Ulteriori informazioni su queste funzioni sono disponibili nella sezione [documento sulle funzioni booleane](./boolean-functions.md). |
| Confronto | Utilizzato per confrontare tra diversi elementi PQL. Ulteriori informazioni su queste funzioni sono disponibili nella sezione [documento sulle funzioni di confronto](./comparison-functions.md). |
| Array, list e set | Utilizzato per interagire con array, elenchi e set. Ulteriori informazioni su queste funzioni sono disponibili nella sezione [documento delle funzioni array, elenco e set](./array-functions.md). |
| Mappa | Usato per interagire con le mappe. Ulteriori informazioni su queste funzioni sono disponibili nella sezione [documento sulle funzioni mappa](./map-functions.md). |
| Stringa | Utilizzato per interagire con le stringhe. Ulteriori informazioni su queste funzioni sono disponibili nella sezione [documento sulle funzioni stringa](./string-functions.md). |
| Oggetto | Utilizzato per interagire con gli oggetti. Ulteriori informazioni su queste funzioni sono disponibili nella sezione [documento sulle funzioni oggetto](./object-functions.md). |
| Aritmetica | Utilizzato per eseguire l’aritmetica di base sugli elementi PQL. Ulteriori informazioni su queste funzioni sono disponibili nella sezione [documento sulle funzioni aritmetiche](./arithmetic-functions.md) |
| Aggregazione | Utilizzato per combinare i risultati di un array in un singolo risultato. Ulteriori informazioni sulle funzioni di aggregazione sono disponibili nella sezione [documento sulle funzioni di aggregazione](./aggregation-functions.md). |
| Data e ora | Utilizzato in combinazione con oggetti data, ora e datetime. Ulteriori informazioni su queste funzioni sono disponibili nella sezione [documento sulle funzioni data/ora](./datetime-functions.md). |
| Filtro | Utilizzato per filtrare i dati all’interno di array. Ulteriori informazioni su queste funzioni sono disponibili nella sezione [documento sulle funzioni di filtro](./filter-functions.md). |
| quantificatori logici | Utilizzato per affermare condizioni all&#39;interno di un array. Ulteriori informazioni sono disponibili nella sezione [documento quantificatori logici](./logical-quantifiers.md). |
| Varie | Le funzioni che non rientrano in nessuna delle categorie di cui sopra si trovano nella [documento sulle funzioni varie](./misc-functions.md). |

## Passaggi successivi

Ora che hai imparato ad usare [!DNL Profile Query Language], puoi utilizzare PQL per creare e modificare i segmenti. Per ulteriori informazioni sulla segmentazione, consulta la sezione [panoramica sulla segmentazione](../home.md).
