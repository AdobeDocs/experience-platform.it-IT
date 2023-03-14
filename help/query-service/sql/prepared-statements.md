---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;istruzioni preparate;preparato;sql;
solution: Experience Platform
title: Istruzioni preparate in Query Service
description: In SQL, le istruzioni preparate vengono utilizzate per creare modelli di query o aggiornamenti simili. Adobe Experience Platform Query Service supporta le istruzioni preparate tramite una query con parametri.
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 8%

---

# Istruzioni preparate

In SQL, le istruzioni preparate vengono utilizzate per creare modelli di query o aggiornamenti simili. Adobe Experience Platform [!DNL Query Service] supporta le istruzioni preparate utilizzando una query con parametri. In questo modo è possibile ottimizzare le prestazioni, poiché non è più necessario ripetere ripetutamente l’analisi di una query.

## Utilizzo di istruzioni preparate

Quando si utilizzano le istruzioni preparate, sono supportate le seguenti sintassi:

- [PREPARA](#prepare)
- [ESEGUI](#execute)
- [DEALLOCARE](#deallocate)

### Prepara un rendiconto preparato {#prepare}

Questa query SQL salva la query SELECT scritta con il nome specificato come `PLAN_NAME`. Puoi utilizzare variabili, come `$1` al posto dei valori effettivi. L&#39;istruzione preparata verrà salvata durante la sessione corrente. I nomi dei piani sono **non** distinzione tra maiuscole e minuscole.

#### Formato SQL

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### SQL di esempio

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Eseguire un&#39;istruzione preparata {#execute}

Questa query SQL utilizza l&#39;istruzione preparata creata in precedenza.

#### Formato SQL

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### SQL di esempio

```sql
EXECUTE test('canada', 'vancouver');
```

### Disallocare un rendiconto preparato {#deallocate}

Questa query SQL viene utilizzata per eliminare l&#39;istruzione preparata denominata.

#### Formato SQL

```sql
DEALLOCATE {PLAN_NAME}
```

#### SQL di esempio

```sql
DEALLOCATE test;
```

## Flusso di esempio con istruzioni preparate

Inizialmente, è possibile disporre di una query SQL, come quella riportata di seguito:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

La query SQL precedente restituirà la seguente risposta:

| id | nome | cognome | data di nascita | e-mail | città | paese |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alessandro | davis | 1993-09-15 | example@example.com | Vancouver | Canada |
| 10001 | antoina | dubois | 1967-03-14 | example2@example.com | Parigi | Francia |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Giappone |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stoccolma | Svezia |
| 10004 | asir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenya |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Cile |

Questa query SQL può essere parametrizzata utilizzando la seguente istruzione preparata:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Ora, l’istruzione preparata può essere eseguita utilizzando la seguente chiamata:

```sql
EXECUTE getIdRange(10000, 10005);
```

Quando viene richiamato, vedrai gli stessi risultati di prima:

| id | nome | cognome | data di nascita | e-mail | città | paese |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alessandro | davis | 1993-09-15 | example@example.com | Vancouver | Canada |
| 10001 | antoina | dubois | 1967-03-14 | example2@example.com | Parigi | Francia |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Giappone |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stoccolma | Svezia |
| 10004 | asir | waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenya |
| 10005 | fernando | rios | 2002-07-30 | example6@example.com | Santiago | Cile |

Dopo aver terminato di utilizzare l&#39;istruzione preparata, è possibile deallocarla utilizzando la chiamata seguente:

```sql
DEALLOCATE getIdRange;
```
