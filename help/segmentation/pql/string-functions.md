---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni stringa;stringa;
solution: Experience Platform
title: Funzioni stringa PQL
topic-legacy: developer guide
description: Il linguaggio PQL (Profile Query Language) offre funzioni che semplificano l’interazione con le stringhe.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 6%

---

# Funzioni stringa

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l’interazione con le stringhe. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Simile

La funzione `like` viene utilizzata per determinare se una stringa corrisponde a un pattern specificato.

**Formato**

```sql
{STRING_1} like {STRING_2}
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa da cui eseguire il controllo. |
| `{STRING_2}` | Espressione da confrontare con la prima stringa. Sono disponibili due caratteri speciali supportati per la creazione di un’espressione: `%` e `_`. <ul><li>`%` viene utilizzato per rappresentare zero o più caratteri.</li><li>`_` viene utilizzato per rappresentare esattamente un carattere.</li></ul> |

**Esempio**

La seguente query PQL recupera tutte le città contenenti il pattern &quot;es&quot;.

```sql
city like "%es%"
```

## Inizia con

La funzione `startsWith` viene utilizzata per determinare se una stringa inizia con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa da cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all’interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è sensibile a maiuscole e minuscole. Per impostazione predefinita, è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se il nome della persona inizia con &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## Non inizia con

La funzione `doesNotStartWith` viene utilizzata per determinare se una stringa non inizia con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa da cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all’interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è sensibile a maiuscole e minuscole. Per impostazione predefinita, è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se il nome della persona non inizia con &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Termina con

La funzione `endsWith` viene utilizzata per determinare se una stringa termina con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa da cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all’interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è sensibile a maiuscole e minuscole. Per impostazione predefinita, è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l’indirizzo e-mail della persona termina con &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## Non termina con

La funzione `doesNotEndWith` viene utilizzata per determinare se una stringa non termina con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa da cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all’interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è sensibile a maiuscole e minuscole. Per impostazione predefinita, è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l’indirizzo e-mail della persona non termina con &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

La funzione `contains` viene utilizzata per determinare se una stringa contiene una sottostringa specificata.

**Formato**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa da cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all’interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è sensibile a maiuscole e minuscole. Per impostazione predefinita, è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l’indirizzo e-mail della persona contiene la stringa &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## Non contiene

La funzione `doesNotContain` viene utilizzata per determinare se una stringa non contiene una sottostringa specificata.

**Formato**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa da cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all’interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è sensibile a maiuscole e minuscole. Per impostazione predefinita, è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l’indirizzo e-mail della persona non contiene la stringa &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## È uguale a

La funzione `equals` viene utilizzata per determinare se una stringa è uguale alla stringa specificata.

**Formato**

```sql
{STRING_1}.equals({STRING_2})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa da cui eseguire il controllo. |
| `{STRING_2}` | Stringa da confrontare con la prima stringa. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se il nome della persona è &quot;John&quot;.

```sql
person.name.equals("John")
```

## Non uguale a

La funzione `notEqualTo` viene utilizzata per determinare se una stringa non è uguale alla stringa specificata.

**Formato**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa da cui eseguire il controllo. |
| `{STRING_2}` | Stringa da confrontare con la prima stringa. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se il nome della persona non è &quot;John&quot;.

```sql
person.name.notEqualTo("John")
```

## Corrisponde

La funzione `matches` viene utilizzata per determinare se una stringa corrisponde a una specifica espressione regolare. Fare riferimento a [questo documento](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) per ulteriori informazioni sui pattern corrispondenti nelle espressioni regolari.

**Formato**

```sql
{STRING_1}.matches(STRING_2})
```

**Esempio**

La seguente query PQL determina, senza distinzione tra maiuscole e minuscole, se il nome della persona inizia con &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

## Gruppo di espressioni regolari

La funzione `regexGroup` viene utilizzata per estrarre informazioni specifiche, in base all&#39;espressione regolare fornita.

**Formato**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Esempio**

La seguente query PQL viene utilizzata per estrarre il nome di dominio da un indirizzo e-mail.

```sql
emailAddress.regexGroup("@(\w+)", 1)
```

## Passaggi successivi

Dopo aver appreso le funzioni stringa, è possibile utilizzarle all&#39;interno delle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consulta la [Panoramica di Profile Query Language](./overview.md).
