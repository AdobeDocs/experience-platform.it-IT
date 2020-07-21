---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Dichiarazioni preparate
topic: prepared statements
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 7%

---


# Dichiarazioni preparate

In SQL, le istruzioni preparate vengono utilizzate per modellare query o aggiornamenti simili.  Adobe Experience Platform [!DNL Query Service] supporta le istruzioni preparate utilizzando una query con parametri. Questo può essere utilizzato per ottimizzare le prestazioni, in quanto non sarà più necessario ripetere continuamente l&#39;analisi di una query.

## Uso di istruzioni preparate

Quando si utilizzano le istruzioni preparate, sono supportate le seguenti sintassi:

- [PREPARARE](#prepare)
- [ESECUZIONE](#execute)
- [DEALLOCATE](#deallocate)

### Preparare una dichiarazione preparata {#prepare}

Questa query SQL salva la query SELECT scritta con il nome specificato come `PLAN_NAME`. È possibile utilizzare le variabili, ad esempio `$1` al posto dei valori effettivi. Questa istruzione preparata verrà salvata durante la sessione corrente. I nomi dei piani **non** fanno distinzione tra maiuscole e minuscole.

#### Formato SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### Esempio di SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Esecuzione di un&#39;istruzione preparata {#execute}

Questa query SQL utilizza l&#39;istruzione preparata creata in precedenza.

#### Formato SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### Esempio di SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### Disallocare un&#39;istruzione preparata {#deallocate}

Questa query SQL viene utilizzata per eliminare l&#39;istruzione preparata denominata.

#### Formato SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### Esempio di SQL

```sql
DEALLOCATE test;
```

## Esempio di flusso utilizzando le istruzioni preparate

Inizialmente, potete disporre di una query SQL, come quella riportata di seguito:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

La query SQL precedente restituirà la risposta seguente:

| id | firstName | lastname | natalità | email | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canada |
| 10001 | antoina | dubois | 1967-03-14 | example2@example.com | Paris | Francia |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Giappone |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stoccolma | Svezia |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenya |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Cile |

Questa query SQL può essere parametrizzata utilizzando la seguente istruzione preparata:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

A questo punto, l&#39;istruzione preparata può essere eseguita utilizzando la seguente chiamata:

```sql
EXECUTE getIdRange(10000, 10005);
```

Quando viene chiamato, si vedranno esattamente gli stessi risultati di prima:

| id | firstName | lastname | natalità | email | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canada |
| 10001 | antoina | dubois | 1967-03-14 | example2@example.com | Paris | Francia |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Giappone |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stoccolma | Svezia |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenya |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Cile |

Dopo aver completato l&#39;istruzione preparata, è possibile deallocarla utilizzando la seguente chiamata:

```sql
DEALLOCATE getIdRange;
```
