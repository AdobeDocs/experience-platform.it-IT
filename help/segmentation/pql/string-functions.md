---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni stringa
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 6%

---


# Funzioni stringa

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l&#39;interazione con le stringhe. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella panoramica [Lingua query](./overview.md)profilo.

## Simile

La `like` funzione viene utilizzata per determinare se una stringa corrisponde a un pattern specificato.

**Formato**

```sql
{STRING_1} like {STRING_2}
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | L&#39;espressione da confrontare con la prima stringa. Esistono due caratteri speciali supportati per la creazione di un&#39;espressione: `%` e `_`. <ul><li>`%` viene utilizzato per rappresentare zero o più caratteri.</li><li>`_` viene utilizzato per rappresentare esattamente un carattere.</li></ul> |

**Esempio**

La seguente query PQL recupera tutte le città contenenti il pattern &quot;es&quot;.

```sql
city like "%es%"
```

## Inizia con

La `startsWith` funzione viene utilizzata per determinare se una stringa inizia con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all&#39;interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è basato sulla distinzione tra maiuscole e minuscole. Per impostazione predefinita, è impostata su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se il nome della persona inizia con &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## Non inizia con

La `doesNotStartWith` funzione viene utilizzata per determinare se una stringa non inizia con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all&#39;interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è basato sulla distinzione tra maiuscole e minuscole. Per impostazione predefinita, è impostata su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se il nome della persona non inizia con &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Termina con

La `endsWith` funzione viene utilizzata per determinare se una stringa termina con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all&#39;interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è basato sulla distinzione tra maiuscole e minuscole. Per impostazione predefinita, è impostata su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l&#39;indirizzo e-mail della persona termina con &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## Non termina con

La `doesNotEndWith` funzione viene utilizzata per determinare se una stringa non termina con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all&#39;interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è basato sulla distinzione tra maiuscole e minuscole. Per impostazione predefinita, è impostata su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l&#39;indirizzo e-mail della persona non termina con &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contiene

La `contains` funzione viene utilizzata per determinare se una stringa contiene una sottostringa specificata.

**Formato**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all&#39;interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è basato sulla distinzione tra maiuscole e minuscole. Per impostazione predefinita, è impostata su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l&#39;indirizzo e-mail della persona contiene la stringa &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## Non contiene

La `doesNotContain` funzione viene utilizzata per determinare se una stringa non contiene una sottostringa specificata.

**Formato**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare all&#39;interno della prima stringa. |
| `{BOOLEAN}` | Un parametro facoltativo per determinare se il controllo è basato sulla distinzione tra maiuscole e minuscole. Per impostazione predefinita, è impostata su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l&#39;indirizzo e-mail della persona non contiene la stringa &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## È uguale a

La `equals` funzione viene utilizzata per determinare se una stringa è uguale alla stringa specificata.

**Formato**

```sql
{STRING_1}.equals({STRING_2})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da confrontare con la prima stringa. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se il nome della persona è &quot;John&quot;.

```sql
person.name.equals("John")
```

## Non uguale a

La `notEqualTo` funzione viene utilizzata per determinare se una stringa non è uguale alla stringa specificata.

**Formato**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da confrontare con la prima stringa. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se il nome della persona non è &quot;John&quot;.

```sql
person.name.notEqualTo("John")
```

## Corrisponde

La `matches` funzione viene utilizzata per determinare se una stringa corrisponde a una specifica espressione regolare. Per ulteriori informazioni sui pattern di corrispondenza nelle espressioni regolari, fare riferimento a [questo documento](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) .

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

La `regexGroup` funzione viene utilizzata per estrarre informazioni specifiche, in base all&#39;espressione regolare fornita.

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

Ora che hai imparato le funzioni stringa, puoi usarle nelle tue query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.

