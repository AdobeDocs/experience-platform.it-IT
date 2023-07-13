---
solution: Experience Platform
title: Funzioni stringa PQL
description: PQL (Profile Query Language) offre funzioni per semplificare l’interazione con le stringhe.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 6%

---

# Funzioni stringa

[!DNL Profile Query Language] (PQL) offre funzioni per semplificare l’interazione con le stringhe. Ulteriori informazioni su altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Mi piace

Il `like` viene utilizzata per determinare se una stringa corrisponde a un pattern specificato.

**Formato**

```sql
{STRING_1} like {STRING_2}
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Espressione da confrontare con la prima stringa. Per creare un’espressione sono disponibili due caratteri speciali supportati: `%` e `_`. <ul><li>`%` viene utilizzato per rappresentare zero o più caratteri.</li><li>`_` viene utilizzato per rappresentare esattamente un carattere.</li></ul> |

**Esempio**

La seguente query PQL recupera tutte le città contenenti il pattern &quot;es&quot;.

```sql
city like "%es%"
```

## Inizia con

Il `startsWith` viene utilizzata per determinare se una stringa inizia con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare nella prima stringa. |
| `{BOOLEAN}` | Un parametro opzionale per determinare se il controllo distingue tra maiuscole e minuscole. Per impostazione predefinita, questo è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se il nome della persona inizia con &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## Non inizia con

Il `doesNotStartWith` La funzione viene utilizzata per determinare se una stringa non inizia con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare nella prima stringa. |
| `{BOOLEAN}` | Un parametro opzionale per determinare se il controllo distingue tra maiuscole e minuscole. Per impostazione predefinita, questo è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se il nome della persona non inizia con &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Termina con

Il `endsWith` viene utilizzata per determinare se una stringa termina con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare nella prima stringa. |
| `{BOOLEAN}` | Un parametro opzionale per determinare se il controllo distingue tra maiuscole e minuscole. Per impostazione predefinita, questo è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l’indirizzo e-mail della persona termina con &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## Non termina con

Il `doesNotEndWith` La funzione viene utilizzata per determinare se una stringa non termina con una sottostringa specificata.

**Formato**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare nella prima stringa. |
| `{BOOLEAN}` | Un parametro opzionale per determinare se il controllo distingue tra maiuscole e minuscole. Per impostazione predefinita, questo è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l’indirizzo e-mail della persona non termina con &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

Il `contains` La funzione viene utilizzata per determinare se una stringa contiene una sottostringa specificata.

**Formato**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare nella prima stringa. |
| `{BOOLEAN}` | Un parametro opzionale per determinare se il controllo distingue tra maiuscole e minuscole. Per impostazione predefinita, questo è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l’indirizzo e-mail della persona contiene la stringa &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## Non contiene

Il `doesNotContain` La funzione viene utilizzata per determinare se una stringa non contiene una sottostringa specificata.

**Formato**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{STRING_1}` | Stringa su cui eseguire il controllo. |
| `{STRING_2}` | Stringa da cercare nella prima stringa. |
| `{BOOLEAN}` | Un parametro opzionale per determinare se il controllo distingue tra maiuscole e minuscole. Per impostazione predefinita, questo è impostato su true. |

**Esempio**

La seguente query PQL determina, con distinzione tra maiuscole e minuscole, se l’indirizzo e-mail della persona non contiene la stringa &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## È uguale a

Il `equals` viene utilizzata per determinare se una stringa è uguale alla stringa specificata.

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

## Diverso da

Il `notEqualTo` viene utilizzata per determinare se una stringa non è uguale alla stringa specificata.

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

Il `matches` viene utilizzata per determinare se una stringa corrisponde a una specifica espressione regolare. Fare riferimento a [questo documento](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) per ulteriori informazioni sui pattern corrispondenti nelle espressioni regolari, vedere.

**Formato**

```sql
{STRING_1}.matches(STRING_2})
```

**Esempio**

La seguente query PQL determina, senza distinzione tra maiuscole e minuscole, se il nome della persona inizia con &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Se utilizzi funzioni di espressione regolare come `\w`, tu **deve** escape del carattere barra rovesciata. Quindi, invece di scrivere solo `\w`, è necessario includere una barra rovesciata aggiuntiva e scrivere `\\w`.

## Gruppo di espressioni regolari

Il `regexGroup` La funzione viene utilizzata per estrarre informazioni specifiche, in base all’espressione regolare fornita.

**Formato**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Esempio**

La seguente query PQL viene utilizzata per estrarre il nome di dominio da un indirizzo e-mail.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>Se utilizzi funzioni di espressione regolare come `\w`, tu **deve** escape del carattere barra rovesciata. Quindi, invece di scrivere solo `\w`, è necessario includere una barra rovesciata aggiuntiva e scrivere `\\w`.

## Passaggi successivi

Ora che hai imparato le funzioni stringa, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni PQL, leggere [Panoramica sulla lingua delle query di profilo](./overview.md).
